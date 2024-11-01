---
layout: post
title: JWT with PHP
description: JWT with PHP
date: 2024-10-21 12:30:00 +0900
categories: [Technical Labs]
tags: [JWT, PHP]
pin: false
math: false
mermaid: false
image:
  path: commons/php-jwt/title.png
  alt: HTTP(Hypertext Transfer Protocol)
---
<!-- categories: [Technical Concepts Summarized, Technical Labs, Technical Terms, Useful Apps To Help With Technology] -->

## Prerequisites
- JWT에 대한 기본 개념에 대한 내용은 [JWT(JSON Web Tokens)](/posts/JWT/)에서 볼 수 있습니다.
- 쿠키와 세션, 그리고 이를 이용한 stateless인 HTTP에서 로그인을 유지 하는 방법에 대한 이해가 필요합니다. 이에 관한 내용은 [cookie & session](/posts/cookie-session)를 보시면 됩니다.
- 이 포스팅에서는 지난 포스팅[PHP-Basic](/posts/PHP-basic)에서 했던 프로젝트에 JWT를 적용해봅니다.

## Overview
JWT가 만능은 아닙니다. [JWT(JSON Web Tokens)](/posts/JWT/)에서 볼 수 있듯이 세션에 비해 단점도 있기 때문에 무조건적으로 JWT로 전환할 수는 없습니다. 따라서 이번 포스팅에서는 세션에서 JWT로의 수정이 아닌 JWT 인증을 추가하여 인증 방식을 스위칭할 수 있게 해봤습니다.


## Summary
JWT 라이브러리 설치
```shell
// 라이브러리 설치 (사용자 프로젝트 루트 폴더에서 명령)
composer require firebase/php-jwt

// docker-compose 사용시 라이브러리 설치
sudo docker-compose exec -w /app lamp composer require firebase/php-jwt

// 아파치 재시작
service apache2 restart
or
apache2ctl restart

// docker-compose 사용시 아파치 재시작
sudo docker-compose exec lamp service apache2 restart
or
sudo docker-compose exec lamp apache2ctl restart
```

토큰을 생성하여 사용자 정보 저장
```php
 $payload = array(
    "user_id" => $user['id'],               // 사용자 ID 저장
    "email" => $user['email'],              // 사용자 이메일 저장
    "exp" => time() + JWT_EXPIRE_TIME       // 만료 시간 설정
);
$jwt = JWT::encode($payload, JWT_SECRET_KEY, 'HS256');  // JWT 토큰 생성

if (version_compare(PHP_VERSION, '7.3.0', '>=')) {      // PHP 버전 7.3 이상 확인
    setcookie(
        'jwt_token',                                    // 쿠키 이름
        $jwt,                                           // 토큰 값
        [
            'expires' => time() + JWT_EXPIRE_TIME,      // 만료 시간
            'path' => '/',                              // 쿠키 경로
            'secure' => false,                          // HTTPS 필요 여부
            'httponly' => true,                         // JS 접근 제한
            'samesite' => 'Lax'                         // CSRF 보호
        ]
    );
} else {                           // PHP 7.3 미만 버전
    setcookie(
        'jwt_token',               // 쿠키 이름
        $jwt,                      // 토큰 값
        time() + JWT_EXPIRE_TIME,  // 만료 시간
        '/',                       // 쿠키 경로
        '',                        // 도메인
        false,                     // HTTPS 필요 여부
        true                       // JS 접근 제한
    );
}
```

토큰을 검증하여 사용자 확인
```php
if (!isset($_COOKIE['jwt_token'])) {  // JWT 토큰 존재 확인
    return false;                     // 없으면 false 반환
}
try {
    $jwt = $_COOKIE['jwt_token'];                               // 쿠키에서 토큰 추출
    return JWT::decode($jwt, new Key(JWT_SECRET_KEY, 'HS256')); // 토큰 검증
} catch (Exception $e) {                                        // 검증 실패시
    return false;                                               // false 반환
}
```

토큰 삭제
```php
if (AUTH_METHOD === 'jwt') {                          // JWT 인증 방식일 경우
    setcookie('jwt_token', '', time() - 3600, '/');   // JWT 쿠키 삭제
} else {                                              // 세션 인증 방식일 경우
    session_start();                                  // 세션 시작
    session_destroy();                                // 세션 파괴
}
```


## Modify a project
**config.php**
```php
<?php
require_once __DIR__ . '/vendor/autoload.php'; // 오토로더 불러오기
use Firebase\JWT\JWT;                          // JWT 클래스 사용
use Firebase\JWT\Key;                          // JWT Key 클래스 사용

$servername = "localhost"; // 데이터베이스 서버 주소
$username = "admin";       // 데이터베이스 사용자 이름
$password = "student1234"; // 데이터베이스 비밀번호
$dbname = "mydatabase";    // 데이터베이스 이름

$conn = mysqli_connect($servername, $username, $password, $dbname); // 데이터베이스 연결 생성

if (!$conn) {                                             // 연결 확인
    die("Connection failed: " . mysqli_connect_error());  // 연결 실패시 오류 메시지 출력
}

define('AUTH_METHOD', 'session');                   // 인증 방식 설정: 'session' 또는 'jwt'
define('JWT_SECRET_KEY', 'your-secret-key-here');   // JWT 암호화 키 (실제 운영시 변경 필요)
define('JWT_EXPIRE_TIME', 3600);                    // JWT 토큰 만료 시간 (초)

function setAuth($user) {                           // 사용자 인증 설정 함수
    if (AUTH_METHOD === 'jwt') {                    // JWT 인증 방식일 경우
        $payload = array(
            "user_id" => $user['id'],               // 사용자 ID 저장
            "email" => $user['email'],              // 사용자 이메일 저장
            "exp" => time() + JWT_EXPIRE_TIME       // 만료 시간 설정
        );
        $jwt = JWT::encode($payload, JWT_SECRET_KEY, 'HS256');  // JWT 토큰 생성

        if (version_compare(PHP_VERSION, '7.3.0', '>=')) {      // PHP 버전 7.3 이상 확인
            setcookie(
                'jwt_token',                                    // 쿠키 이름
                $jwt,                                           // 토큰 값
                [
                    'expires' => time() + JWT_EXPIRE_TIME,      // 만료 시간
                    'path' => '/',                              // 쿠키 경로
                    'secure' => false,                          // HTTPS 필요 여부
                    'httponly' => true,                         // JS 접근 제한
                    'samesite' => 'Lax'                         // CSRF 보호
                ]
            );
        } else {                           // PHP 7.3 미만 버전
            setcookie(
                'jwt_token',               // 쿠키 이름
                $jwt,                      // 토큰 값
                time() + JWT_EXPIRE_TIME,  // 만료 시간
                '/',                       // 쿠키 경로
                '',                        // 도메인
                false,                     // HTTPS 필요 여부
                true                       // JS 접근 제한
            );
        }
    } else {                                 // 세션 인증 방식일 경우
        session_start();                     // 세션 시작
        $_SESSION['user_id'] = $user['id'];  // 세션에 사용자 ID 저장
        $_SESSION['email'] = $user['email']; // 세션에 이메일 저장
    }
}

function getAuth() {                          // 인증 정보 조회 함수
    if (AUTH_METHOD === 'jwt') {              // JWT 인증 방식일 경우
        if (!isset($_COOKIE['jwt_token'])) {  // JWT 토큰 존재 확인
            return false;                     // 없으면 false 반환
        }
        try {
            $jwt = $_COOKIE['jwt_token'];                               // 쿠키에서 토큰 추출
            return JWT::decode($jwt, new Key(JWT_SECRET_KEY, 'HS256')); // 토큰 검증
        } catch (Exception $e) {                                        // 검증 실패시
            return false;                                               // false 반환
        }
    } else {                                                   // 세션 인증 방식일 경우
        session_start();                                       // 세션 시작
        return isset($_SESSION['user_id']) ? [                 // 세션 정보 반환
            'user_id' => $_SESSION['user_id'],
            'email' => $_SESSION['email']
        ] : false;
    }
}

function clearAuth() {                                    // 인증 정보 삭제 함수
    if (AUTH_METHOD === 'jwt') {                          // JWT 인증 방식일 경우
        setcookie('jwt_token', '', time() - 3600, '/');   // JWT 쿠키 삭제
    } else {                                              // 세션 인증 방식일 경우
        session_start();                                  // 세션 시작
        session_destroy();                                // 세션 파괴
    }
}

function requireAuth() {                 // 인증 필수 확인 함수
    $user = getAuth();                   // 인증 정보 확인
    if (!$user) {                        // 인증되지 않은 경우
        header('Location: /signin.php'); // 로그인 페이지로 이동
        exit();                          // 스크립트 종료
    }
    return $user;                        // 인증 정보 반환
}

?>

?>
```

**signin.php**
```php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $email = mysqli_real_escape_string($conn, $_POST['email']);
  $password = mysqli_real_escape_string($conn, $_POST['password']);
  $query = "SELECT * FROM users WHERE email = '$email'";
  $result = mysqli_query($conn, $query);
  $user = mysqli_fetch_assoc($result);
  mysqli_close($conn);

  error_log('user: ' . json_encode($user));
  if ($user && password_verify($password, $user['password'])) {
    setAuth($user); // 통합된 인증 설정 함수 사용
    header('Location: main.php');
    exit();
  } else {
    echo "<script>alert('Incorrect email or password'); window.location.href='signin.php';</script>";
    exit();
  }
}
?>
```

**singup.php**  
변경 사항 없음

**main.php**
```php
<?php
require_once 'config.php';

$user = requireAuth(); // 통합된 인증 정보 확인 함수 사용
$email = $user->email;

$query = "SELECT * FROM users WHERE email = '$email'";
$result = mysqli_query($conn, $query);
$user = mysqli_fetch_assoc($result);
$username = htmlspecialchars($user["username"]);
mysqli_close($conn);

?>
```

**setting.php**
```php
<?php
require_once 'config.php';

$user = requireAuth(); // 통합된 인증 정보 확인 함수 사용
$email = $user->email;

$sql = "SELECT username, email, gender, welcome_message FROM users LIMIT 1";
$result = mysqli_query($conn, $sql);

if ($row = mysqli_fetch_assoc($result)) {
  $username = htmlspecialchars($row["username"]);
  $email = htmlspecialchars($row["email"]);
  $gender = htmlspecialchars($row["gender"]);
  $welcome_message = htmlspecialchars($row["welcome_message"]);
} else {
  echo "No records found";
}

mysqli_close($conn);

?>
```

**signout.php**
```php
<?php
require_once 'config.php';

clearAuth();  // 통합된 로그아웃 함수 사용
header('Location: signin.php');
exit();
?>
```

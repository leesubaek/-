https://github.com/leesubaek/-/blob/main/README.md

pnp로 간단한 로그인 페이지 만들기 [Uploading login.php…]()
1.login.php
-> 처음 로그인 하는 페이지 
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        form {
            background-color: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
            text-align: center; 
        }

        h2 {
            text-align: center;
            color: #333;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #555;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 16px;
            box-sizing: border-box;
        }

        button {
            background-color: #4caf50;
            color: #fff;
            padding: 10px;
            border: none;
            border-radius: 3px;
            cursor: pointer;
            width: 100%;
        }

        a {
            text-decoration: none;
            color: #007bff;
        }

        .links {
            text-align: center;
            color: 
            margin-top: 20px;
        }

        .links p {
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <form action="dashboard.php" method="get">
        <h2>로그인</h2>
        <label for="username">이름</label>
        <input type="text" id="username" name="username" required>

        <label for="password">비밀번호</label>
        <input type="password" id="password" name="password" required>

        <button type="submit">로그인</button>
        
        
    </form>
   
</body>
</html>

2.db.php
<?php

$host = 'localhost'; 
$dbname = 'login_page'; 
$username = 'root'; 
$password = 'apmsetup'; 

try {
    $db = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8", $username, $password);
    $db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION); 
} catch (PDOException $e) {
    echo "데이터베이스 연결에 실패했습니다: " . $e->getMessage();
    exit;
}

$inputUsername = $_GET['username'];
$inputPassword = $_GET['password'];

$query = "SELECT * FROM users WHERE username = :username AND password = :password";
$stmt = $db->prepare($query);
$stmt->bindValue(':username', $inputUsername);
$stmt->bindValue(':password', $inputPassword);

try {
    $stmt->execute();
} catch (PDOException $e) {
    echo "쿼리 실행 중 오류가 발생했습니다: " . $e->getMessage();
    exit;
}

if ($stmt->rowCount() > 0) {
    header("Location: dashboard.php");
    exit;
} else {
    echo "아이디 또는 비밀번호가 일치하지 않습니다.";
    exit;
}
?>
-> db와 연결하여 로그인 정보 확인
3.dashboard.php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard</title>
</head>
<body>
    <h2>Welcome! but this is site has NOT data  :( just Enjoy!</h2>
    <p>Lee su baek's login project!</p>
</body>
</html>
-> 로그인 완료 후 의미 없는 페이<?php


![스크린샷(55)](https://github.com/leesubaek/-/assets/155121986/30945057-67d9-499b-b1cb-3044f6aa2e86)
![스크린샷(56)](https://github.com/leesubaek/-/assets/155121986/ad2f1a73-a549-4406-a396-55365f9d7658)

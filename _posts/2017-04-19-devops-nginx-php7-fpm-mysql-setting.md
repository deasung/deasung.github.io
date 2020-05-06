---
title: nginx , php7 fpm설정된 서버에서 mysql 연동안될때
published: true
---


본인의 aws 서버환경은 nginx + php7 fpm 방식으로 간단한 테스팅할려고 셋팅하였습니다

자바로 rds연동하다가 삘받아서 php연동해서 테스트할려고했는데 안되서

우선 ec2 ubuntu서버에 pdo 설치되어있는지 확인후에 안되어잇어서 sudo apt-get install php7.0-mysql 설치후에

## PDO(PHP Data Object)는

> - 5.1.0 이상의 PHP에서 표준으로 사용하는 데이터베이스 접속방법입니다. PHP에서는 MySQL뿐만 아니라 다른 여러 데이터베이스에도 접속할 수 있습니다. MySQL 이외의 데이터베이스에 접속할 때, mysql_connect()와 mysql_select_db() 등의 함수를 이용하려면 사용하는 데이터베이스에 맞게 프로그램을 달리 작성해야 합니다. 그러나 PDO를 이용하면 같은 명령으로 여러 종류의 데이터베이스를 조작할 수 있습니다.

```
try {

    $dbh = new PDO('호스트주소;dbname=데이터베이스명', $mysql_username, $mysql_password);

    foreach ( $dbh->query('SELECT * from JOBHISTORY') as $row ) {

        print_r ( $row );

    }

    $dbh = null;

} catch ( PDOException $e ) {

    print "Error!: " . $e->getMessage() . "
";

    die();

}
```

결론은 우선은 해결했습니다만...먼가찜찜하네요
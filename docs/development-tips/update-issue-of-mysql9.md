# MySQL 9로 업데이트할 때 로그인 이슈

맥을 개발머신으로 사용하는 개발자라면 Homebrew로 개발에 필요한 프로그램을 설치하고 버전관리를 하게 됩니다. 그런데, 최근에 `brew upgrade`로 설치된 프로그램을 업그레이드할 때 mysql이 8.x에서 9.x로 바뀌었는데요, mysql을 5버전부터 이용한 프로그램의 경우 유저 패스워드 인증 방법을 `mysql_native_password`로 사용하는 경우 에러가 발생하게 됩니다.

MySQL 9.x에서는 더이상 `mysql_native_password`을 지원하지 않으며, 따라서 `caching_sha2_password`으로 바꾸어 줘야 합니다.

## `mysql_native_password`에서 `caching_sha2_password` 으로 바꾸는 법

1. 테이블 Grant를 비활성화 합니다

    MySQL 설정 파일에 아래를 추가합니다. 보통 `/usr/local/etc/my.cnf`에 있어요.

    ```ini
    [mysqld]
    skip-grant-tables
    ```

2. MySQL을 재시작합니다:

    ```shell
    brew services restart mysql
    ```

3. MySQL에 root 유저로 접속합니다:

    ```shell
    mysql -uroot
    ```

4. 유저 인증 방법을 업데이트합니다:

    ```shell
    Refresh the privileges:

    FLUSH PRIVILEGES;
    ```

5. `mysql_native_password` 플러그인을 사용하는 유저 리스트를 얻는다:

    ```shell
    SELECT User, Host, plugin FROM mysql.user WHERE plugin = 'mysql_native_password';
    ```

6. `caching_sha2_password` 플러그인으로 5번에서 나온 계정을 모두 업데이트 한다:

    ```shell
    ALTER USER '{user}'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'new_password';
    ```

7. 테이블 Grant를 다시 활성화한다:

    업데이트 후에 1번에서 추가한 `skip-grant-tables`를 삭제합니다.

8. 수정한 내용을 반영하기 위해서 MySQL을 재시작합니다:

    ```shell
    brew services restart mysql
    ```

이 순서를 따라하면 MySQL 9로 업그레이드 할 때의 인증 방법에 대한 이슈를 해결할 수 있습니다.

# [UBUNTU-POSTGRESQL](https://help.ubuntu.com/community/PostgreSQL)

## 머릿말[](Introduction)
PostgreSQL은 강력한 객체 관계 데이터베이스 관리 시스템으로, 유연한 BSD 스타일 라이선스 하에 제공된다. PostgreSQL는 많은 진보된 기능을 포함하며, 매우 빠르고 표준을 준수한다.
[](PostgreSQL is a powerful object-relational database management system, provided under a flexible BSD-style license.[1] PostgreSQL contains many advanced features, is very fast and standards compliant.)

PostgreSQL는 C, C++, 파이썬, 자바, PHP, Ruby 등 많은 프로그래밍 언어들과 연결되어, 간단한 웹 어플리케이션에서부터 수백만 레코드를 가진 대용량 데이터베이스까지 어떤 것이든 강화하는데 사용될 수 있다.
[](PostgreSQL has bindings for many programming languages such as C, C+/+, Python, Java, PHP, Ruby... It can be used to power anything from simple web applications to massive databases with millions of records.)

## 클라이언트만 설치할 경우 [](Client Installation)
외부에 이미 존재하는 PostgreSQL 서버에 접속만하려고 하면, PostgreSQL 메인 패키지를 설치하지 말고, PostgreSQL 클라이언트 패키지를 설치한다. 아래의 명령을 사용한다.
[](If you only wish to connect to an external PostgreSQL server, do not install the main PostgreSQL package, but install the PostgreSQL client package instead. To do this, use the following command)

```bash
 sudo apt-get install postgresql-client
```
그리고 나서 다음의 명령으로 외부서버에 연결한다.
[](you then connect to the server with the following command)

```bash
 psql -h server.domain.org database user
```
비밀번호를 입력한 후에 명령줄로 PostgreSQL에 접속한다. 예를 들어, 아래처럼 입력할 수 있다.
[](After you inserted the password you access PostgreSQL with line commands. You may for instance insert the following)

```bash
 SELECT * FROM table WHERE 1;
```

연결 종료는 아래의 명령으로 한다.[](You exit the connection with)

```bash
 \q
```

## 메인 패키지 설치하기 [](Installation)
로컬에 서버를 설치하려면 아래의 명령을 사용한다.
[](To install the server locally use the command line and type:)

```bash
 sudo apt-get install postgresql postgresql-contrib
```

그러면 여러분의 우분투 릴리즈에서 이용가능한 최신 버전 릴리즈 및 그와 함께 널리 이용되는 애드온들을 설치할 것이다.
[](This will install the latest version available in your Ubuntu release and the commonly used add-ons for it.)
보다 최신 릴리즈를 얻는 방법은 최하단의 [외부 링크들](#외부-링크들) 항목을 보라.
[](See "External Links" below for options for getting newer releases.)

### PostGIS, 프로시저 언어, 클라이언트 인터페이스 등을 설치하기 [](Installing PostGIS, procedural languages, client interfaces, etc)
추가적인 패키지들은 프로시저 언어 런타임, PostGIS 같은 애드온,  파이썬을 위한 psycopg2 같은 언어 클라이언트 인터페이스 등을 포함한다. 이들의 목록은 다음의 명령으로 얻을 수 있다.
[](Additional packages contain procedural language runtimes, add-ons like PostGIS, language client interfaces like psycopg2 for Python, etc. You can get a listing with:)

```bash
 apt-cache search postgres
```
 
### 관리 [](Administration)
`pgAdmin III`는 PostgreSQL를 위한 쉬운 GUI이며, 초심자에게 딱이다. 설치하려면 아래의 명령을 사용한다.
[](pgAdmin III is a handy GUI for PostgreSQL, it is essential to beginners. To install it, type at the command line:)

```bash
 sudo apt-get install pgadmin3
```

System>Administration 메뉴에서 `Synaptic package manager`를 사용해서 이 패키지를 설치할 수도 있다.
[](You may also use the Synaptic package manager from the System>Administration menu to install these packages.)

## 기본적인 서버 설정 [](Basic Server Setup)
시작하려면, "postgres"라는 PostgreSQL 사용자(role)의 암호를 설정해야 한다. 우리는 외부에서 다른 방법으로 서버에 접속할 수 없을 것이다. 로컬 "postgres" 리눅스 사용자로써, psql 명령을 사용하여 서버에 연결하고 조작하는 것이 허용된다.
[](To start off, we need to set the password of the PostgreSQL user {role} called "postgres"; we will not be able to access the server externally otherwise. As the local “postgres” Linux user, we are allowed to connect and manipulate the server using the psql command.)

터미널에서 다음 명령을 친다. [](In a terminal, type:)

```bash
sudo -u postgres psql postgres
```

이 명령은 로컬 사용자인 "postgres"와 같은 이름의 role로, "postgres"라는 데이터베이스(psql 명령의 첫번째 인자)에 연결한다. "postgres" 데이터베이스 role에 대한 암호 설정은 다음 명령을 사용한다.
[](this connects as a role with same name as the local user, i.e. "postgres", to the database called "postgres" {1st argument to psql}. Set a password for the "postgres" database role using the command:)

```bash
\password postgres
```

그리고 나서 커서가 깜박일 때 암호를 입력한다. 암호 텍스트는 보안을 위해 콘솔창에 표시되지 않는다. `컨트롤` + `D`를 치거나 `\q`를 치면 posgreSQL 입력창을 종료한다.
[](and give your password when prompted. The password text will be hidden from the console for security purposes. Type Control+D or \q to exit the posgreSQL prompt.)

### 데이터베이스 만들기 [](Create database)
첫번째 데이터베이스를 간단히 "mydb"라고 만들려면, 아래의 명령을 친다.
[](To create the first database, which we will call "mydb", simply type:)

```bash
 sudo -u postgres createdb mydb
```

### Postgresql 8.4 또는 9.3 이상을 위한 (PgAdmin의) 서버 Instrumentation 설치 [](Install Server Instrumentation {for PgAdmin} for Postgresql 8.4 or 9.3) 
PgAdmin은 완전하게 기능하려면 애드온 설치가 필요하다. "adminpack" 애드온은, 서버 Instrumentation이라고 부르는데, postgresql-contrib 패키지의 일부이므로, 이 패키지를 반드시 설치해주어야 한다.
[](PgAdmin requires the installation of an add-on for full functionality. The "adminpack" addon, which it calls Server Instrumentation, is part of postgresql-contrib, so you must install that package if you haven't already:)

```bash
 sudo apt-get install postgresql-contrib
```

그리고나서 "Postgresql 8.4"에 대한 확장을 활성화하기 위해, adminpack.sql 스크립트를 실행하는데, 아래 명령을 사용한다.
[](Then to activate the extension, for ""Postgresql 8.4"", run the adminpack.sql script, simply type:)

```bash
 sudo -u postgres psql < /usr/share/postgresql/8.4/contrib/adminpack.sql
```

"Postgresql 9.3" 이상에서 "postgres" 데이터베이스 안에 adminpack "확장"을 설치하려면 다음 명령을 사용한다.
[](For "Postgresql 9.3"+ install the adminpack "extension" in the "postgres" database:)

```bash
 sudo -u postgres psql
 CREATE EXTENSION adminpack;
```

## 다른 서버 설정 방법(쉬운 방법)
같은 컴퓨터에서 데이터베이스에 연결하려고 한다면, 설정이 더 쉬워진다.
[](If you don't intend to connect to the database from other machines, this alternative setup may be simpler.)
우분투에서는 기본적으로, 같은 컴퓨터 내부에서 이루어지는 연결에는 'ident sameuser' 인증을 사용하게 설정되어 있다. 자세한 정보는 Postgresql 문서를 보라. 핵심만 간추리면, 우분투 사용자 이름이 'foo'인데 이 'foo'를 Postgresql 사용자로 추가하면, 그 데이터베이스에 연결할 때 암호가 필요 없다는 뜻이다.
[](By default in Ubuntu, Postgresql is configured to use 'ident sameuser' authentication for any connections from the same machine. Check out the excellent Postgresql documentation for more information, but essentially this means that if your Ubuntu username is 'foo' and you add 'foo' as a Postgresql user then you can connect to the database without requiring a password.)
갓 설치된 데이터베이스에 연결할 수 있는 유일한 사용자가 "postgres" 사용자 뿐이기 때문에, 여러분의 로그인 이름과 동일한 이름으로 여러분 스스로 데이터베이스 계정(데이터베이스 수퍼유저)을 만들고 그 사용자에 대한 암호를 만드는 방법을 제시한다.
[](Since the only user who can connect to a fresh install is the postgres user, here is how to create yourself a database account {which is in this case also a database superuser} with the same name as your login name and then create a password for the user:)

```bash
 sudo -u postgres createuser --superuser $USER
 sudo -u postgres psql
```

```bash
 postgres=# \password $USER
```
($USER를 인식하지 못하면 여러분의 로그인 이름을 그 위치에 직접 적는 것도 방법이다.)
클라이언트 프로그램은 기본적으로, 여러분의 로그인 이름을 사용해서 로컬 호스트에 연결해서 로그인 이름으로 데이터베이스를 찾으려고 한다. 그러므로 일을 쉽게 하려면, 위에서 부여받은 여러분의 새로운 수퍼유저 권한을 사용해서 로그인 이름과 같은 이름으로 데이터베이스를 만들어라.
[](Client programs, by default, connect to the local host using your Ubuntu login name and expect to find a database with that name too. So to make things REALLY easy, use your new superuser privileges granted above to create a database with the same name as your login name:)

```bash
 sudo -u postgres createdb $USER
```

이제 여러분 소유의 데이터베이스에 연결해서 SQL을 날려보는 것이 아래처럼 편해진다.
[](Connecting to your own database to try out some SQL should now be as easy as:)

```bash
 psql
```

데이터베이스를 만드는 것도 예제처럼 쉽다. 아래의 명령을 실행하고 나서
[](Creating additional database is just as easy, so for example, after running this:)

```bash
 create database amarokdb;
```

여러분은 곧바로 사용자 Amarok에게 가서 postgresql을 사용해서 그 음악 카탈로그를 저장하라고 말할 수 있다. 데이터베이스 이름은 amarokdb가 되었을 것이고, 그 사용자 이름은 여러분 소유의 로그인 이름이 되었을 것이며, 'ident sameuser' 덕분에 암호조차 필요가 없어서 암호를 비워둘 수 있다.
[](You can go right ahead and tell Amarok to use postgresql to store its music catalog. The database name would be amarokdb, the username would be your own login name, and you don't even need a password thanks to 'ident sameuser' so you can leave that blank.)

## pgAdmin III GUI 사용하기 <!--Using pgAdmin III GUI-->
PostgreSQL가 무엇을 할 수 있는지 알기 위해, 그래픽 기반 클라이언트로 시작해 볼 수 있다. 터미널 창에서 다음을 입력한다.
<!--To get an idea of what PostgreSQL can do, you may start by firing up a graphical client. In a terminal type :-->

```bash
 pgadmin3
```

pgAdmin III 인터페이스가 보여질 것이다. 좌측 상단의 "Add a connection to a server" 버튼을 클릭하자. 새 대화창에서, 주소 127.0.0.1(로컬 호스트가 기본값이므로 그냥 비워둘 수도 있다.), 서버 설명, 기본 데이터베이스(위의 예제에서 "mydb"), 여러분의 사용자 이름("postgres")과 암호를 입력하자. pgAdmin III가 서버에 접속하려면 한 단계가 더 필요한데, 그것은 `pg_hba.conf` 파일을 고쳐서 인증 방식을 peer에서 md5(암호설정을 하지 않았다면 작동하지 않을 것이다)로 변경하는 것이다.
<!--You will be presented with the pgAdmin III interface. Click on the "Add a connection to a server" button (top left). In the new dialog, enter the address 127.0.0.1 (Local host is default, so it can be left out.), a description of the server, the default database ("mydb" in the example above), your username ("postgres") and your password. One more step is required in order to allow pgAdmin III to connect to the server, and that is to edit pg_hba.conf file and change the authentication method from peer to md5 (will not work if you have not set the password):-->

```bash
sudo nano /etc/postgresql/9.3/main/pg_hba.conf
```

위 방식으로 파일로 들어가서 아래의 줄을 찾아서 그 아래의 줄로 바꾸자.
<!--and change the line-->

```bash
# Database administrative login by Unix domain socket
local   all             postgres                                peer
```

```bash
# Database administrative login by Unix domain socket
local   all             postgres                                md5
```

이제 서버 설정 변경을 재로딩하고 pgAdmin III를 PostgreSQL 데이터베이스 서버에 연결하자.
<!--Now you should reload the server configuration changes and connect pgAdmin III to your PostgreSQL database server.-->

```bash
sudo /etc/init.d/postgresql reload
```

이 GUI로 데이터베이스를 만들고 관리하고, 쿼리하고, SQL을 실행할 수 있다.
<!--With this GUI you may start creating and managing databases, query the database, execute SQl etc.-->

## 서버 관리하기
[PostgreSQL 공식 문서](http://www.postgresql.org/docs/current/static/admin.html)를 보라.
<!--To learn more about managing PostgreSQL (but without the Ubuntu specifics) see the official PostgreSQL documentation-->

### 사용자와 권한 관리하기
사용자 관리는 [PostgreSQL 문서의 클라이언트 인증 챕터](http://www.postgresql.org/docs/current/static/client-authentication.html)에서 자세하게 논의한다. 다음은 시작을 위한 도입부이다. 사용자를 관리하려면, 먼저 `/etc/postgresql/current/main/pg_hba.conf` 를 열고 잠겨서 보안되고 있는 기본 설정을 수정해야 한다. 예를 들어, 만약 여러분이 postgres가 그 소유의 사용자들(시스템 사용자와 링크되어 있지 않다)을 관리하게 하고 싶다면, 아래의 내용을 추가할 것이다.
<!--User management is discussed in detail in the client authentication chapter of the PostgreSQL documentation; the following is an introduction to get you started.
To manage users, you first have to edit /etc/postgresql/current/main/pg_hba.conf and modify the default configuration which is very locked down and secure. For example, if you want postgres to manage its own users (not linked with system users), you will add the following line:-->

```bash
8<-------------------------------------------
# TYPE  DATABASE    USER        IP-ADDRESS        IP-MASK           METHOD
host    all         all         10.0.0.0       255.255.255.0    md5
8<-------------------------------------------
```

위 내용은 여러분의 로컬 네트워크(10.0.0.0/24 - 여러분 소유의 로컬 네트워크를 교체한다!)에서, postgres 사용자가 그 네트워크를 통해서 고전적인 사용자/암호 쌍을 제공하는 데이터베이스에 연결할 수 있음을 의미한다.
<!--
Which means that on your local network (10.0.0.0/24 - replace with your own local network !), postgres users can connect through the network to the database providing a classical couple user / password.
-->

사용자가 네트워크를 통해 서버의 데이터베이스에 연결하게 허용하는 이외에, PostgreSQL이 다른 네트워크들로부터 들어오는 패킷을 감지(Listen)할 수 있게 해주어야 한다. 그럴려면, /etc/postgresql/current/main/postgresql.conf를 에디터로 열고 listen_addresses를 아래와 같이 변경한다.
<!--
Besides allowing a user to connect over the network to the to a database on the server, you must enable PostgreSQL to listen across different networks. To do that, open up /etc/postgresql/current/main/postgresql.conf in your favourite editor and alter the listen_addresses as below:
-->

```bash
listen_addresses = '*'
```

위 표현은 모든 네트워크 인터페이스로들부터 패킷을 감지하기 위한 것이다. listen_addresses에 대한 다른 옵션은 문서를 참조하라. 
데이터베이스에 대한 완전한 권한을 갖는 사용자로 데이터베이스를 만들려면, 아래의 명령을 사용한다.
<!--
to listen on all network interfaces. See the docs for listen_addresses for other options.
To create a database with a user that have full rights on the database, use the following command:
-->

```bash
sudo -u postgres createuser -D -A -P myuser
sudo -u postgres createdb -O myuser mydb
```

첫번째 명령줄은 데이터베이스 생성 권한이 없고(-D) 사용자 권한 추가 권한(-A)도 없는 사용자를 만드는데 암호를 입력받는 커서(-P)가 열릴 것이다. 두번째 명령줄은 myuser가 소유자인 mydb 데이터베이스를 만든다.
이 간단한 예제가 대부분의 경우에 부합할 것이다. 더 자세한 내용은, 관련된 man페이지를 참조하거나 온라인 문서를 참조하기 바란다.
<!--
The first command line creates the user with no database creation rights (-D) with no add user rights -A) and will prompt you for entering a password (-P). The second command line create the database 'mydb with 'myuser' as owner.
This little example will probably suit most of your needs. For more details, please refer to the corresponding man pages or the online documentation.
-->

### 서버 재시작하기
네트워킹 설정 후에는 서버를 다시 가동할 필요가 있는데, 아래의 명령을 추천한다.
<!--
After configuring the networking / users you may need to reload the server, here is a suggested command to do so.
-->

```bash
sudo /etc/init.d/postgresql reload
```

postgresql.conf의 어떤 설정 변경은 완전한 재시작이 필요한데, 그러면 활성 연결은 종료되고 커밋되지 않은 트랜잭션은 취소되게 된다.
<!--
Some settings changes in postgresql.conf require a full restart, which will terminate active connections and abort uncommitted transactions:
-->

```bash
sudo /etc/init.d/postgresql restart
```

## 더 읽을 거리
여러분이 SQL에 친숙하지 않다면 이 강력한 언어를 연구하고 싶을 것이다. 비록 PostgreSQL을 간단하게 사용하는데는 이 언어가 필요하지 않더라도 말이다.(간단한 장고 프로젝트의 경우가 그렇다.)
PostgreSQL 웹사이트는 이 데이터베이스를 사용하는데 관한 풍부한 정보를 갖고 있다. 특히나 튜토리얼은 시작에 유용하다. 이미 우분투 패키지를 통해 PostgreSQL를 설치했다면 튜토리얼에서 설치 단계를 생략할 수 있다.
<!--
If you are not familiar with SQL you may want to look into this powerful language, although some simple uses of PostgreSQL may not require this knowledge (such as a simple Django project).
The PostgreSQL website contains a wealth of information on using this database. In particular, the tutorial is a useful starting point, but you can skip the installation step as you've already installed it using Ubuntu packages.
-->

## 장애 대응하기
### fe_sendauth: no password supplied
여러분의 pg_hba.conf가 md5 인증이 원본 호스트, 연결 방법, 요청된 사용자 이름/데이터베이스에 기반한 연결에 사용되게 명시하고 있지만, 여러분의 어플리케이션이 암호를 제공하지 않았다.
인증 모드를 변경하거나 연결하려는 사용자의 암호를 설정하고 여러분의 어플리케이션 연결 설정에 그 암호를 명시한다.
<!--
Your pg_hba.conf specifies that md5 authentication is to be used for this connection based on the origin host, connection method and the requested username/database, but your application didn't supply a password.
Change the authentication mode or set a password for the user you're connecting to and then specify that password in your application's connection settings.
-->

### FATAL: role "myusername" does not exist
기본적으로 PostgreSQL는 현재 유닉스 사용자와 같은 이름으로 PostgreSQL 사용자를 연결한다. 여러분은 데이터베이스에 그 이름으로 PostgreSQL 사용자를 생성하지 않은 것이다.
적절한 사용자를 생성하거나, 연결가능한 다른 사용자 이름을 명시한다. 명령줄 도구에서 -U 플래그가 이것을 한다.
<!--
By default PostgreSQL connects to the PostgreSQL user with the same name as the current unix user. You have not created a PostgreSQL user by that name in your database.
Create a suitable user, or specify a different username to connect with. In the command line tools the -U flag does this.
-->

### FATAL: database "myusername" does not exist
그 사용자 이름은 존재하는데, 그 이름으로 된 데이터베이스가 없다.
기본적으로 PostgreSQL는 연결하려는 사용자와 동일한 이름으로 된 데이터베이스에 연결한다. 하지만 그 데이터베이스가 존재하지 않는다고 그 데이터베이스를 자동으로 생성하지는 않는다.
그 데이터베이스를 생성하던가, 아니면 연결하려는 다른 데이터베이스를 명시한다.
<!--
A user named "myusername" exists, but there's no database of the same name.
By default PostgreSQL connects to the database with the same name as the user you're connecting as, but it doesn't auto-create the database if it doesn't exist.
Create the database, or specify a different database to connect to.
-->

### FATAL: Peer authentication failed for user "myusername"
여러분이 유닉스 소켓으로 로컬호스트에 연결하려고 하는 상황이다. 사용자 "myusername"이 이미 존재하지만 유닉스 사용자 중에는 그와 같은 이름의 사용자가 없다. PostgreSQL는 사용자/데이터베이스 콤보를 위하여 유닉스 소켓에 peer 인증을 사용하게 설정되는데 그러면 유닉스 사용자 이름과 PostgreSQL 사용자 이름이 일치할 것이 요구된다.

원하는 PostgreSQL 사용자와 일치하는 유닉스 사용자로부터 연결--아마도 sudo -u 그사용자이름 psql--하거나 pg_hba.conf를 바꿔서 이 사용자 이름을 위하여 "md5" 같은 다른 인증 모드를 사용한다.
<!--
You are connecting to localhost via a unix socket. A user named "myusername" exists, but your current unix user is not the same as that username. PostgreSQL is set to use "peer" authentication on unix sockets for this user/db combo so it requires your unix and postgresql usernames to match.
Connect from the unix user that matches the desired PostgreSQL user - perhaps with sudo -u theusername psql - or change pg_hba.conf to use a different authentication mode like "md5" for this username.
-->

### could not connect to server: No such file or directory
이런 에러는 (유닉스 소켓 경로가 다를 수 있는데, 여러분이 어떻게 설치하느냐에 좌우된다.)
<!--
An error like this (possibly with a different unix socket path, depending on your install):
-->

```bash
 psql: could not connect to server: No such file or directory
 Is the server running locally and accepting
 connections on Unix domain socket "/tmp/.s.PGSQL.5432"?
```

아래의 몇 가지 것들에 해당할 수 있다.
* 서버가 동작하지 않고 있다.
* 서버가 여러분의 클라이언트 libpq에서 기본적으로 다른 유닉스 소켓 디렉터리를 가지는데, 기본값이 다르게 컴파일되었기 때문이거나 아니면 설정이 일치하지 않기 때문이다.
* 서버가 다른 포트를 감지하고 있다. PostgreSQL은 5432같은 포트 넘버를 소켓 파일에 대한 접미사로 사용하여 유닉스 소켓에 TCP/IP 포트를 에뮬레이트한다.

이들을 차례대로 제거한다.

먼저 서버가 동작 중인지 확인한다. 우분투에서는, `ps -u postgres -f`가 사용자 postgres로 동작하는 프로세스들을 보여준다 - postgres로 이름붙은 것들 여러가지를 보고 싶을 것이다.

이제 서버가 클라이언트가 예상하는 것을 감지하는지 확인한다. PostgreSQL 서버의 소켓 디렉터리를 확인하려면 다음의 명령을 사용한다.

<!--
can mean a number of things:

* The server isn't running;

* The server has a different unix_socket_directories to the default in your client's libpq, either due to different compiled-in defaults or a mismatched setting;

* The server is listening on a different "port". PostgreSQL emulates TCP/IP ports on unix sockets by using the port number as the suffix for the socket file, e.g. 5432.

Eliminate these in turn.

First make sure the server is running. On Ubuntu, ps -u postgres -f will show you any processes running as user postgres - you want to see multiple ones named postgres.

Now make sure the server is listening where your client thinks it is. To find out your PostgreSQL server's socket directory:
-->

```bash
 sudo -u postgres psql -c "SHOW unix_socket_directories;"
```

또는 옛날 PostgreSQL에서는, unix_socket_directory은 인자처럼 이름이 변경되었다. 서버의 포트를 보려면(포트는 TCP/IP와 유닉스 소켓 양쪽에 적용된다)
<!--
or on older PostgreSQL versions, unix_socket_directory as the parameter changed name. To show the server's port (which applies for both TCP/IP and unix sockets):
-->

```bash
 sudo -u postgres psql -c "SHOW port;"
```

유닉스 사용자 postgres로도 psql에 연결할 수 없다면 lsof로 소켓 디렉터리를 체크할 수 있다.
<!--
If you can't even connect with psql under unix user postgres you can check the socket dir with lsof:
-->

```bash
 $ sudo lsof -U -a -c postgres
 COMMAND   PID     USER   FD   TYPE             DEVICE SIZE/OFF   NODE NAME
 postgres 6565 postgres    5u  unix 0xffff88005a049f80      0t0 183009 /tmp/.s.PGSQL.5432
 postgres 6566 postgres    1u  unix 0xffff88013bc22d80      0t0 183695 socket
 postgres 6566 postgres    2u  unix 0xffff88013bc22d80      0t0 183695 socket
```

이 경우에 첫번째 줄은 소켓 위치이다. 이 서버는 포트 5432와 소켓 디렉터리 /tmp를 가지고 있다.

만약 여러분의 클라이언트가 다른 소켓 디렉터리를 찾고 있다면, 여러분은 아마도 기본 소켓 경로와(또는) 기본 포트 그리고 여러분의 클라이언트 어플리케이션이 링크된 libq가 여러분이 운영중인 PostgreSQL와 다르게 컴파일된 유닉스 소켓 경로와(또는) 포트를 가지고 있는 상태에서 연결하려고 시도하고 있을 것이다. 대부분 여러분의 LD_LIBRARY_PATH나 /etc/ld.so.conf가 여러분의 PostgreSQL 버전과 함께 제공되는 것 이전에 다른 libq를 가지고 있기가 쉽다. 이는 일반적인 일은 아닌데, 여러분은 그냥 소켓 디렉터리를 덮어쓸 수 있다.

대체 소켓 디렉터리와/또는 연결을 위한 포트를 명시하려면, 여러분의 연결 옶션에 호스트 파라미터로 소켓 dir을 명시한다. 예를 들어, 사용자 bob으로 /tmp에서 포트 5433을 감지하는 서버에 연결하려면 아래의 명령을 사용한다.
<!--
In this case the first line is the socket location. This server has socket directory /tmp with port 5432.
If your client is looking in a different socket directory, you're probably trying to connect over unix sockets to the default socket path and/or to the default port, and the libpq your client application is linked to has a different compiled-in unix socket path and/or port than your running PostgreSQL. Most likely your LD_LIBRARY_PATH or /etc/ld.so.conf has a different libpq before the one that came with your version of PostgreSQL. This doesn't generally matter much, you can just override the socket directory.
To specify an alternative socket directory and/port port to connect to, specify the socket dir as the host parameter in your connection options, e.g. to connect as user bob to the server listening in /tmp on port 5433:
-->

```bash
 psql -h /tmp -p 5433 -U bob ...
```

또는 연결-문자열 형식은 아래와 같다.
<!--
or in connection-string form:
-->

```bash
 psql "host=/tmp port=5433 user=bob ..."
```

libq를 사용하는 어떤 클라이언트(모든 PostgreSQL 클라이언트 툴들, 예를 들면, psycopg2, 루비/레일즈의 Pg gem, PHP의 postgres와 PDO, 펄의 DBB::Pg 등등)에도 똑같이 적용된다. libq 클라이언트가 아닌 것들, PgJDBC, py-postgresql 등은 적용되지 않지만, 이들 대부분은 유닉스 소켓을 전혀 지원하지 않는다. non-libq 기반 클라이언ㅌ들에 대한 것은 클라이언트 문서를 보라.
<!--
The same works with any client that uses libpq (all the PostgreSQL client tools, plus e.g. psycopg2, the Pg gem in Ruby/Rails, PHP's postgres and PDO, Perl's DBB::Pg, etc). It does NOT work with non-libpq clients like PgJDBC, py-postgresql, etc, but most of these don't support unix sockets at all. See the client documentation for non-libpq based clients.
-->

[1] PostgreSQL을 어플리케이션에 사용하는데 돈을 내지 않아도 된다. 상업적인 비공개 소스 소프트웨어라도 마찬가지다. http://www.postgresql.org/about/licence/ 를 보라.
<!--
[1] You do not have to pay in order to use PostgreSQL for any application, such as commercial closed source software. See http://www.postgresql.org/about/licence/.
-->

## 외부 링크들
### 공식 PostgreSQL 다운로드
PostgreSQL 프로젝트는 [다운로드 페이지](http://www.postgresql.org/download/)에서 공식적으로 다운로드 가능한 링크 목록을 제공하는데, 우분투 소프트웨어 리파지터리도 여기에 포함된다. 특히, 우분투 사용자는 apt.postgresql.org을 통하여 apt-get을 사용함으로 PostgreSQL 우분투 릴리즈에 패키징된 것들 보다 더 최신 버전을 받을 수 있다.

PostgreSQL에 관한 지원과 서비스는 [서비스와 지원 페이지](http://www.postgresql.org/support/professional_support/)를 보라.
<!--
The PostgreSQL project provides an official list of download locations, including an Ubuntu software repository, at its download page. In particular, Ubuntu users can get newer PostgreSQL versions than those packaged in their Ubuntu release using apt-get via apt.postgresql.org.
For support and services around PostgreSQL see the services and support page.
-->

### EnterpriseDB

The PostgreSQL Linux downloads page contains a section on "Graphical installer" built by EnterpriseDB. You download the installer, change its properties to allow to run it as command (it has .run extension), and run it from command prompt as in "sudo whateveritwas.run".

You end up with 

configured DB server instance, which starts with your server
pgAdmin III UI client application
Note that the installed software will not be integrated with Ubuntu software center. As a result, you will not receive any security updates from Ubuntu. However, the installed version will closely match the latest Ubuntu version.

### Turnkey Linux

An Ubuntu-based PostgreSQL appliance is one of the easiest ways to get up and running with PostgreSQL on Ubuntu. It's part of a family of pre-integrated TurnKey Linux Software Appliances based on Ubuntu 10.04.1 (Lucid LTS). 

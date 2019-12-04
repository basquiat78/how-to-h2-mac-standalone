# how-to-h2-mac-standalone
어떤 목적에 의해 가볍게 테스트하기 위해서 h2를 스프링 부트위의 런타임이 아닌 스탠드얼론 형식으로 설치해서 사용할려고 했었다.

하지만 한시간동안 다음과 같은 에러에 고통을 받았고 결국에는 터미널을 통해서 데이터베이스를 생성해서 로그인하면서 해결했는데 지금까지 설치해서 사용해 본 경험이 없던 나에게는 정말 짜증나는 일이 아닐 수 없다....


그래서 짧막하게 남겨보고자 한다.

# Prerequisites

OS: MacOs
H2: Version 1.4.200 (2019-10-14)


## Install Using Brew Or Download

http://h2database.com/html/main.html

두 가지 방법을 통해서 설치해서 처음에는 실행하고 접속했더니 다음과 같은 에러가 발생했다.

이게 최신 버전은 그렇고 이전 버전의 경우에는 상황이 좀 다르긴 한데 위에 언급한 버전을 기준으로 이야기하고자 한다.

보통 스프링 부트에 얹어서 사용하게 되면 그냥 연결하면 그냥 한방에 연결이 되는데 설치의 경우에는 다음과 같은 에러를 보게 된다.

```
Database "/Users/basquiat/test" not found, either pre-create it or allow remote database creation (not recommended in secure environments) [90149-200] 90149/90149 (도움말)
```

아마도 이전 버전의 경우라면 

```
Database "~/test" not found, and IFEXISTS=true, so we cant auto-create it [90146-199]
```

원래 이녀석은 자동으로 생성해 주는걸로 알고 있는데 보안 때문인지 위의 에러로 바꼈다.

한시간을 같은 짓거리를 반복하다가 결국 찾아낸게 있는데 터미널을 통해서 데이터베이스를 생성하는 것이다.

이해 할 수 없는 것은 그냥 테스트용으로 사용하는 것인데 무슨 보안이야기를 꺼내고 있나 이런 생각이 들지만 어찌되었든 이 녀석도 DB라는 녀석이라는 건가....

결국 웹 콘솔에서는 생성할 수 없다는 결론을 Stackoverflow에서 확인했다.

## 그렇다면 너는 어떻게 해겷했니??

그냥 다음과 같이 터미널에서 생성해 버렸다.

```
basquiatyoonui-MacBookPro: basquiat$ java -cp h2-*.jar org.h2.tools.Shell

Welcome to H2 Shell 1.4.200 (2019-10-14)
Exit with Ctrl+C
[Enter]   jdbc:h2:~/test
URL       
[Enter]   org.h2.Driver
Driver    
[Enter]   sa
User      
Password  
Type the same password again to confirm database creation.
Password  
Passwords don't match. Try again.
Password  
Type the same password again to confirm database creation.
Password  
Connected
Commands are case insensitive; SQL statements end with ';'
help or ?      Display this help
list           Toggle result list / stack trace mode
maxwidth       Set maximum column width (default is 100)
autocommit     Enable or disable autocommit
history        Show the last 20 statements
quit or exit   Close the connection and exit

sql> exit
Connection closed

```

h2를 압축해제해서 생성된 폴더의 bin폴더로 들어가서 

```
java -cp h2-*.jar org.h2.tools.Shell
```

다음과 같은 명령어를 쳤더니...

```
Welcome to H2 Shell 1.4.200 (2019-10-14)
Exit with Ctrl+C
[Enter]   jdbc:h2:~/test
URL       
[Enter]   org.h2.Driver
Driver    
[Enter]   sa
User      
Password  
Type the same password again to confirm database creation.
Password  
Passwords don't match. Try again.
Password  
Type the same password again to confirm database creation.
Password  
Connected

```

이렇게 나온다.

첫 번째 Enter에서 일반적으로 사용하는 jdbc:h2:~/test 를 입력하면 Driver를 입력하는 란이 저절로 튀어 나온다.

그냥 순서대로 엔터를 누르고 아이디/비번을 설정하면 끝이다.

보통 sa에 암호는 공란으로 해서 엔터 엔터를 막 누르면 데이터베이스가 생성되고 로그인을 할 수 있게 된다.

# At A Glance

뭐 설치해서 사용해 본적이 있었어야지...

하긴 처음 IT에 발을 들이고 들어간 BPM회사에서는 HSQLDB도 비슷한 방식으로 쓰긴 했는데...암튼 담에는 이딴 걸로 고생하지 말자....





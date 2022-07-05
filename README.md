# city-weather-App
검색한 도시의 날씨를 알아보는 앱<br>
## 기능 상세
도시 이름을 입력하면 현재 날씨 정보를 가져와 화면에 표시되게 합니다<br>
도시 이름을 잘못 입력하면 alert 메세지가 뜹니다<br>
<br>
## 활용 기술
Current Weather API<br>
URLSession<br>
<br>
## 앱 통신과 프로토콜
인터넷 상에서의 통신을 말한다<br>
많은 정보들이 주고 받기에 인터넷에는 엄격한 규약이 존재한다<br>
이것을 프로토콜이라고 부른다<br>
<br>
# HTTP
hyper text를 전송하기 위한 프로토콜<br>
기본적으로 요청 request와 응답 response으로 이루어져 있다<br>
(인터넷 프로그래밍 시간에 지겹도록 했다)<br>
클라이언트가 웹서버에게 요청하면 그에 맞는 응답 결과를 돌려준다<br>
계속 연결되어 있지 않다는 것이 http통신의 특징이다<br>
<br>
http 통신은 요청을 보내고 응답을 받을 때, 그 정보를 패킷에 담아 보내는데 <br>
패킷은 크게 헤더와 바디로 이루어져 있다.<br>
헤더는 보내는 사람의 주소, 받는 사람의 주소, 패킷의 생명 시간 등이 담겨져 있고<br>
바디에는 우리가 전하고자 하는 실제 내용이 들어있다.<br>
<br>
클라이언트가 서버에게 http 통신을 요청하려면 url 주소와 http 메소드를 정해줘야 한다<br>
서버에서는 메소드에 따라 어떤 요청인지 분간할 수 있다,<br>
GET:클라이언트가 서버에 리소스를 요청할 때 사용<br>
POST:클라이언트가 서버의 리소스를 새로 만들 때 사용<br>
PUT:클라이언트가 서버의 리소스를 전체 수정할 때 사용<br>
PATCH:클라이언트가 서버의 리소스를 일부 수정할 때 사용<br>
DELETE:클라이언트가 서버의 리소스를 삭제 할 때 사용<br>
HEAD:클라이언트가 서버의 정상 작동 여부를 확인할 때 사용<br>
OPTIONS:클라이언트가 서버에서 해당 URL이 어떤 메소드를 지원하는지 확인 할 때 사용<br>
CONNECT:클라이언트가 프록시를 통하여 서버와 SSL 통신을 하고자 할 때 사용<br>
TRACE:클라이언트와 서버간 통신 관리 및 디버깅을 할 때 사용<br>
<br>
<br>
# 상태코드
100번대 informational: 요청 정보를 처리 중<br>
200번대 success: 요청을 정상적으로 처리함<br>
300번대 redirection: 요청을 완료하기 위해 추가 동작 필요<br>
400번대 client error: 서버가 요청을 이해하지 못함<br>
500번대 server error: 서버가 요청 처리를 실패함<br>
<br>
# Apple에서 http - http 통신을 하기 위해 만든 URLSession
특정한 url을 이용하여 데이터를 다운로드하고 업로드 하기 위한 API<br>
앱은 하나 이상의 urlSession 인스턴스를 생성하며, 각 인스턴스는 관련 데이터 전송 작업 그룹을 조정한다<br>
URLSession은 request 와 reponse를 기본 구조로 갖고 있다<br>
request는 서버로 요청을 보낼 때, 어떤 http 메소드를 사용할 것인지, 캐싱 정책은 어떻게 할 것인지 설정할 수 있고<br>
reponse는 url요청의 응답을 나타내는 객체다<br>
URLSession은 URLSessionconfiguration을 통해 생성할 수 있다<br>
이렇게 생성된 URLSession을 통해 한 개 이상의 URLSessionTask를 생성할 수 있으며 이 URLSessionTask를 통해 실제 서버와 통신할 수 있다.<br>
<br>
URLSessionAPI는 여러가지 유형의 세션을 제공한다<br>
이 타입은 URL세션 객체가 소유한 configuration property 객체에 의해 결정이 된다<br>
URL세션의 종류<br>
-공유 세션(Shared Session)<br>
기본 요청을 하기 위한 세션, 싱글톤으로 사용<br>
URLSession.shared()<br>
-기본 세션(Default session)<br>
공유 세션과 유사하게 작동하지만, 직접 원하는 설정을 할 수 있다<br>
캐시와 쿠키 인증 등을 디스크에 저정한다<br>
또 선천적으로 데이터를 생성하기 위해 델리게이트를 지정할 수 있다<br>
-임시 세션(Ephemeral Session)<br>
공유 세션과 유사하나 캐시, 쿠키, 사용자 인증정보를 디스크에 저장하지 않는다<br>
메모리에 올려서 세션에 저장하고, 세션 만료시 데이터가 사라진다<br>
-백그라운드 세션(background session)<br>
백그라운드 세션을 사용하면 앱이 실행되지 않는 동안 background 에서 컨텐츠 업로드 및 다운로드를 할 수 있다<br>
<br>
### URLSessionTask
이렇게 URLSession이 구성되었으면, URLSessionTask를 이용해 각 세션내에 작업을 추가할 수 있다<br>
Task의 종류는 다음과 같다<br>
-URLSessionDataTask<br>
데이터 객체를 사용해 데이터를 요청하고 응답한다<br>
주로 짧고 빈번하게 요청하는 경우 사용된다<br>
-URLSessionUploadTask<br>
데이터 객체 또는 파일 형태의 데이터를 업로드 하는 작업을 수행한다<br>
앱이 실행되지 않았을 때, 백그라운드 업로드를 지원한다<br>
-URLSessionDownloadTask<br>
데이터를 다운로드 받아서 파일의 형태로 저장하는 작업을 수행<br>
앱이 실행중이 아닐 때, 백그라운드 다운로드를 지원<br>
-URLSessionStreamTask<br>
TCP/IP 연결을 생성할 때, 사용되는 Task<br>
-URLSessionWebSocketTask<br>
웹소켓 프로토콜 표준을 통해, 통신하는 task이다<br>
<br>
### URLSession Life Cycle
1. Session Configuration을 결정하고 Session을 생성<br>
2. 통신할 URL과 Request 객체를 설정<br>
3. 사용할 Task를 결정하고 그에 맞는 completion handler나 delegate메소드를 작성한다<br>
4. 해당 Task를 실행<br>
5. Task완료 후 completion handler 클로저가 호출<br>
<br>

# REST API

RESTful한 API를 말하며, 일련의 특징과 규칙 등을 지키는 API다.

### 특징

1. Uniform-Interface

API에서 자원들은 각각의 독립적인 인터페이스를 가진다.
각각의 자원들이 url 자원식별, 표현을 통한 자원조작, Self-descriptive messages, HATEOAS 구조를 가지는 것을 말한다.

**url 자원식별**

identification of resources를 말한다. 자원은 url로 식별돼야 한다.

**표현을 통한 자원조작**

manipulation of resources through representations은 url과 GET, DELETE 등 HTTP 표준 메서드 등을 통해 자원을 조회, 삭제 등 작업을 설명할 수 있는 정보가 담겨야 한다는 것을 의미한다.

**Self-descriptive messages**

HTTP Header에 타입을 명시하고 각 메시지(자원)들은 MIME types에 맞춰 표현돼야 한다.
예를 들어 .json을 반환한다면, application/json으로 명시해줘야 한다.
MIME types는 문서, 파일 드으이 특성과 형식을 나타내는 표준이다.
IETF의 RFC6838에 정의 및 표준화가 되어 있다.
'font/ttf', 'text/plain', 'text/csv'등을 말한다.

**HATEOAS 구조**

Hypermedia as the Engine of Application State의 약자다.
하이퍼링크에 따라 다른 페이지를 보여줘야 하며, 데이터마다 어떤 URL에서 원했는지 명시해야 하는 것이다.
보통은 href, links, link, url 속성 중 하나에 해당 데이터의 URL을 담아서 표기해야 한다.
링크를 유추할 수 있는 변수명을 쓰면 된다.

2. Stateless

이 규칙은 HTTP 자체가 Stateless이기 때문에 HTTP를 이용하는 것만으로도 만족된다.
그리고 이는 REST API를 제공해주는 서버는 세션을 해당 서버 쪽에 유지하지 않는다는 의미다.

3. Cacheable

HTTP는 원래 캐싱이 된다. 아무런 로직을 구현하지 않아도 자동으로 캐싱이 된다.
새로고침을 하면 304가 뜨면서 원래 있던 js와 css 이미지 등을 불러오는 것을 볼 수 있다.
이는 HTTP 메서드 중 GET에 한정되며, 한정된 시간을 정할 수가 있다.
캐싱된 데이터가 유효한지를 판단하기 위해 'Last-modified'와 'Etag'라는 헤더값을 쓴다.
'Etag'는 전달되는 값에 태그를 붙여서 캐싱되는 자원인지를 확인해주는 것이다.

4. Client-Server 구조

클라이언트와 서버가 서로 독립적인 구조를 가져야 한다.
물론 이는 HTTP를 통해 가능한 구조다.
서버에서 HTTP 표준만 지킨다면 웹에서는 그에 따른 화면이 잘 나온다.
서버는 그저 API를 제공하고, 그 API에 맞는 비즈니스 로직을 처리하면 된다.
마찬가지로 클라이언트에서는 HTTP로 받는 로직만 잘 처리하면 된다.

5. Layered System

계층 구조로 나눠져 있는 아키텍쳐를 뜻한다.
WEB 기반 서비스를 하면 보통 이런 시스템을 구축하게 된다.

## REST API의 URI 규칙

자원을 표기하는 URI의 아래 6가지 규칙을 적용해야 한다.

1. 동작은 HTTP 메서드로만 해야 하고, url에 해당 내용이 들어가면 안 된다.
2. .jpg, .png 등 확장자는 표시하지 말아야 한다.
3. 동사가 아닌 명사로만 표기해야 한다.
4. 계층적인 내용을 담고 있어야 한다. '/집/아파트/전세' 이런 식으로 내려가야 한다.
5. 대문자가 아닌 소문자로만 쓰며, 너무 길어서 바를 써야 한다면, 그냥 -(바)를 쓴다.
6. HTTP 응답 상태코드를 적재적소에 활용한다. 성공시에는 200, 리다이렉트는 301 등으로

### 쿼리스트링

REST API는 /를 기반으로만 구축되는 것도 있지만, 적절히 쿼리 스트링을 혼재해서 쓰기도 한다.
검색, 페이지네이션, 정렬 등 매개변수가 많거나 복잡할 때 쓰면 좋다.

# 브라우저 렌더링 과정

브라우저는 브라우저 엔진, 렌더링 엔진, 네트워크 통신부, 자스크립트 해석기, UI 백엔드, 자료 저장소로 이뤄져 있다.
이중 렌더링 엔진이 브라우저 엔진을 바라보며, DOM 트리와 CSS 파서 등을 기반으로 렌더 트리를 구축해 결과적으로 우리가 보는 화면을 구축한다.

### DOM트리

하나의 html 페이지는 div, span 등의 요소를 가진다. 이런 요소들이 HTML 파서에 의해 "구문분석"된다.
그리고 요소는 하나하나가 모두 노드(Node)로 설정되어 트리 형태로 저장이 되는데, 이를 "DOM 트리"라고 한다.
div > span, span 이라는 요소가 있다면 div라는 부모노드 밑에 span이라는 자식 노드가 2개 생긴다.

### CSSOM 트리

각각의 노드는 CSS 파서에 의해 정해진 스타일 규칙이 적용되어 있다.
"span.color = "red"는 노드 색깔이 빨간색이다." 등을 의미한다.
이런 걸 기반으로 CSSOM이라는 트리가 만들어진다.
이 과정은 DOM 트리 구축과 "동시에" 일어난다.

### 렌더 트리와 렌더레이어 생성

DOM 트리와 CSSOM 트리가 합쳐져 렌더객체(Render Object)가 생성된다.
그리고 이들이 모여 병렬적인 렌더 트리가 생성된다.

이때 "display: none"이 포함된 노드는 지워지고, font-size 등 상속적인 스타일은 부모 노드에만 위치하도록 설계하는 등의 최적화를 거쳐 렌더 레이어가 완성된다.

"display: none"은 렌더 트리에서 삭제되지만, "visibility: hidden"은 요소를 보이지 않게 하지만, 여전히 레이아웃에서 공간을 차지한다.

렌더 레이어가 완성될 때, GPU에서 처리되는 부분(CSS3D / video & canvas / filter / animation / transfrom: translateZ(0)) 등이 있다.
이 요소들은 각각 강제적으로 그래픽 레이어(Graphic Layer)로 분리된다.

### 렌더레이어를 대상으로 Layout 설정

이때 좌표는 보통 부모를 기준으로 설정된다. Global Layout은 브라우저 사이즈가 증가하거나, 폰트 사이즈가 커지면 변경된다.

### 렌더 레이어를 대상으로 칠하기 (Paint)

픽셀마다 점을 찍듯 칠한다. 이를 레스터화라고 한다.

### 레이어 합치기 (Composite layer) 및 표기

각각의 레이어로부터 비트맵이 생성되고, GPU에 텍스처로 업로드된다.
그 다음, 텍스처들은 서로 합쳐져 하나의 이미지로 렌더링 되며 화면으로 출력된다.

### 렌더 트리와 DOM 트리는 1 : 1 대응인가

아니다. DOM 트리 > 렌더 객체 > 렌더 트리가 되는 과정에서 display: none 으로 사라지는 렌더 객체(노드)가 있을 수 있기에 1 : 1 대응이 아니다.

### www.naver.com을 쳤을 때 생기는 과정과 DNS

> 리다이렉트, 캐싱, DNS, IP 라우팅 & ARP, TCP 연결 구축을 거쳐 요청과 응답이 일어나는 TTFB(Time to First Byte)가 시작되고, 이 후 컨텐츠를 다운받게 된다. 그 이후에 브라우저 렌더링 과정을 거쳐 네이버라는 화면이 나타난다.

#### 리다이렉트

리다이렉트가 있다면, 진행하고, 없다면 그대로 해당 요청에 대한 과정이 진행된다.

#### 캐싱

> 요청된 값의 결과값을 저장하고, 그 값을 다시 요청하면 다시 제공하는 기술이다.

해당 요청이 캐싱이 가능한지 아닌지를 파악한다.
캐싱이 이미 된 요청이라면, 캐싱된 값을 반환하고, 아니라면 그 다음 단계로 넘어간다.

1. 브라우저 캐시

쿠키, 로컬 스토리지 등을 포함한 캐시다. 개인캐시라고도 한다.
브라우저 자체가 사용자가 HTTP를 통해 다운로드하는 모든 문서를 보유하는 것이다.
예를 들어, 어떤 사이트를 갔다가 다시 방문하면 굉장히 빠르게 콘텐츠가 나타나는 이유가 이것 때문이다.

2. 공유 캐시

클라이언트와 서버 사이에 있으며, 사용자간에 공유할 수 있는 응답을 저장한다.
대표적인 예로, 요청한 서버 앞단에 프록시 서버가 캐시하는 것을 말한다.
이를 리버스 프록시를 둬서 내부 서버로 포워드한다고도 말한다.

예를 들어, Node.js 서버를 구축할 때 앞단에 프록시 서버로 nginx서버를 둬서 이 서버를 캐싱 서버로도 사용할 수 있다.
또한 AWS Cloudfront 또는 Cloudflare와 같은 콘텐츠 전송 네트워크 (CDN)을 둬서 캐싱할 수도 있다.

#### DNS

> 계층적인 도메인 구조와 분산된 데이터베이스를 이용한 시스템으로 FQDN을 인터넷 프로토콜인 IP로 바꿔주는 시스템이다. 이는 DNS 관련 요청을 네임서버로 전달하고 해당 응답값을 클라이언트에게 전달하는 리졸버, 도메인을 IP로 변환하는 네임 서버 등으로 이뤄져 있다.

캐싱을 거쳐서 요청해야 함이 분명하다면, 실제 서버에 요청할 단계다.
브라우저가 요청한 FQDN(Fully Qualified Domain Name)인 www.naver.com 등의 이름을 DNS를 통해 실제 IP 주소를 확인한다.

\*FQDN : 호스트와 도메인이 합쳐진 완전한 도메인 이름을 말한다. www 등은 호스트 부분이고, naver.com 은 도메인이라고 한다.

예를 들어, www.naver.com에 DNS 쿼리가 오면 오른쪽부터 역순으로 [Root DNS] -> [.com DNS] -> [.naver DNS] -> [.www DNS] 과정을 거쳐 완벽한 주소를 찾아 IP 주소를 매핑한다.

#### DNS 캐싱

미리 해당 도메인 이름을 요청했다면, 로컬 PC에 자동적으로 저장된다. 브라우저 캐싱과 OS 캐싱이 있다.

#### IP 라우팅

해당 IP를 기반으로 IP 라우팅이 일어나고 ARP 과정을 거쳐 실제 서버를 찾는다.

#### TCP 연결 구축

브라우저가 TCP 3웨이 - 핸드셰이크 및 SSL 연결 등을 통해 연결을 설정한다.
이후 요청을 보낸 후, 드디어 해당 요청한 서버로부터 응답을 받는다.
TCP 연결은 HTTP/2까지 일어난다. HTTP/3는 QUIC을 통해 연결하고 데이터를 주고 받는다.

#### 콘텐츠 다운로드

브라우저는 사용자가 요청한 컨텐츠를 서버로부터 다운받는다.

#### 브라우저 렌더링

받은 데이터를 바탕으로 브라우저 엔진이 브라우저 렌더링 과정을 거쳐 화면을 만든다.
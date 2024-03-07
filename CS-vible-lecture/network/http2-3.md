# HTTP/2와 HTTP/3의 차이

### HTTP/2

구글은 2009년에 HTTP/1.1의 한계를 극복하기 위해 SPDY 프로토콜을 개발했다.
이후 2015년, 이를 기반으로 하는 HTTP/2 프로토콜을 만들었다.

1. 바이너리 포맷 계층

애플리케이션 계층과 전송 계층 사이에 `바이너리 포맷 계층`을 추가했다.
HTTP/1.0은 일반 텍스트 메시지를 전송하고, 줄바꿈으로 데이터를 나눴다.
HTTP/2.0은 0과 1로 이뤄진 바이너리 데이터로 변경됐고, 더 작은 메시지가 프레임으로 캡슐화되어 전송된다.

2. 멀티플렉싱

단일 TCP연결의 여러 스트림에서 여러 HTTP 요청과 응답을 비동기적으로 보낼 수 있다.
이를 통해 HOL을 해결했다.

HTTP/1.1에서는 병렬 요청을 하려면, 다중 TCP 연결을 통해서 하고, 일반적으로 TCP 연결 하나 당 병렬 요청은 불가능했다.

이를 HTTP/2.0에서는 리소스를 작은 프레임으로 나누고, 이를 스트림으로 프레임을 전달한다.
각각의 프레임은 스트림ID, 해당 청크의 크기를 나타내는 프레임이 추가되었기 때문에 작게 나눠서 다운로드가 되더라도 결과적으로 응답데이터에서는 올바른 순서로 재조립할 수 있게 된다.

3. 서버푸시

서버가 리소스를 클라이언트에 푸시를 할 수 있다.
요청된 html파일과 함께 다른 개체를 별도로 보낼 수 있다.
만약 요청한 html에 css가 포함되어있다면, 별도 요청없이 css를 같이 보낼 수 있다.

4. 헤더압축

HTTP/1.1에서는 무거운 헤더가 있었지만, 이를 허프만 인코딩 압축 방법 등으로 압축시켰다.
똑같은 서버에서 2개의 이미지를 준다고 했을 때, 중복되는 헤더는 제외한 채 보내고, 해당 공통 필드로 헤더를 재구성하며, 중복되지 않은 헤더값은 허프만 인코딩 압축 방법으로 압축해 전송한다.

\*허프만 인코딩이란?
문자열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트수를 사용해 표현한다.
빈도가 낮은 정보는 비트 수를 많이 사용해 전체 데이터 표현에 필요한 비트양을 줄이는 알고리즘이다.

5. 우선순위

서버에서 원하는 순서대로 우선순위를 정해 리소스를 전달할 수 있다.

### HTTP/3

HTTP/2는 여전히 TCP를 사용하기에 초기 연결에 대한 RTT로 인한 지연시간이라는 문제점이 있고, 이를 해결했다.

QUIC(Quick UDP Internet Connections) 이라는 계층 위에서 돌아간다.
TCP 기반이 아닌 UDP기반으로 돌아간다.
HTTP/2에서 장점이었던 멀티플렉싱 등을 갖고 있고, 초기연결성정시 지연시간 감소라는 대표적 특성을 갖고 있다.

HTTP/2의 경우, 3 - RTT가 필요했다면, QUIC는 1 - RTT만 필요하다는 장점이 있다.
TLS로 암호화 통신을 구축할 때의 단 한 번의 핸드셰이크를 활용해 클라이언트와 서버간의 연결, 암호화 통신 모두 다 구축을 한다.
이를 통해 1 - RTT만에 모든 연결을 성립할 수 있다.

또한 정송된 패킷이 손실됐다면, 수신측에서 에러를 검출하고 수정하는 방식이다.
열악한 네트워크 환경에서도 낮은 패킷손실률을 자랑하는 순방향 오류 수정 매커니즘(FEC, Forward Error Correction)이라는 특성을 가진다.
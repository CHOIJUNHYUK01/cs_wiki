# CORS

> Cross Origin Resouce Sharing의 약자다. HTTP 헤더를 기반으로 브라우저가 다른 오리진에 대한 리소스 로드를 허용할지 말지에 대한 메커니즘을 말한다.

### 오리진

https://site.com:8080

    https: // protocol
    site.com // hostname
    8080 // port

hostname + port = host
host + protocol = origin

### SOP (Same-Origin Policy)

브라우저 상에서 오로지 같은 오리진끼리만 요청을 허가하는 보안정책이다.
이러한 SOP가 없다면 내 계정 정보가 변경되거나 유출될 수 있다.
이를 1차적으로 막아주는 게 SOP 보안정책이다.

하지만 다른 오리진끼리 요청해야 하는 순간이 온다면 이를 브라우저 상에서 조금 더 유연하게 바꿔서 어떠한 경우에는 다른 오리진끼리도 요청 및 응답할 수 있게 만든 게 CORS다.

### preflight request

만약 요청을 보낼 때, GET, HEAD, POST와 같은 메서드 타입, 헤더에 해당되지 않은 게 하나라도 포함이 된다면 preflight request를 보낸다.
OPTIONS 메서드로 해당 서버에 원래 요청을 보내기 전 요청을 보내서 해당 서버의 Access-Control-\* 을 파악해, 만약 없다면 CORS 에러를 뿌리게 되는 요청이다.

    메서드 타입 : GET, HEAD, POST

    헤더 : Accept, Accept-Language, Content-Language, Content-Type, -application/x-www-form-urlencoded, -multipart/form-data, -text/plain, Range(참고로 firefox 브라우저는 해당 헤더를 허용하지 않는다)

아래와 같은 메서드 타입과 헤더를 가진 요청을 간단한 요청(simple request)이자 안전한 요청이라고 한다.

    Access-Control-*이란?

    오리진 : Access-Control-Allow-Origin
    메서드 : Access-Control-Allow-Methods (허용된 방법)
    헤더 : Access-Control-Allow-Header(허용된 헤더)
    인증관련 헤더(true or false): Access-Control-Allow-Credentials

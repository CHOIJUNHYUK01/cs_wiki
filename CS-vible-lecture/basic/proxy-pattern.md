# 프록시 패턴

> 객체가 어떤 대상 객체에 접근하기 전, 그 접근에 대한 흐름을 가로채서 해당 접근을 필터링하거나 수정하는 등 역할을 하는 계층이 있는 디자인 패턴이다.

프록시 서버도 이 패턴을 사용하는 대표적인 예시다.
서버 앞단에 두어 캐싱, 로깅 등에 활용하는 서버다.

`cloudflare`도 서비스 앞단에 프록시 서버를 두어 불필요하거나 공격적인 트래픽을 막는다.

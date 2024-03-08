# 로컬스토리지

> 웹 스토리지 객체로, 브라우저 내에 { key : value } 형태로 오리진에 종속되어 저장되는 데이터다. (오리진이 같은 브라우저 내에서 공유 된다.)

하나의 키에 오로지 하나의 값만 저장된다.
데이터는 사용자가 브라우저에서 수동으로 삭제하지 않는 한, 평생 로컬 저장소에 저장되며 만료 날짜가 ㄷ없다.
사용자가 창이나 탭을 닫아도, 컴퓨터를 종료해도 만료되지 않는다.
단, 최대 저장용량은 5MB다.

보통 사용자의 행위를 기억할 때 사용된다.
가령 로그인을 유지하기 위한 값 등으로 사용되며, 로컬 스토리지 데이터는 자동으로 서버에 전송되지 않는다.
다만 쿠키는 자동으로 전송된다.

### 사용법

```javascript
// 설정
localStorage.setItem(key, value);
// key에 해당하는 value 가져오기
localStorage.getItem(key);
// 제거
localStorage.removeItem(key);
// 전체 제거
localStorage.clear();
```

### 오리진

    https://site.com:8080/path/page?p1=v1&p2=v2#hash

이렇게 있다고 치자.

전체는 `href`라고 한다.

`protocol`은 `https:`까지다.
`host`는 `hostname`과 `port`로 이뤄져 있다. `site.com`이 host, `8080`이 port다.

이 두 가지를 합친걸 `origin`이라고 한다.

`/path/page`까지가 `pathname`이라고 한다.
`?p1=v1&p2=v2`는 `search`라고 한다.
`#hash`는 `hash`다.

### 캐싱

UX를 개선하기 위해 텍스트 창에 입력한 값을 로컬 스토리지를 통해 캐싱하는 게 그 예시다.
브라우저의 로컬 스토리지가 갖고 있는 값을 통해 입력창에 해당 값을 미리 넣어놓는 것이다.

# 세션 스토리지

> 로컬 스토리지와 매우 유사하다. 이것도 웹 스토리지 객체로 브라우저 내에 { key : value } 형태로 오리진에 저장되는 데이터다.

하나의 키에 오로지 하나의 값만 저장된다.
최대 저장용량은 5MB다.

단, 사용자가 브라우저 탭을 닫으면 데이터는 만료된다.

### 사용법

사용법도 로컬스토리지와 동일하다.
localStorage를 sessionStorage로 바꾸면 된다.

보통 세션 스토리지보다는 로컬 스토리지를 많이 사용한다.
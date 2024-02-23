# MVC 패턴

> 모델, 뷰, 컨트롤러로 이뤄진 디자인 패턴이다.

### 모델

> 앱의 데이터인 데이터베이스, 상수, 변수 등을 뜻한다.

뷰에서 데이터를 생성하거나 수정할 때, 컨트롤러를 통해 모델이 생성 또는 업데이트 된다.

### 뷰

> inputbox, checkbox, textarea 등 사용자 인터페이스 요소를 나타내며, 모델을 기반으로 사용자가 볼 수 있는 화면을 뜻한다.

모델이 갖고 있는 정보를 따로 저장하지 않아야 하고, 변경이 일어나면 컨트롤러에 이를 전달해야 한다.

### 컨트롤러

> 하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 하며, 이벤트 등 메인 로직을 담당한다.

모델과 뷰의 생명 주기도 관리한다.
모델이나 뷰의 변경 통지를 받으면 이를 해석해 각각 구성 요소에 해당 내용을 알려준다.

### 장점

1. 앱의 구성 요소를 세 가지 역할로 구분해 개발 프로세스에서 각각의 구성 요소에만 집중해 개발할 수 있다.
2. 재사용성과 확장성이 용이하다.

### 단점

앱이 복잡해질수록 모델과 뷰의 관계가 복잡해진다.

# 이와 비슷한 MVP 패턴

> 컨트롤러 대신 프레젠터로 교체된 패턴이다. 이는 뷰와 프레젠터가 1 : 1 관계로, MVC 보다 더 강한 결합을 지닌 디자인 패턴이다.

# MVVM 패턴

> 컨트롤러가 뷰모델로 바뀐 패턴이다. 뷰모델은 뷰를 추상화한 계층이고, VM : V = 1 : N 이라는 관계를 갖는다.

VM은 커맨드와 데이터 바인딩을 가진다.

    커맨드 : 여러 요소에 대한 처리를 하나의 액션으로 처리할 수 있는 기법
    데이터 바인딩 : 화면에 보이는 데이터와 브라우저 상의 메모리 데이터를 일치시키는 방법

## 최종 차이점

| 특징 | MVC                    | MVP                    | MVVM                 |
| ---- | ---------------------- | ---------------------- | -------------------- |
| 관계 | C : V = 1 : n          | P : V = 1 : 1          | VM : V = 1 : n       |
| 참조 | 뷰는 컨트롤러를 참조 X | 뷰는 컨트롤러를 참조 O | 뷰는 뷰모델을 참조 O |
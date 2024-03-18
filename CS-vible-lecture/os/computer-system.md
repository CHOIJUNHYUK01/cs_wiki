# 운영체제와 컴퓨터시스템의 구조

### 운영체제 종류

1. GUI

> 그래픽을 사용해 컴퓨터와 상호작용하는 인터페이스다. windowOS, macOS 등 현대 OS가 이를 대표한다.

2. CUI

> 사용자가 키보드만을 사용해 문자를 기반으로 컴퓨터와 상호작용하는 인터페이스다. MS-DOS가 대표적이다.

터미널을 생각하면 된다.
chatGPT 또한 이에 속한다.

### 운영체제의 역할

> 운영체제의 커널이 담당한다.

1. CPU 스케줄링과 프로세스 상태관리
2. 메모리관리
3. 디스크 파일 관리
4. I/O 디바이스 관리

### 운영체제의 구조

1. 유저프로그램
2. 하드웨어

- OS가 담당하는 부분

1. 인터페이스(GUI 또는 CUI)
2. 시스템콜
3. 커널(I/O 드라이버, 파일시스템 등)

### 컴퓨터 시스템의 구조

1. CPU : 인터럽트에 의해 메모리에 존재하는 명령어를 해석해 실행하는 일꾼
2. DMA 컨트롤러 : CPU의 일을 보조하는 일꾼
3. 메모리 : 전자회로에서 데이터, 상태 등을 기록하는 장치(작업장)
4. 타이머 : 특정 프로그램에 시간을 다는 역할
5. 디바이스 컨트롤러 : IO 디바이스들의 작은 CPU
6. 로컬버퍼 : 디바이스에 달려있는 작은 메모리

### CPU

> 산술논리연산장치, 제어장치, 레지스터로 구성된 장치다. 인터럽트에 의해 메모리에 존재하는 명령어를 해석해 실행한다.

- 산술논리연산장치

ALU(arithmetic and logical unit)은 덧셈, 뺄셈 등 산술연산과 논리연산을 하는 회로장치다.

- 제어장치

CU(control unit)는 프로세스의 조작을 지시하며, 명령어를 읽고 해석하며 데이터 처리를 위한 순서를 결정한다.

- 레지스터

CPU 안에 있는 매우 빠른 임시기억장치다.

### 인터럽트

> 어떤 신호가 들어왔을 때, CPU를 잠시 정지시키는 것을 말한다. 0으로 숫자를 나누는 산술 연산오류, 프로세스 오류 등으로 발생한다.

오류 뿐만 아니라, 키보드, 마우스 등 IO 디바이스를 사용할 떄의 인터럽트, 우선순위가 높은 프로세스의 발생 등으로 발생한다.

CPU는 메모리에 있는 명령어를 순차적으로 실행하는데
인터럽트가 발생되면 점프해서 인터럽트 핸들러 함수가 모여있는 인터럽트 벡터로 가서 인터럽트 핸들러 함수(인터럽트 서비스 루틴, ISR)가 실행된다.
이후 인터럽트가 종료되면 다시 순차적으로 실행한다.

### 인터럽트 종류

> 하드웨어 인터럽트, 소프트웨어 인터럽트 두 가지로 나뉜다.

1. 하드웨어 인터럽트

IO 디바이스 등 하드웨어에서 발생하는 인터럽트다.
예를 들어, 마우스를 기반으로 버튼을 클릭할 떄, 디스크에서 파일읽기, 쓰기 작업이 완료됐을 때 발동된다.

2. 소프트웨어 인터럽트

트랩이라고도 한다.
프로세스 오류, 프로세스 종료, 시작 등을 기반으로 프로세스에서 발생하는 인터럽트다.
하드웨어 인터럽트보다 우선순위가 높은 인터럽트다.
# 취업 인터뷰 준비

### UI 처리를 위한 메인 스레드

- 성능: 멀티스레드를 많이 활용
- UI: 단일 스레드 모델 적용
    - 교착 상태, 경합 상태 등 여러 문제 발생 가능
    - 메인 스레드에서만 허용
- 과정: 앱 프로세스 시작 -> 메인스레드(UI스레드) 생성

### Looper Class

- messagequeue에서 message를 Handler에 전달함.
- 스레드 별로 Looper 생성 -> TLS(Thread local storage)에 저장되고 꺼내짐
- set()으로 Looper 추가 / get()으로 Looper를 가져온다.
- Looper.prepare(): 스레드 별로 Looper생성
- 각각의 MessageQueue(메시지를 담는 자료구조)를 가짐 -> 경합 상태 해결

### Handler
- Message를 MessageQueue에 넣는 기능과 꺼내서 처리하는 기능
- post(), postAtTime(), postDelayed() 메서드를 통해서 Runnable 객체 전달
- Handler의 용도
    - 백그라운드 스레드에서 UI 업데이트: 백그라운드 스레드에서 네트워크, 데이터베이스 작업 등을 하는 도중에 UI 업데이트
    - 메인스레드에서 다음 작업 예약: 다음 UI 작업을 MessageQueue에 넣음.
    - onCreate()에서 Handler의 post()에 전달한 Runnable은 onResume() 이후에 실행

- Message를 보낸다는 것: 메시지에 저장된 데이터의 종류를 식별하기 위한 값을 상수로 정의, HandlerMessage()에서는 상수 값에 따른 처리 코드를 조건문으로 작성해야 함. -> 오직 대상 스레드에 작성된 코드를 실행하기 위해서
- Runnable을 보낸다는 것: 핸들러 사용의 주 목적이 대상 스레드의 코드를 실행하는 것 -> 실행 코드를 보낸다?! -> 실행 코드가 담긴 객체

### Dialog
- 사용자에게 추가 정보 입력, 결정을 내릴 때 표시하는 작은 화면

### Toast
- 작은 팝업으로 메시지에 필요한 공간만 차지하고 진행 중인 작업이 그대로 표시되고 사용자와 상호작용이 유지됨.

### Snackbar
- 토스트와 유사하지만 사용자가 메시지에 응답할 수 있다.

### Context
- 안드로이드 시스템이 어플리케이션이나 컴포넌트 등의 현재 맥락을 관리하기 위한 것
- 여러 컴포넌트의 상위 호환
- 추상 클래스이며 메서드 구현이 거의 없음
- 상수 정의와 추상 메서드로 이루어짐.
- context를 직접 상속한 것은 contextwrapper이며 이를 상속한 것은 activity, service, application
- 생성된 객체에서 어떤 일이 일어나고 있는지 알 수 있음.
- 어플리케이션에 관련하여 시스템이 관리하고 있는 정보에 접근

    - Application Context
        - Application lifecycle에 귀속
        - 앱이 죽기 전까지 동일한 객체 귀속
        - 어떤 context보다 오래 유지

    - Activity Context
        - Activity LifeCycle에 귀속
        -getContext()로 접근
        - Activity 범위 내에서 전달

### Annotation
- 특정 클래스, 변수, 메서드 등에 붙이는 코드로 해당 타겟의 기능을 좀 더 명확히 설명함.
- ex) @peprecated, @suppresswarning

### LayoutInflator
- xml에 저장된 자원들을 view형태로 반환
- 자바 코드에서 view, viewgroup을 사용하거나 Adapter의 getview() 등 배경화면이 될 Layout을 만들어놓고 View 형태로 변환받아  Activity, Fragment에서 실행
- setContentView()와 같은 원리






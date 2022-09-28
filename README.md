# 취업 인터뷰 준비

### UI 처리를 위한 메인 스레드

- 성능: 멀티스레드를 많이 활용
- UI: 단일 스레드 모델 적용
    - 교착 상태, 경합 상태 등 여러 문제 발생 가능
    - 메인 스레드에서만 허용
- 과정: 앱 프로세스 시작 -> 메인스레드(UI스레드) 생성

### Looper Class

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




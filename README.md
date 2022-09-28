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




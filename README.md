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

### Android JetPack

- 앱을 구축하는데 도움이 되는 훌륭한 도구
- 개발자들이 더욱 쉽게 높은 클라스의 앱을 구현하도록 도와주는 라이브러리 모음
- 4 가지가 존재(Foundation, Architecture, Behavior, UI)
    - Foundation
        - 기본 컴포넌트
        - Backward Compatibility, Testing, Kotlin language support
            - App Compat: 오래된 버전(support)와 미터리얼 디자인 지원
            - Androidx: extension을 간결하게 쓰고 직관적으로 보이게
            - Multidex: 앱에 대한 여러 dex file 지원
            - Test: 단위 및 런타임 UI 테스트
    - Architecture
        -  Robust Apps / Testable APps / Maintainable Apps
            - Data binding: 레이아웃의 UI 요소를 앱의 데이터 소스에 선언함으로서 바인딩
            - LifeCycle: Activity와 Fragment의 LifeCycle을 관리
            - LiveData: 변경사항이 있으면 View에 알림
            - Navigation: 앱 네비게이션에 필요한 모든 것을 핸들링
            - paging: 데이터 소스에 필요에 따라 순차적 정보를 불러옴.
            - Room: SQLite에 접근
            - ViewModel: LifeCycle에 관련된 UI를 관리
            - WorkManager: 백그라운드 작업 관리

### onStop에서 DB 업데이트가 모두 저장?
- 몇몇의 경우엔 onStop이 호출되지 않음.
- 메모리 부족이나 configuraiton changed 경우 강제로 종료될 수 있음.
- back 버튼을 누를 경우 onSaveInstanceState 호출 x

### AsyncTask가 Deprecated된 이유?
- 비동기적으로 실행될 필요가 있는 작업들을 위해 사용되는 클래스
- 장점: 비동기 처리가 쉽고, 핸들러보다 코드가 깔끔한.
- 단점: 재사용이 불가, 종료하지 않으면 종료 x
    - 액티비티 종료 시점과 어싱크가 끝나는 시점이 다를 수 있으며 이는 메모리 누수를 야기함.
    - 순차 실행으로 인한 속도 저하
    - 프레그먼트에서 어싱크 실행시 액티비티와 fragment가 분리될 때 getContext, getActivity가 null이 될 수 있음.
    - 예외 처리가 없음

### SharedPreference
    - 데이터를 파일로 저장
    - key-value 형태로 원시적 데이터 형태로 저장
    - 단수 저장 경우 사용

### View
    - 화면에 보이는 모든 것
    - 자신이 화면 어디에 배치되어야 하는지에 대한 정보는 없음.
    - 화면에 배치되기 위해서는 ViewGroup(Layout), View Container에 담을 필요가 있음.
    - tools:context -> preview 기능을 도와줌.

### Process LifeCycle
- Android application은 linux 프로세스에서 실행된다.
- 해당 코드의 요구의 일부를 실행하는 경우 응용 프록램에 대해 생성되고 더 이상 필요로 하지 않을 때까지 계속 실행
- 가능한 오래 유지하려고 하지만, 프로세스 생성과 메모리 확보를 위해 종료시키는 경우가 있음.
- 중요도 결정을 통해서 가장 낮은 프로세스부터 종료의 대상
    - Foreground Process
        - 사용자가 현재 조작하고 있는 일에 대해 필요한 process
        - 사용자가 조작중인 Activity / BroadcastReceiver가 현재 동작 중인 상태
        - Service에서 콜백함수 활성화

    - Visible Process
        - Foregroud component를 가지고 있지만, 사용자가 화면에서 볼 수 없는 프로세스
        - onPause()가 호출되었지만, 여전히 화면에서 확인할 수 있는 activity ex) dialog
    - service Process
        - 1, 2에 포함 x
        - 사용자가 눈으로 확인할 수 있는 어떤 요소 외에도 연결되어있지 않지만, 사용자가 하고 있는 일에 영향을 주는 것
    - Cached Process
        - onStop()이후에 더 이상 사용자에게 보이지 않는 Process
        - 메모리가 부족할 경우 System이 이를 종료시킴
    - Empty Process
        - Acitivity component가 없는 process
        - 다음에 재실행될 때 시작 시간을 다운시키기 위해서
        - 빈번하게 방문할 경우 다시 로드해야하는데 이를 방지하기 위해 onDestroy() 이후에도 메모리 유지
        




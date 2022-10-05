# 취업 인터뷰 준비(2022/09/28 - 2022/10/05)

### Application Class
- 안드로이드 기본 클래스
- 안드로이드 앱의 모든 컴포넌트, 액티비티, 서비스를 포함하고 있는 클래스
- 다른 클래스보다 먼저 인스턴스화 된다.

### View.GONE과 View.INVISIBLE의 차이
- Invisible: 뷰를 그려놓고 보이지 않지만 레이아웃에 공간 차지
- Gone: getView()가 호출되지 않아 뷰를 그리지 않고 레이아웃에 공간을 차지하지 않음.

### Gradle (앱 수준/프로젝트 수준)
- 유연성과 성능에 중점을 둔 오픈소스 빌드 자동화 도구
- 자바 및 코드를 APK 파일로 컴파일하는데 도움이 됨.
- 모듈: 솟 파일 및 기능의 개별 단위로 프로젝트를 분할할 수 있도록 빌드 설정의 모음.

### Retrofit
- REST API 통신을 위해 구현된 라이브러리
- 백그라운드에서 실행되며 callback을 통해 메인스레드에서 UI 업데이트 제공
- HttpClient -> HttpUrlConnection -> Volley -> Okhttp와 Retrofit
- 사용하는 이유
    - HttpUrlConnection을 사용하면 매번 connection 설정을 해야하는 반복적인 작업을 진행해야함.
    - 속도, 편의성, 가독성이 좋음.
    - 자체적으로 비동기 실행과 스레드를 관리한다.

### FragmentManager VS SupportFragmentManager
- FragmentManager
    - Fragment 객체, 백스택을 관리함
    - Activity class에서 가져옴
    - Activity와 Fragment 둘다 관리
- SupportFragmentManager
    - FragmentActivity class에서 가져옴
    - androidx에서 사용하기 위한 fragmentManager
    - activity를 상속, androidx로 마이그레이션

### String VS StringBuffer
- String: 수정하려면 지우고 다시 생성
- StringBuffer: 필요한 크기를 변경하여 문서 변경

### View LifeCycle
1. View(context: Context): 코드에서 view를 동적으로 만들 때 사용, context는 view가 실행될 때 현재 리소스 등을 구성하는데 사용
2. Attachment/Detachment: view가 window에 연결/분리 될 때
3. onAttachToWindow: view가 window에 연결되면 호출
4. onDetachFromWindow: view가 window에서 분리될 때 호출
5. onFinishInflate: view가 전개가 끝날 때 호출
- Traversals: View 계층 구조는 부모 노드에서 분기가 있는 리프 노드의 트리 구조와 같음.
- Animate - Measure(View의 크기를 확인하기 위해 호출) - Layout(View를 측정하여 화면에 배치) - Draw(크기와 위치가 이전 단계에서 계산되어 View는 이를 기준으로 그릴 수 있음)
- requestLayout: 뷰가 변경되었을 경우, View를 다시 측정하기 위해 이 메소드 호출 (measure - Layout)

### 상태의 저장과 복구
- onSaveInstanceState(): Activity가 종료될 때 데이터를 저장, 상태를 저장하려면 고유 ID 제공
- Application Class: 라이프사이클을 알고 있고 어플리케이션 관리하는 메모리는 힙에 선언
- SharedPreference: xml 형태로 로컬에 저장
- Singleton: stack 영역에서 메모리 관리

### MutableLiveData를 선언하고 get()
- MutableLiveData: read / write 가능
- =과 get()의 차이
    - get()으로 가져올 때는 LiveData로 형 변환
    - = 사용시 LiveData 변수 하나가 생기면서 이 변수가 return


### by lazy와 lateinit
- 공통점
    - 나중에 초기화한다는 점
    - 초기화 이후에 값이 변할 수 있는 변수
- lateinit
    - var에서만 사용 가능
    - null이 되면 안되는 상황에서 사용
    - 초기화 하지 않으면 초기화하라는 메모
    - primitive type에는 적용 불가능
- by lazy
    - val에서만 사용 가능
    - 사용될 것이 사용 시 어떤 값에 들어가는지 x가 다른 계산식에 영향을 받거나 다른 변수를 초기화한 후에 값을 알 수 있는 경우

### kotlin scope function(범위 지정 함수)
- let
    - 자기 자신을 인수로 전달하고 수행된 결과 즉 블록의 마지막 값을 반환
- run
    - 익명 함수처럼 사용하는 방법과 객체를 호출하는 방법을 모두 제공
    - run 안에서 선언된 변수는 모두 임시로 사용
    - 마지막 결과를 반환
- with
    - 인수로 객체를 받고 블록에 리시버 객체로 전달
    - 블록에서 수행된 마지막 결과
    - null이 아닌게 확실한 경우에만 사용

- apply
    - 블록에 객체 자신이 리시버 객체로 전달되고 반환
    - 생성과 동시에 초기화되고 자기 자신을 return
- also
    - 수신 객체 지정 람다에 매개변수 T로 코드 블록 내에 명시적으로 전달되며 코드 블록 내에 전달된 수신객체를 그대로 반환

### 동일성과 동등성
- 동등성(==): 완전히 동일한 값인지?
- 동일성(===): 같은 주소를 창조하는지?

### data class에서 copy를 사용하는 이유
- 복사본은 원본과 다른 생명주기를 가지고 복사를 변경한 후에 변경해도 다른 부분에 영향을 주지 않음.

### 중첩 클래스와 내부 클래스
- 중첩 클래스: 바깥쪽 클래스에 대한 참조를 저장하지 않는다.
- 내부 클래스: 외부 클래스를 참조한다.

### companion object
- 클래스가 메모리에 적재되면서 함께 생성
- 최상위 함수의 객체 선언
- 클래스 내의 private 함수에 접근할 때 사용하는 객체
- 팩토리 패턴(한 종류의 객체를 만들기 위해서 해당 객체를 생성하는 팩토리 interface구현)을 구현하는데 효과적

### singleton
- 특정 클래스에 대한 인스턴스를 한번의 static 메모리 영역에 할당
- 해당 클래스에 대한 생성자를 여러 번 호출하더라도 최초의 생성된 객체 반환
- 장: 메모리 낭비 방지, 데이터 공유가 쉬움
- 단: 너무 많은 일을 하거나 많은 데이터 공유시 결합도가 높아짐.


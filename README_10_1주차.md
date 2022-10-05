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
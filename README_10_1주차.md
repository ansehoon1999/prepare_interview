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

# FragmentManager VS SupportFragmentManager
- FragmentManager
    - Fragment 객체를 관리함
    - Activity class에서 가져옴
    - Activity와 Fragment 둘다 관리

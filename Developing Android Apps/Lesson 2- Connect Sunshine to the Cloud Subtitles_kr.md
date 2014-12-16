01 - 소개
=================

1 단원에서 우리는 모의 늘어서 기본 UI에서 새 프로젝트를 구축했습니다
데이터. 이 단원에서는 햇빛을 연결합니다
클라우드에서 모의​​ 데이터와 교환
OpenWeatherMap API를 사용하여 실시간 기상 데이터입니다.
이를 위해 우리는 Android에 대해 알아 보겠습니다
허가제 네트워크 I / O 및 어떻게 이동하는 방법
시간 메인 UI 스레드에서 작업을 소모한다.02 - 오픈 날씨가 제공하는 리뷰 데이터
=============================================

저 주에, 우리는 우리의 태양 광 애플 리케이션을 만드는거야
OpenWeatherMap 서비스. OpenWeatherMap 무료 기상 데이터를 제공하고 있습니다
예측 API. 그리고 사이트 다음에 링크되어 있기 때문에,
당신이 함께 따를 수 있습니다. 사이트를 스크롤하여
당신이 사용할 수있는 데이터 유형을 알 수 있습니다.그
당신이 이것을 클릭 할 수 있기 때문에 또한 예제 쿼리를 가지고
날씨는 런던에서 무엇인지 확인 1.
그것은 날씨 사용자 친화적 인 설명이 포함
이런 경우에 깨진 구름 등의 조건. 과
우리는 우리의 응용 프로그램 이후를 사용합니다. 위해
기상 조건의 완전한 목록은 당신이 돌아갈 수 있습니다
메인 페이지. 그리고 아래로 스크롤합니다.그리고 클릭
날씨 조건 코드는 여기 링크에서.
이 페이지에서 우리는 완전한 목록을 가지고
기상 조건. 그것은 구름에서 모든 것이 포함되어 있습니다
비 얼음 또는 화산재. 나도 몰라
당신을 잘하면 너무 자주 발생하지 않습니다.03 - Web 쿼리를 시도
========================

이동하여 API에 익숙해 지도록되었습니다 시간이 걸릴
메인 페이지로 돌아가 다른 검색어를보고,
다른 매개 변수를 지원하고있다. 단지 URL의 쿼리 params를 수정
주소 표시 줄. 설정이 완료되면 구름에 떠있는 상자를 체크합니다.04 - 우리가 원하는 쿼리를 찾아
===========================

이제 우리는 대부분 파악할 수있을 것입니다
우리의 응용 프로그램을 사용해야합니다 적절한 URL. 에 근거
우리는 전에 본 UX 와이어 프레임, 당신은 우리가 것이다 것을주의했다
데이터의 1 주일 분을 원한다.이 퀴즈를 위해과를 위해
나는 나중에 당신을 보여줄 것입니다 코드 예제는 우리가하고있는
있는 마운틴 뷰의 우편 번호를 사용하는 것
어느 우편 번호, 도시 이름 또는 위도, 경도를 지정하는
좌표. 그런 다음 서버에서 형식은 JSON 형식으로되고 싶어
그리고 우리는 단위가 미터법으로보고 싶어요.하지만 우리의 UI는 의지
섭씨 또는 화씨를 표시 할 수있다
사용자의 취향에 기초하고 있으며, 우리는 그냥 있어요
변환 우리 자신합니다. URL을 입력 해주세요
그것은 아래 상자에 이러한 요구 사항을 충족


05 - 우리가 원하는 쿼리를 찾아
===========================

마운틴 뷰의 우편 번호 94043의 경우, 이것은 쿼리가 어떻게 될지이다
처럼 보인다.우리는 JSON 형식, 온도 단위로 있으면 모드를 설정
미터법에 있으면 카운트 param가 7 일과
예측 데이터. 그러면이 URL을 봐 것이고, 우리의 응용 프로그램에서 사용


06 - 기상 데이터를 요청하는 HTTP 요청
==================================

내 오픈 일기도에서 데이터를 가져 오는
응용 프로그램은 먼저 우리는 HTTP 요청을 할 필요가있다
우리는 이전에 결정한 URL API입니다.그럼 우리
얻기 위해 입력 스트림로부터의 응답을 읽어야
JSON 문자열. 그것은 아직 분석되지 않지만, 우리는 걱정입니까
약 그런. 그럼 우리는 연결을 절단하여 정리
임의의 입력 스트림을 닫습니다. 우리는 또한 모든 오류를 기록 할
우리는 잡는다.그것은 네트워킹 보일러 플레이트 코드의 많은이므로,
우리는 코드 조각을 제공하고 왔습니다
그것은 이러한 단계를 처리합니다. 링크를 참조하십시오
다음 GitHub의 요지. 당신이 촬영 한 후
계속하려면이 상자를 선택하여 그것을 봐.


07 - HTTP 요청
==================

샘플 코드에서는 알 수 있습니다
우리는 HTTP URL 연결을 만들 수 있습니다.로
를 통해 데이터를 송수신하기위한 HTTP를 사용하여
네트워크는 우리는 Android에서 2 개의 클라이언트가있다.
HTTP URL을 연결 클래스, 및
얼룩덜룩 HTTP 클라이언트 클래스. 두 옵션을 모두 지원
HTTPS 스트리밍 업로드 및 다운로드 설정 가능한 시간 초과
IPB 6과 연결 풀링. 추천
HTTP URL을 Connection 클래스는 일반적인 목적과 빛이라
체중, 그것은의 요구에 맞게 최적화되어있는
대부분의 Android 응용 프로그램입니다.연결에 대한 자세한 내용은
네트워크 다음 교육 안내 및 블로그 게시물의 링크를 참조하십시오. 08 - Logcat
===========

당신은 우리의 샘플 코드도 볼 수 있습니다
오류 메시지를 기록 log.e 전화 라인을 가지고있다. 과 동시에
adb 명령 줄 도구 장치가 플러그와
에서 디버깅을보기 위하여는 adb logcat을 입력 할 수 있습니다
오류 메시지가 logcat에 인쇄되어있는 것.
logcat 옵션에 대한 자세한 내용은 링크를 참조하십시오.
다음에. 로그를 표시하는 또 다른 방법은 사용하는 것입니다
Android 스튜디오. 당신은 화면의 Android 버튼을 클릭하면
그것은 Android 장치 모니터를 시작합니다.어떻게 포함
그래는 앞서 언급 한 DDMS 툴. 다음을 클릭하십시오
장치는 당신이 여기에 우리의 애플 리케이션임을 알 수 있습니다
실행중인 프로세스. 당신이 LogCat 탭을 클릭하면
여기에 당신의 이러한 모든 로그 메시지, 무엇을하는
우리는 ADB logcat에서 보았다. 지금 로그를 보려고하는
그 중 하나의 방법으로 자신. 당신이 모두를 할 경우,
당신은 브라우니 점을 얻는다.계속하려면이 상자를 선택하십시오.


09 - Android에서 로깅
=======================

안드로이드에 메시지를 기록 할 때 다음과 같은 것들이 필요
그것은 때 표시되어야 할 것인가 로그 수준을 결정한다.
자세한 로깅을 제외하고 당신의 응용 프로그램에 컴파일해서는 없습니다
개발 중. 디버그 로그로 컴파일되어 있지만, 그들은 제거하는
실행 시간 초과.오류, 경고 및 정보 로그입니다
모든 유지. 그리고 이것은 어떤 로깅 API의 외모입니다
처럼. 첫 번째 매개 변수는있다 로구타구 한
당신은 로그 메시지를 확인하고 원하는 모든 문자열이어야합니다.
이것은 로그 태그를 정의하는 것이 좋습니다
당신의 클래스의 상수. 일반적으로 그것은 당신의 클래스의 이름입니다
또는 응용 프로그램. 두 번째 매개 변수는 실제 로그입니다
메시지.우리는 다시 모니터에 가면, 우리는 그것을 볼 수 있습니다
이것은 로구타구 라인이며, 이것은 어디에
로그 메시지가있다. 당신이 드롭 다운을 클릭하면
여기에서는 로그 수준에 따라 로그를 필터링 할 수 있습니다. 예를 들어
당신은 모든 오류 메시지를 보려면 오류를 클릭 할 수 있습니다.당신은 경고에 ​​클릭하면 모든 경고가 표시됩니다
메시지뿐만 아니라 그것보다 어려운 것. 더
같은 다른 수준을 위해 간다. 그리고 중복 수단 일
당신은 모든 로그 수준에서 모든 로그를 볼 수 있습니다.
PROTIP로, 당신은 당신을 위해 로그 스팸을 방지해야하며,
다른 개발자를 위해.로그 버퍼가 가득 중요했습니다
당신이 정말로 확인해야 오류 메시지 중 하나 의지의 역할
로그 또는 그것은 중요하지 않다 로그 메시지의 바다에서 길입니다.


10 - 네트워크 전화
=================

멋지다.이제 우리는 우리가 사용할 수 있음을 알고있다
우리의 응용 프로그램을 디버깅하기 위해 로그인 우리는하고 돌아거야
여기에서는이 네트워크의 코드 조각과 드롭
실제 기상 데이터를 조회하기 위해 태양 광 응용 프로그램. 오픈
메인 activity.java 프로젝트를 백업합니다. 이 클래스에서는,
플레이스 홀더 내의 플레이스 홀더 조각 클래스로 스크롤
위의 조각 클래스에서는 뷰 메소드를 작성하고 아래로 스크롤
로 가서 여기에 네트워크 코드 조각을 추가합니다.
당신이 그것을 필요로 할 때 그녀의 공백을 얻으려면 다시 아래에 붙여 넣습니다.당신이 사용할 필요가 있을지도 모릅니다
이러한 자동 가져 오기 옵션 또는 수입을 추가
수동으로. 다음 단계를 참조하십시오. 당신이 실행하면
응용 프로그램은 당신이 충돌하고있는 표시됩니다. 로그를 사용하십시오
유죄 오차를 파악하는 고양이
충돌을 일으킨 범인. 우리는을 위해 그것을 상정하고있다
이 퀴즈 질문입니다.당신이 실행하는 장치를 사용하는
벌집 이후. 필요에 따라 에뮬레이터를 사용하십시오.


11 - 충돌 솔루션의 원인
===================================

귀하의 휴대 전화에서 실행하려면 Apple 충돌
왜냐하면 네트워크의 메인 스레드의 예외를 얻었다. 우리가 찾았습니다.우리의 컴퓨터에 우리 장비를 연결하여 답변과
오류에 대한 Android 장치 모니터를 체크한다. 당신은 할 수있다
이것이 우리의 패키지 이름과이 것을 여기서 볼
우리의 프로세스 ID이다. 당신이를 위해 로그를 검색하는 경우
프로세스 ID는 다음 우리의 오류가 표시됩니다. 이것은 결국 트리거이다
메인 스레드 예외의 네트워크를 통해.당신이 관심이 있다면
우리의 코드의 어떤 행에 같이 실제로 발생한
이것은 당신이 스택 추적을 아래로 스크롤 할 수 있습니다
자세히보기. 이것은 우리의 프레임 워크 코드
정말 닿는 장소 생략하고 여기에 할 수 있습니다 우리의
응용 프로그램. 그것은 onCreateView 방법에있어서, 플레이스 홀더 조각 클래스이다. 과
너무 라인 116 메인 activity.java 파일에서 일어난다
우리는 코드로 돌아 가면 그 라인에 당신은 그것을 볼 수 있습니다 urlConnection.connect
실제로 오류의 원인이 된, 우리는 주 스레드에서 그것을 할 수 없습니다.


12 - 백그라운드 스레드 VS 메인 스레드
=====================================

우리는 프레임 워크가 우리를 원치 않는 것을 말할 때
메인 스레드에서 네트워크 작업을 수행하려면 어떤
메인 스레드가 있나요? 이 경영하는 자, Android 어플리케이션
주 스레드의 기본은 또한 UI 스레드로 불린다.이것은 모든 사용자 입력을 처리하고 및
그런 화면 그리기 등의 출력. 따라서 우리가 원하는
그렇지 않으면 여기에 URI를 모든 시간이 걸리는 작업을 피하기 위해
망가하려고하고있다. 대신 백그라운드 작업자를 킥오프
당신은 어떤 장기 실행 할 필요가있는 경우 스레드
작품.이것은 비트 맵을 해독하는 네트워크 호출을 할 수 포함 또는
읽기 데이터베이스에서 쓰기. 예. 그래서 어떻게 든
우리가 떠날 네트워크 코드를 이동해야
메인 스레드.하지만 어떻게 우리가하려고하는
그? 거기에 몇 가지 옵션이 있는데, 그럼 살펴 보자
단순화 Android 클래스의 이름을 위해
따라서 백그라운드 스레드의 생성 및 UI 스레드 동기화,
배경 작업의 결과는 위 돌아올 것이다
메인 스레드 이후 우리는 우리를 업데이트하기 위해 그것을 사용할 수 있습니다
UI.온라인 검색과이 질문에 대한 답변을 찾을
그 상자에 클래스 이름을 입력하십시오. 여기에 몇 가지
당신을위한 조언. 당신은 지금까지 어떻게 발생할 경우
Android에서 무언가를하는 당신은 정상에 그것을 찾을 수 없습니다
당신은 stackoverflow.com을 확인하려고 할 수 있습니다 개발자 사이트. 그것은 문제 다
많은 Android 개발자는 귀중한 자원으로 사용하면 대답 사이트.
그래서 기회는 누군가가 가지고있는 가능성이있다
이미 당신이 가지고있는 유사한 질문을했다.


13 - 백그라운드 스레드 VS 메인 스레드
=====================================

당신은 비동기 작업에 응답 할 경우, 당신은 맞습니다.우리는 대답 비동기 작업을 선택한 이유를 이해하기 위해,
우리는 개발자 문서를 확인할 수 있습니다. 이 API에서
우리는 스크롤 할 수 있으며, 프로세스와 스레드 가이드
노동자는 섹션 스레드. 곧, 당신이 따라하고 싶은 경우
에 따라 링크를 아래에 포함되어 있습니다.즉, 예를 들어, 고
당신이 네트워크에서 이미지를 다운로드하려면
다음 URL로하고 업데이트 할
UI는이 비트 맵이 표시되도록. 그런데, 작성
이미지를 다운로드하기 위해 자신의 스레드가
유효한 옵션이 많은 오버 헤드가 있습니다
당신은 응용 프로그램을 실제로 스레드로부터 제작에 취급한다.후
당신은 당신의 이미지를 다운로드하고 당신이 직접 업데이트 할 수 없습니다
백그라운드 스레드에서 UI. 그러나 Android 몇 가지를 가지고
에 UI를 조작하는 코드를 실행하기위한 옵션
다른 스레드에서 실행. 이 예에서는 또 다른
실행 가능한 백에 비트 맵의​​ 결과를 얻기 위하여 창조되는
이미지 뷰를 업데이트하기위한 메인 스레드.이 솔루션
당신은 2 관리해야하기 때문에 조금 귀찮습니다
여기에 란나부루. 추상 떨어져이 복잡성 때문에, 우리는 사용 할 수 있습니다
그 후 비동기 작업은 비동기 적으로 킥오프
작업. 예를 들어, 누군가가 버튼을 클릭하면 당신
그냥 작업을 초기화하고 당신이 실행하는 호출 할 수 있습니다
게다가, 그 후 필요로하는 모든 매개 변수를 전달합니다.당신은 비동기 클래스를 확장 할 때,이 점에 유의하십시오
당신이 지정할 필요가 제네릭 의약품의 커플. 처음에는
관광에 전달되는 유형
배경 방법. 그래서, 당신은이 이미지의 URL로 전달하려는 경우
그것은 백그라운드를하고 여기에서 다음 지정된 문자열이다
당신은 문자열 매개 변수를 가져옵니다.또 하나는 용입니다
당신이 진행을 취득 할 때 가져옵니다 객체의 유형
작업으로 업데이트가 실행됩니다. 우리는 그 여기에서 사용하지 않는
그래서 보이드 것을 지정해도 괜찮습니다.그리고 세 번째 유형은 결과 유형입니다
우리는 onPostExecute 메소드를 통해 메인 스레드에 다시 전송됩니다 것을


14 - AsyncTask를위한 어떤 스레드
===============================

AsyncTask의 주요 이점은 당신이 얻을 수 있습니다
당신의 앱 로직에 집중하기 위해 당신은 무엇을 할 필요가 있는가?
백그라운드 스레드에서 당신은 때 실행하는 데 필요한 것
그것은 다시 메인 스레드에 온다.당신이 할 필요가 없습니다
스레드와 핸들러에 대한 자세한 신경. 메서드
나는 당신을 나타낸 것이 유일한 밖에 호출 구현할 필요가있다.
onPostExecute는 옵션뿐만 아니라 몇 가지 다른 방법이다. 각각에 대해
방법은 그것이 메인 또는 백그라운드 스레드 여부 가르쳐주세요.각 하나가 올바른 얻을 확률은 50 % 또는 100 %를 가지고
당신이 실제로 Java 문서를 확인하고 가기 때문에 지금 그것을 할 줄 휙.


15 - AsyncTask를위한 어떤 스레드
===============================

비동기 작업 문서, 우리는 할 수
에 대해 말하고 섹션으로 스크롤
보호 된 메서드. 여기에서는 그 다른 방법을 참조하십시오.
위의 대 UI 스레드에서 호출되는
백그라운드 스레드.또한 어떤 정보가 포함되어 있습니다
주문이 방법으로 호출됩니다. 에 대한 상대
밖에 호출 방법. 예를 들어, onPreExecute은 위의 호출
밖에 호출 전에 UI 스레드. 그 정보에 이렇게
이제 우리는 퀴즈의 정답을 가져올 수 있습니다. 로
우리는 이전에 언급 한 onPreExecute는 주 스레드에서 발생합니다. 과
여기에서는 모든 설정 작업을 수행 할 수 있습니다. 다음에 밖에 호출이 일어난다
백그라운드 스레드에서.이것이 실행되고있는 동안 당신이 실제로 수 있습니다
당신이 원하는대로 여러 번 publishProgress를 호출
당신은 UI에 정보를 전달할 수 있습니다. 그 이니까,
그 후 특정 사용자에게 전달 업데이트 할 수 있습니다
일의 비율이 열린다. 이것이 불려 갈 때마다.
이것은 몇 가지 정보를 onProgressUpdate 트리거.그 후
당신은 내 선적 표시기를 표시 할 수 있습니다
뭔가의 10 %는 50 %가 완료되고 실시 말하는 당신의 UI는 100 %가 발생. 그리고 모든이
주 스레드에서 발생합니다. 그 후, 1 회 모두 완료
백그라운드 스레드는 그것은 onPostExecute를 호출
메인 스레드에서 결과.


16 - AsyncTask로 이동
======================

것은 우리 만 개방함으로써 배운 것을 적용 해 봅시다
우리의 프로젝트 MainActivity.java 파일. 우리는 걸릴 거예요
이 네트워크 코드 조각하고 그것을 위로 이동
그것은 자신의 AsyncTask이므로, 그것은 백그라운드에서 실행됩니다
스레드. 작업 내에서 정의하려고하고있다
이 조각 클래스. 하지만 실제로지만, 그러고 보니
아직 PlaceholderFragment라고. 그럼 조금 일을하자
그것을 진짜 이름을 제공함으로써 지금 리팩토링. 그러면 부릅시다
그것이 ForecastFragment.그리고 당신은 그것을 업데이트 할 수 있습니다
다른 적절한 장소에서도 마찬가지. 우리는 또한 캔
이동 ForecastFragment 그렇게 자신의 파일에
MainActivity는 너무 길고 지루한 얻을 수 없습니다. 중
ForecastFragment 우리는 새로운 내부 클래스를 정의해야합니다
AsyncTask에서 연장 FetchWeatherTask라고. 그리고 당신
여기에 네트워크 코드 조각을 이동할 수 있습니다.먼저하세요
변경 당신의 응용 프로그램을 실행하고 그것은해야
이런 걸 봐. 실제로 그렇지에는 차이가 없습니다
지금 충돌하지 않는다. 다음 단계는 실행하는 코드를 추가합니다
작업. 그리고 이후 단원에서 우리는 JSON 파싱 및 업데이트를하는
UI. 그러나 다른 한편으로 당신의 코드에 이러한 초기의 변경을 실시한다.17 - AsyncTask로 이동
======================

예측 조각의 솔루션을 위해 우리
AsyncTask를 확장 FetchWeather / 작업을 구현했습니다. 제네릭
우리는 무효가됩니다 사용하고 있으며, 이것은 지금까지 괜찮습니다. 다음에 밖에 호출에
이 방법 우리는 우리의 네트워킹 코드 조각을 복사
여기에. 그것은 [들리지 않음을 제외하고는 동일합니다
특정 우리는 null를 돌려 케이스 대신
null 것으로 예측 JSON 문자열을 설정한다.이전 코드는 우리가 기대 뷰를 작성하고 있었다
급증하면 뷰를 돌려줍니다. 그래서 그것이 가지고있는 것이 중요합니다
코드의 나머지 부분에. 이 있었다고해도,
네트워크 코드의 오류. 이제 네트워크 코드가 켜져 있는지
동기화 작업이 가운데 후에 오는 것은 정말 없습니다
주어진 배경 방법. 그래서 그냥 빨리 구제하기 괜찮아요
언제든지 오류가 있습니다.또한 우리의 로그 메시지를 위해 그것을 알고있다
우리는 로구타구 상수를 정의했습니다. 이 작업의 상단에.
이 로구타구는 FetchWeatherTask.class의 이름이되도록 정의되어있다. 더
우리 대신이 구문을 사용한 이유
문자열 FetchWeatherTask를 선언, 그것은 이유
우리는이 두 가지 동기가되고 싶어요. 혹시 이름을 변경하는 경우
당신도 여기를 갱신하지 않으면 클래스가 그것은 예외를 throw합니다. 18 - 새로 고침 버튼을 추가합니다.
=======================

우리는 이전에 언급했듯이, 당신은 여전히​​ 가짜를보고하고있다
응용 프로그램의 데이터입니다.우리는에 코드를 추가해야합니다
실제로 주님의 백그라운드 작업을 킥오프
스레드. 우리 경우는 디버깅을 위해, 그것은 좋은 것이다
작업 우리가 원했던 언제든지 실행할 수 있습니다
어떻게 든 UI​​와 상호 작용한다. 그래서, 우리는 추가거야
디버깅을위한 재생 메뉴 옵션. 경고하지만,
이 메뉴 옵션은 최종 애플리케이션에서 이동해야하는 것이 아닙니다.19 - AsyncTask가 최적이 아닌 이유
=================================

계속하기 전에, 나는해야
여기에 점프. 캐서린은 이미하게 말하고있다
새로 고침 단추는 디버그 전용이며,
그럼, 왜 봐 봅시다. 실제 삶에서 당신
항상 업데이트 버튼을 제거하기 위해 받아야한다
안드로이드에서. 좋은 앱이 작동합니다
당신도 위해 요청해야 전에 당신이 원하는 당신을주고, 좋은 집사 님
그것.[저장] 버튼과 같은 많은 그것은 유물이다
지나간 시대. 즉, 그들을위한 최고의 든든한 안전 담요입니다
우리 모두가 플로피 디스크에서 자랐다. 능력을 가진
백그라운드 작업을 실행하거나 서버에서 직접 메시지를 보낼
우리의 응용 프로그램에 사용자를 강제 할 이유는 없잖아요
수동으로 새로 고침을 공격한다. 그러나 앱이 최신 것이다
와 클라우드와 동기화가 주어져야한다.그러나 같은
우리는 인쇄 선처럼 그것은 그래서 이것은 디버깅입니다 말했다
이 특정 목적을 위해 수용해야합니다. 그럼 또 봐 보자
다음의 잠재적 인 문제이다 우리의 백그라운드 스레드 모델?


20 - AsyncTask가 최적이 아닌 이유
=================================

그런데, 전송은 UI 스레드에서 일어나고 있지 않지만,
그것은 나쁜 것은 아닙니다. 실제로, 그것은 그건 좋은 일이다
UI 스레드에서 일어나고 있지 않다.그래서 문제는 없습니다
어느 쪽이든. 데이터 전송은 가장 현대적인 스마트 폰의 중요한 부분이다
응용 프로그램은 그 결과는 문제가 아니다. 진짜 문제는 것입니다
전송은 그 생애 묶여있는 스레드에서 일어나고있는
명시 적으로이 경우의 UI 구성 요소 활동. 이렇게
활성 화면 회전과 같은 것에 의해 종료 된 경우
전송을 종료합니다.21 - 동기화하기위한 더 나은 방법
========================

그것이 활동에 생성되는 것이기 때문에, 그것은 할 수 있습니다
또 다른 휴대 전화를 회전 시키도록 간단하게 종료
오리엔테이션. 그래서 유일한 지금까지 그 작업에 사용할 필요가 있습니다
라이프 사이클은 호스트의 활동에 묶여 있다고 기대되는
유일한 1 초 또는 2 초 동안 실행한다.모바일에서는
그것이 있어도 대부분의 사소한 네트워크를 전제하고 안됩니다
액세스 빨리 일어날하려고하고있다. 그래서 더 나은 접근
서비스를 이용하기위한 것이다. 응용 프로그램 구성 요소 없음
가능성이 낮은 UI
중단. 아마도 부정확 한 반복 알람을 사용하여 일정.
더 나은, Android는 특별한 솔루션의 노하우를 가지고
비동기 어댑터로.그리고 특히 일정에 설계되어 있습니다
당신의 배경 데이터는 가능한 한 효율적으로 동기화합니다. 더
아직 Google 클라우드 메시징을 사용하게된다. 이것은 수 있습니다
당신은 위의 변경 당신의 비동기 어댑터에 통지
서버 측. 그래서 유일한 지금까지 네트워크 요청을 시작하고있다
안드로이드에서 당신이 무언가가 있다고 알고있는 경우
서버에서 업데이트된다.지금 우리는 집중되고있다
우리의 응용 프로그램을 작동하려면, 그것은 전경에있을 때. 그러나 우리는 돌아갑니다
눈에 보이지 않게 업데이트하기 위해 이러한 방식을보고
배경에서 안드로이드 조금
나중에. 지금 새로 고침 버튼과 새로운 스레드에 유의하십시오
우리는 응용 프로그램의 나머지 부분을 연결하면서 해결책은 단순히 자리 표시 자입니다.22 - 메뉴 버튼
=================

덕분 도우이 점을 염두에두고는 추가하자
우리의 응용 프로그램에 대한 재생 메뉴 버튼. 일시을 위해
목적이 유일하지만 그렇지 않으면 도우는 성난 것이다
우리. Android에서는 메뉴 옵션은 XML로 정의되어 있습니다
그리고 그들은 조각에 선언 할 수 있습니까?
활동.조각 또는 활성이 작성되면, 그것은
에서 실제 메뉴 항목이 XML을 팽창
응용 프로그램. 당신은 액션 버튼이있는 것을 알 수 있습니다
작업 표시 줄에 표시되는 메뉴 항목은 이것이다,
그런이 검색 메뉴 항목으로. 이 공간은 예약되어 있습니다
안드로이드에서 가장 유명한 액션을 위해.그럼 아무거나
아무개는 오버플로 메뉴에 덜 중요한 폭포
3 개의 점에서이 버튼을 탭합니다. 이 메뉴
항목은 가장 자주 자주 최소한으로 사용로부터 주문 된
사용. 그리고 더 스크린의 열매를 가지고있는 대형 장치에
부동산, 당신은이 메뉴 항목의 일부 수 있도록 지정할 수 있습니다
방이 있는지 실제로 작업 표시 줄에 들어간다.만약
당신이 Resources 폴더에 우리의 프로젝트로 돌아 가기
메뉴 폴더가 있고, RES라고되어 있으면
그 안쪽에는 main.xml 파일이 있습니다. 당신이 그것을 열 때
당신은 메뉴의 레이아웃 XML을 참조하십시오 도가 있음
설정에 정의 된 하나의 메뉴 옵션. 그것은 나타나는 것은 아닙니다
작업 표시 줄에 조치로서, 그것은 의미
오버 플로우 메뉴입니다. 당신은 이것을 확인할 수 있습니다
휴대 전화에 응용 프로그램을 체크한다.순서를 정의하려면
메뉴 항목에서 그냥 이것에 여러 항목을 추가 할 수 있습니다
XML 파일 및 그 순서대로 표시됩니다
응용 프로그램에서. 당신은 그러나 순서가 마음에 들지 않으면 및
당신이 명시 적으로 설정하고 싶은 경우, 당신은 지정할 수 있습니다
카테고리 값의 순이었다. 지금은 그것을 100과 세트,
설정 메뉴는 하단에되도록
우리는 우리의 응용 프로그램에서 정의하는 다른 모든 메뉴 옵션.[설정] 아래에 표시됩니다 만 메뉴 옵션
메뉴는 도움말 메뉴이다. 자세한 내용은 링크를 참조하십시오.


23 - 새로 고침 버튼
===================

페치 날씨 작업이 조각이기 때문에
그 작업을 트리거하는 메뉴 옵션은 단편 내에 있어야합니다
도. 우리가 새로운 메뉴 레이아웃을 생성해야합니다 의미
조각을 위해, 우리는 그것을 forecastfragment.xml 부르기로합니다. 파일 의지
자원 디렉토리 아래에 메뉴 폴더에 살고 있습니다. 내부
그 파일이 우리가 재생을위한 새로운 메뉴 옵션을 선언 것이라고
그것을이 메뉴 항목의 ID를 준다. 우리는 또한 정의해야합니다
이 단어의 문자열 레이블, 최신 정보로 업데이트. 우리는이 것을 가지고있다
이만큼 메뉴 XML을 만드는 한 번 단계
이 연습에서 파일의 변경.당신이 컴파일하고 실행하는 경우
응용 프로그램은 눈에 보이는 변화는 없을 것이다. 그것은 표시되지 않습니다
우리는 메뉴를 부풀려 않은 장치의 최대 사이다 때문에
아이템. 그것을 팽창시키는 것은 부호화 시험 후가됩니다
이것. 메뉴는 main.xml과 같이 구현되어 있는지를 본다
예. 추가 팁 메뉴 훈련 지침을 참조하십시오.
다음에. 설정이 완료되면 당신은 여기에서이 상자를 클릭 할 수 있습니다.


24 - 새로 고침 버튼
===================

여기에 최신 정보로 업데이트 버튼 코드
forecastfragment 메뉴 XML 파일입니다. 우리가하고 싶은
오버 플로우 메뉴에 표시되기 때문에 우리는 showAsAction 설정
결코로.우리는 또한 문자열을 선언합니다. 당신은 할 수있다
이것, strings.xml 파일 여기서 문자열을 검색
이다의 가치 폴더에 위치합니다
RES 폴더. 당신의 strings.xml 파일을 검색 할 수 있습니다
다른 언어로 번역. 이것은 추가 값 폴더를 추가합니다
RES 아래. 예를 들어, 당신이 가지고있는 것이다
스페인어, 프랑스어 값 -FR 값 -ES ,. 과
그 값의 각 폴더에 당신
것입니다 strings.xml 파일을 가지고있는 것이다
그 언어의 지역화 된 문자열이 포함되어있다.
번역처럼 돈이 없기 때문에
직업적인 끝은 문자열을 표시 할 수 있습니다
당신이 가짜 = 번역 가능한 사용하여 변환 할 필요가 없습니다.예를 들어,
그것은 적절한 이름이다 않거나 그것이 이번 같은 디버깅을 위해서라면
그들이이 문자열을 생략 할 수 있습니다 번역자에게 보여줄 수 있습니다


25 - 업데이트 버튼 동작
============================

이제 우리는 메뉴 XML을 가지고 있는지에 코드를 추가
조각은 그것을 팽창시킨다. 당신은 플레이스 홀더를 남길 수 있습니다
새로 고침 버튼이 선택된 경우.이게 무슨 그것이 필요하다
설정이 완료되면보세요. 당신은 거기에 최신 정보로 업데이트 메뉴 항목이 표시 될 것입니다
그러나 그것을 누르면 아무것도하지 않습니다. 즉, 지금까지 괜찮습니다.
필요에 따라 참고로 mainactivity.java를 볼 수 있습니다. 당신이 취득하는 경우
스택과 대답하려고하면 메뉴 항목이 표시됩니다 표시되지 않은
먼저이 질문 : 당신이 호출 할 필요가 무엇을 해야할지 조각 방법
그것은 볼 수있는 메뉴 옵션을 가지고 있는지보고하기 위해?


26 - 업데이트 버튼 동작
============================

해결책은 우리가 호출 할 필요가있다이다
Fragment.setHasOptionsMenu (참). 그렇게 우리는 요
적절한 옵션 메뉴의 콜백을 얻을
조각의 메소드, 우리는 할 수 있도록
메뉴를 부풀려 때 메뉴 항목
선택되어있다. 그리고 이것은 어디 조각이다
메뉴를 팽창시킨다. 그리고, 그 전부터 기억하십시오
ForecastFragment 클래스, 우리는 공공의 빈 생성자를 가지고 있으며,
우리는 또한 onCreateView을 덮어? 또한 여기에 fetchWeatherTask을 정의합니다.지금, 우리는 추가 조각의 수명을 무시 죽음거야
의 onCreate라는 사이클 법. 이것은 어디 조각이다
생성되고 이것은의 onCreate보기 전에 발생
UI가 초기화되는 장소이다 방법. 그래서 중
의 onCreate, 우리는 진정한이면 setHasOptionsMenu를 호출하는거야
우리는 이러한 방법을 위해 허리를 호출하고 싶은 것을 보여주고있다.onCreateOptionsMenu가 호출되면 우리는 메뉴를 팽창시키는거야
우리는 이전라는 예측 조각을 정의 된 레이아웃. 우리는 또한 해요
메뉴 항목이 선택 될 때 통지를 받는다. 때 메뉴 항목에
ID 액션 새로 고침이 호출되면 우리는거야
지금 true를 반환한다.우리는 가야겠다
이후에보다 상세하게 활동 상과 단편 라이프 사이클 메소드
수업은 당신이 원한다면 당신은 지금 아래 링크의 문서를 읽을 수 있습니다.


27 - AsyncTask를 실행합니다
======================

지금 코드를 변경해야 할 때 새로 고침 메뉴 항목
선택된 그것은 FetchWeatherTask을 실행한다. 그러나 위에 만요.때 당신을
그것은 실제로 충돌 새로 고침 버튼을 누릅니다. 왜하지 마십시오
이 원인을 오류 표시하려면 로그를 확인하십시오.


28 - AsyncTask를 실행합니다
======================

예측 조각 클래스에서는 수정
onOptionsItemSelected 방법. 업데이트 메뉴 항목이 선택되면,
우리는 새로운 FetchWeatherTask을 만들고 우리가 부르고
그에서 실행됩니다.통화는 더 이상 없지만
그것은 AsyncTask 그래서 UI 스레드를 차단
응용 프로그램은 여전히​​ 충돌합니다. 우리는 로그를 확인하면
우리는 응용 프로그램이 충돌 한 것을 참조하십시오. 그러나 이번에는
보안 식으로. 그것은 권한이 거부되었다고 말하면
당신은 인터넷 권한이 부족하거나하지 여부를 묻는다.그리고 사실,
우리는 인터넷 권한이 부족하기 때문에, 우리는 그것을 요​​구해야합니다.


29 - 권한
================

그러면 각 응용 프로그램 APK가 설치되어있는 액세스 권한에 대해 이야기하자,
그것은 자신의 독특한 Linux 사용자 ID가 부여이다. 그리고 각각의
응용 프로그램은 Android 가상 머신에서 인스턴스에서 실행됩니다.
[SOUND] 그 결과, 각 응용 프로그램은 완전히 모래 박스입니다.[BLANK_AUDIO]
파일의 프로세스 및 기타 리소스에 액세스 할 수 없습니다
다른 응용 프로그램에. 이 샌드 박스 접근에 사용되는
기본적으로 앱이 민감 액세스 할 수 있는지 확인하십시오
데이터 또는 부정적인 영향을 다른 영향을 미칠 수있는 작업을 수행 할
응용 프로그램, OS 또는 사용자. 액세스의 종류
인터넷 사용자의 위치를​​ 검색하거나 읽거나 변경
연락처 데이터베이스.대신 사용자 각각에게 묻는다
앱이 당신 민감 뭔가에 액세스하려고 할 시간
그것은 매니페스트에서 당신의 응용 프로그램에 필요한 권한을 선언했다.
당신은 허가의 모든 목록을 얻을 수 있습니다
당신의 앱은 Android 개발자 사이트에서 여기에 필요할 수 있습니다.그럼, 왜 그냥 모든 권한을 요구하지 않는 경우
다시 그것을 걱정하지 마십시오? 그런데, 때 사용자가 설치
당신의 앱들은 모두 나열됩니다. 이 대화에서 맞이
당신이 더 많은 것과 함께 요구되어왔다 권한
사용자 친화적 인 설명.아무것도이 앱이 해커에 의해 만들어 졌다고 말하는 것
내가 중 명확한 우리집 롭을 내 데이터를 훔치는 싶은 사람
은행 계좌 등을 내 누드 사진을 찍고 공유
위의 모든 권한 액세스를 원해 날씨 앱
장치. 가장 좋은 방법은 권한의 절대 최소값을 요구하는 것입니다.당신이 새로운 권한을 요청할 필요가있을 때마다 그것을 받아
기타가 있으면 중지 고려해야 할 플래그로
같은 목표를 달성 할 가능성이 있습니다 선택. 예를 들어, AN을 사용하는
의도는 직접 오히려 카메라에 액세스하는 것보다 카메라 앱을 실행합니다.그럼 우리는과 당신의 데이터를 공유하는 방법을 살펴 보자
다리를 만들기위한 의도 및 콘텐츠 공급자를 사용하여 다른 응용 프로그램
이 앱 sandboxs 사이. 당신은 그들을 선언하여 사용할 수 있습니다
이러한 경우에 허용에
마찬가지로, 기밀 정보에 대한 액세스를 제한합니다.


30 - 매니페스트에 권한
================================

탐구하는 시간을 가지고
developers.android.com의 보안 섹션. 이들 중 하나
다음 활동에만 할 수 있습니다
매니페스트에서 사용 허가를 선언 한 후?


31 - 매니페스트에 권한
================================

선언하면서 수수료가 사용하는 데 필요한
카메라, 전화를 걸거나 연락처 정보 접근한다. 당신
시스템 응용 프로그램을 사용하여이 것의 각각을 할 수 있습니다
중개로.카메라 어플, 다이얼러 및 연락처를 위해
응용 프로그램은 각각의 데이터를 제공하는 데 사용되는
사용자가 작업을 취소 할 수있는 기회를 가지고있는 요구
당신은 그들에게 너의 것을 거부하기 위해 런타임 기능을 제공 시작
액세스. 하지만 UI는 사용자의 현재 위치에 액세스 할 수
그것이 명시 적으로 사용자의 허가를 선언하는 경우.32 - 인터넷 권한을 추가
===============================

덕분 FREDO! 그래서 옛날처럼 우리는거야
허가를 받아야한다. 가서 변경
Android 매니페스트 파일은 인터넷 권한을 요구한다.
그리고 우리의 정확한 문자열 이름을 가르쳐
당신이 사용 허가. 응용 프로그램을 실행합니다
다시 그것은 충돌하지 않는 것을 보장한다.당신은 할 수있다
모두 네트워크 호출의 출력을 기록
당신이 다시 제대로 기상 데이터를 얻고 있는지 확인합니다. 33 - 인터넷 권한을 추가
===============================

대답은 android.permission.INTERNET입니다. 나는 지금 당신이 나타납니다
어디에서이 코드에 위치. 아래
메인 폴더는 Android Manifest.xml 파일을 엽니 다.
Android 매니페스트 파일에서 우리는 용도를 선언
허용 허용의 이름이있다. 우리
반환 된 데이터가 올바른지 확인하기
인쇄하기위한 상세한 로그 문을 추가
forecastJsonStr. 이것은 페치 날씨 작업이다.
우리는 그것이 로그에 나타날 때까지 일어나고있는 것을 확인할 수 있습니다. 이 예에서는 지금
명령 줄을 사용하는 것.내 경우에는 이들은 그 후 실시간 로그이며,
새로 고침을 치는 내가 여기에 기상 데이터를 참조하십시오. 자세한 로그 이것은 우리입니다
로구타구 날씨 작업을 페치. 여기에서 forecastJsonStr입니다,
이는 서버에서 모든 출력이있다.


34 - 우편 번호 Param
======================

좋은 일.いいぞ. 데이터를 안전하게 착탄 한
우리의 휴대 전화.하지만 난 그것에 대해 생각 실제로 한
대신 우리의 우편 번호를 하드 코딩 우리는 정말 생각합니다
수 있도록 우리의 태양 기차 앱 사용자처럼 [SOUND]
설정에서 자신의 위치를​​ 변경한다. 그럼 만들어 보자
그것은 입력으로 가지고있다하여 FetchWeatherTask보다 유연
우편 번호 매개 변수입니다.우리는 그것을하고있는 동안, 우리는해야
또한 리팩토링 약간을 할이 기회를 이용.
대신 서버의 쿼리 문자열을 연결하는
URL 우리가 구축하는 UriBuilder 클래스를 사용해야합니다
그 URL까지 우리는 기본 URL을 선언 할 수 있습니다
그 쿼리 PARAM의 각 쌍을 추가하고
PARAM은 그 위에 값. 이 게시물에 대한 PARAM을 포함
코드. JSON 형식 미터법 및 날짜 계산.이것은 요
지금까지 우리 있으면 미래에 그것을 쉽게하기
이용자가 이러한 옵션이 설정 가능하도록해야합니다.
당신은 URL이 제대로 구축되어 있는지 확인하려는 경우. 후
이 작업을 수행하려면, 당신은 그것을 밖으로 인쇄하기 위해 자세한 로깅을 사용할 수 있습니다.35 - 우편 번호 Param
======================

예측 단편은 우리는 변화하는
FetchWeatherTask, 우리는 전달할 수 있도록
우편 번호 매개 변수 우리는 그 작업을 수행했을 때.
당신이 점프하는이 클래스를 클릭 할 수 있습니다
어디 그것이 정의되고있는한지이 단축키를 사용할 수 있습니다.그리고 여기에서 당신은 우리가 알
인 것이 일반적인 입력 유형을 변경
문자열 만 호출 메소드는 문자열 params을받을 수 있도록.
이제 우리는 하나의 문자열 param로 전달되고,
params 중의 제로 번째의 위치를​​ 읽을 수있는
배열 그 우편 번호를 검색합니다. 우리가하고있는 것에 주목하십시오
여기에서는 UI 빌더를 사용하여 우리는 쿼리를 추가하고있다
매개 변수 하나씩.우리는 이러한 상수를 정의
쿼리 params를 여기에서 볼 수있는 것처럼. 과 값 때문에
우리는 또한 여기에 그들을 정의합니다. 당신이 상상할 수있는
미래에는 이러한 외부로 설정 될 수 있음을
이 클래스 것이 지금의 우리는 다만거야
여기에 그들을 정의합니다. 이 URI 있는지 확인하려면
잘 정의 된, 우리는 자세한 로그 명령을 추가
구축 된 URI를 인쇄한다.는 그것을 확인하자
우리가 실제로 추가 된 로그가 표시됩니다. 오버플로
메뉴 우리는 최신 고침을 누릅니다. 그럼 우리는 로그를 참조하십시오
우리의 UI를 가진 태그 FetchWeatherTask는 프린트. 그것은 말


36 - 희망의 JSON 속성을 식별
=====================================

우리가 구축 된 URL은 좋아 보인다과 JSON
서버에서 문자열도 좋을 것 같다. 하지만 아직
하나의 긴 문자열.는 더 신중하게보기 위하여 그것을보고하자
우리는 그 때 어떤 데이터를 추출해야합니다. 하기 위해
서버에서 돌아 오는 문자열의 의미 우리
JSON 포맷 또는 JSON의 prettifier 통해서 그것을 넣을 수 있습니다.
당신은 그 용어는 Google 경우 찾을 수있을 것입니다
이 1과 같은 유용한 도구입니다. 여기에 붙여 넣기
Web 쿼리의 결과입니다.그리고 다음 출력 포맷
우리는 우리에게 이러한 요소의 계층 구조를 보여준다. 지금 기준으로
당신은 선샤인 앱 위해 본 와이어 프레임, 당신이 할 수있는
우리는 추출 신경이 리프 노드의 어떤 들려?
우리는을 위해 부모 노드를 횡단해야합니다 비록
다음 화면에서 퀴즈의 목적은 우리 뿐이다
리프 노드를보고있다.다음, 당신의 선택하십시오
우리는 예측의 목록을 표시하기 위해해야​​합니다 속성


37 - 희망의 JSON 속성을 식별
=====================================

그리고 여기에 우리가 걱정 특성은 우리의 응용 프로그램에서 예상 목록을 표시합니다.


38 - 최대 온도를 분석
===========================

다음 단계를 위해 초점을 맞추고 연습을하자
이러한 속성 중 하나의 값을 추출하는 것에. 우리는하고있다
조금 다른이 연습을하는거야.당신은 이것을 구현합니다
Udacity 플랫폼으로. 그리고 우리는 그 사실을 확인할 수있을 것입니다
당신의 코드는 맞습니다. 이 비디오 후, 당신은 IDE가 표시됩니다
이런. 여기에 몇 가지 스타터 코드가 포함되어 및
다른 탭에서 여러 J 단위 테스트. 구체적으로는, 우리
만약 최대 온도를 얻기 위해이 기능을 구현하는
하루에.당신은 기상 JSON을 주어왔다
문자열 당신이 얻을 것이다처럼 포맷 된
오픈 날씨지도 서비스에서. 당신도
또한 우리는 걱정 일 인덱스를 받았다.
코드를 만지고 부담없이
Android 스튜디오 또는 독립적 인 개발 환경 이전에
당신이 여기에 당신의 대답을 붙여 넣습니다. 또는 사용할 수 있습니다
Udacity IDE. 어느 쪽이 당신에게 더 자연스러운 느낌.39 - 최대 온도를 분석
===========================

해결을 위해 우리는 목록의 배열을 찾는다.
리스트의 각 요소는 예측 1 일을 나타냅니다. 주어진
하루 인덱스 우리는 그런 온도 노드를 찾아
최고 온도. 그리고 그것은 코드가 어떻게 될지이다
처럼 보인다. 우리는 JSON에 JSON 문자열을 변경
오브젝트. 그럼 우리는 목록의 배열을 찾는다. 그 중
우리는 마음에 하루를 찾으십시오. 그럼 우리가보고
임시 노드에 대해.그리고 최고 온도를 구한다.


40 - JSON 파싱
=================

당신은 JSON 데이터를 요약 부하는 방법을 배우시면 꽤이다
정직은 PARS의 나머지 수 있도록하려면
우리에게 필요한 필드에 입력합니다. 이것은 위의 과정이 아니므
Java 또는 JSON은 우리가 구문 분석을 제공하는거야
다음 요점 코드. 그리고 이것은 무엇입니까
요점은 다음과 같습니다. 3 헬퍼 메소드가 있습니다.처음에는
날짜를 포맷하기 위하여. 둘째는 온도를 반올림위한 것입니다. 제 3
일기 예보의 배열에 forecastJsonStr를 돌기를위한 것입니다.
이러한 유용한 기능을 사용하기 위해 반입 날씨의 작업을 업데이트합니다. 과
배경 방법의 DO는 문자열 배열을 반환해야합니다
예측. 당신은 배열 있는지 확인하기 위해 출력을 기록 할 수 있습니다
맞다. 1 일 날씨 형식은 다음과 같습니다.41 - JSON 파싱
=================

우리는 FetchWeatherTask가 배열을 반환하고 싶다
문자열의 예측. 우리가해야하는 것을 의미
비동기 작업의 반환 형식을 변경합니다.
다음에 밖에 호출 법은 우리가 읽은 후에
입력 문자열에서 우리는이 코드를 실행한다.
우리는 헬퍼 메소드 getWeatherDataFromJson과 우리를 호출
forecastJson 문자열에 전달할뿐만 아니라,
예측 기간. 우리도 잡아
구문 분석에 문제가 있는지 모든 JSON 형식의 예외.우리
예측 데이터의 문자열 배열을 확인하고 싶었
맞다. 그래서 getWeatherDataFromJson 메소드에서 우리는 몇 가지를 추가했습니다
배열의 각 요소를 출력하는 명령문을 기록.


42 - 어댑터를 업데이트
=======================

로그에서, 우리는 적당한 원근법을 가지고 있다는 것을 알고있다
데이터와 우리가 원하는대로 적절한 형식으로
문자열의 배열. 그래서 궁극적으로 업데이트 할 때가왔다
UI.AsyncTasks이 데이터를 전달할 수있는 방법을 다시 생각해
메인 스레드에 백업한다. 당신이보기 위하여 Ctrl + O를 칠 수 있습니다
우리는 AsyncTask 덮어 쓸 수 있습니다 사용 가능한 메소드의 목록입니다. 만약
당신이 그들 중 하나를 클릭 그것은 사전에 입력됩니다
당신을위한 코드. 그 후, 당신은 새와 ArrayAdapter를 업데이트 할 수 있습니다
AsyncTask 의해 취득 된 데이터.힌트로서 당신
ForecastAdapter 전역 변수도 할 수 있습니다. 그러면 당신
FetchWeatherTask 내에서 액세스 할 수 있습니다. 이 있는지 확인하십시오
정적 클래스는 없습니다, 그렇지 않으면 당신은 할 수 없습니다
예측 조각에서 멤버 변수에 액세스합니다. 그럼 가서
컴파일 및 응용 프로그램을 구축한다.당신은 그것을 실행할 때와
당신은 주간 분가 나타날 것입니다 업데이트 버튼을 히트
해당 지역에 대한 기상 데이터. 그것이 작동하는 다음과 같은 수 있습니다
그렇지 않기 때문에 자세한 로그 글을 삭제
로그를 어지럽히고.당신은이에 임하고있다로
코드 지원되지 않는 연산 예외가 나타날 경우
당신이 가짜를 만들 때 확인하십시오
당신은 ArrayAdapter를 초기화 할 때, 당신이 합격 한 것을 데이터
문자열 목록이 아니라
배열. 당신은 명확하게 호출 할 수있는 방법
메소드 또는이 목록 컬렉션에 Add 메서드.43 - 어댑터를 업데이트
=======================

솔루션은 onPostExecute 메소드를 재정의하는 것입니다
AsyncTask의. 그리고 이것은 주로 작동합니다
스레드. 우리는 예측 결과의 문자열 배열을 받아
Do로부터의 반환 값으로왔다
상기 배경의 방법으로. 먼저 ForecastAdapter를 클리어
모든 전회 예상 항목. 그럼 우리가 간다
먼저 각각의 새로운 예측 항목 씩을 추가
ForecastAdapter 1. 이것은 결국 트리거합니다
업데이트 목록보기.당신은 벌집을 대상으로하는 경우에주의하십시오
위의 장치와 당신은 여기에서 addAll 메소드를 사용할 수 있으며,
그래서 그들을 하나씩 추가 할 필요가 없습니다. 당신은 한 번만를 추가하고 한 번 목록보기를 업데이트 할 수 있습니다.
당신이 최신 정보로 업데이트 충돌 후를위한 일기 예보가 표시됩니다
해당 지역은 다음 7 일.우리는 히트에도 불구하고
최신 정보 업데이트, 우리는 모든 세부 로그 문장이 인쇄되어있을 필요는 없습니다
여기에. 우리가 가지고 있기 때문에 우리는 더 이상 필요로하지 않는
우리의 코드는 현재의 UI를보고 올바른지 확인하는 방법.


44 - ArrayAdapter를위한 소스 코드
=================================

당신은 1 단원에서이 그림을 기억하고 있습니까? 어댑터
원시 데이터에 대한 참조를 가진다.라는 지시가
어떻게 각 목록 항목의 레이아웃을 구축한다. 이러한 레이아웃은 궁극적으로 만드는
그것은 여기에서 목록보기로. 그러나 무엇이 있으면 발생
이 데이터의 변경. 는 예를 들어, 넷째가 있다고하자
돈이라는 접촉. 어댑터 목록을 만드는 방법을 알고
돈의 아이템 레이아웃. 하지만 지금 목록보기가 오래되어
그것은 세 가지 항목이있다 때문이다.어떻게 든 우리는 어댑터가 필요합니다.
사물이 가지고있는리스트 뷰에 알리려면
변경. 그리고 우리를 위해 운 방법이 있습니다
adapter.notifyDatasetChanged () :라고. 이것은 연결되어있는 모든 관찰자에게 통지하고
따라서, 기본 어댑터 데이터는 가지고
변경. 그런 다음 목록보기 이입해야합니다
다시 그 아이. 그래서 어댑터를 요구
얼마나 많은 항목이 존재 하는가? 와 어댑터
4 응답합니다. 그 후,리스트 뷰 가서 가져
각각 개별적으로 그것은 화면을 꽉 찰 때까지.그리고 ListView 컨트롤이 가능하다는 것을 메소드를 통해서 다
모든 목록 항목을 가져옵니다. 그러나 이제
생각해야합니다. 어떻게 우리는 실제로리스트 뷰를 갱신했습니다
성공하여 우리 안의 코드 줄을 추가하지 않고
앱? 글쎄, 당신은 추가 할 때마다 선 어댑터 또는
그것은 내부적으로 notifyDataSetChanged를 호출 거기에서 요소를 제거합니다. 그 수단
우리는 아무것도 할 필요가 없습니다.그러나 어떻게 할 수 있습니다
이를 확인? 이제 우리는 실제 구현을 확인 할 수 있습니다
프레임 워크의 ArrayAdapter 클래스. 그리고 여기에서
Android의 내부 ArrayAdapter 클래스 코드
프레임 워크. 당신은 아래의 링크와 함께 따를 수 있습니다.
먼저 Add 메서드를 검색하는거야. 기억,
우리는 예측 문자열을 추가했습니다. 이것을 사용하는 어댑터
방법.그리고 물론, 우리는 그것을 볼 통지한다
방법으로 변경하여 데이터 집합이 내부적으로 호출됩니다. 하지만 당신
여기에이 부울에 대해 무엇을 생각하고있을 가능성이 있습니다. 잘
는 그것을보고하자. 당신이 제일 위로 스크롤하면
당신은 변화 통지는 다음과 같이 선언되어있는 것을 알 수 있습니다
처음에는 참. 당신은 다른 참조를 통해 이동으로 당신은거야
그것은 여기서 밖에 바뀐 것을 알 수 있습니다.이 세트는
변경 방법에 통지한다. 우리는이 나라를 호출하지 않으므로
방법 가짜 값으로, 그때 우리는 우리가하고있는 것을 알고있다
안전 할 때마다 어댑터의 갱신을 통지 할 예정이다.
이제 add 메소드로 돌아가 보자. 하고 싶은
당신에게 하나의 더 많은 것을 보여주고있다. 당신은 추가 기능을 알 수 있습니다
모든 방법은 한 번만 옵저버에 통지한다.반면
당신이 이것을 호출 할 때마다 그것이 업데이트됩니다 add 메소드
그것은 관찰자이다. 그것은 우리의 코드가 실제로 상쾌하다는 것을 의미
목록마다. 그래서 당신은 위의 벌집을 대상으로하는 경우
당신이 좀 더 있으면이 방법을 사용할 수 있습니다
효율적입니다. 일반적으로 시도하여 이렇게 두려워하지 말라
스스로.일반적인 프로 끝으로 혹시 무언가를 모르는 경우는
가서 확인하게 자유롭게 느낀다
Android 소스 코드. 프레임 워크 코드를 치료하지 마십시오
블랙 박스처럼. Android는 오픈 소스라는 사실을 활용하십시오. 더
더 당신은 플랫폼에 대해 배울
당신이 될 수 있습니다 Android 개발자보다.45 - 스크린 샷을
======================

지금 우리의 응용 프로그램은 실제 데이터를 나타내고 있음을 우리는 가지고 있어야합니다
우리의 앱 스크린 샷, 그래서 우리는 그것이 무엇인지 기억합니다
우리는 지금까지 그것을 만들었을 때처럼. 나는 개인적으로이 일을 좋아
그럼 내가 볼 수 있기 때문에 응용 프로그램을 구축하는 과정을 통해
뒤로, 그리고 그것이 어떻게 진화했는지를 참조하십시오.나는 당신에게 하나를 보여 주마
당신의 장치의 스크린 샷을 찍을 수있는 방법. 열
Android 장치를 모니터링하고 여기에서 장치를 클릭하십시오. 그 후, 클릭
이 카메라 아이콘을 화면 캡처하려면. 때 팝
저장을 칠 수 있으며, 설정이 완료되면 업.특정 물리적 장치는 실제로 하드웨어 키가 존재하고 있음
당신은 스크린 샷을 잡을 수 있습니다. 예를 들어 위
넥서스 5는 당신이 오랫동안 다운 볼륨에 누를 수 있습니다
동시에 전원 키. 그것은 새
스크린 샷. 이것은 사진 응용 프로그램에 저장되어 있으며,
그럼 당신이 원하는 사람에게 그것을 공유 할 수 있습니다.당신이 구축하고있는 것을 훌륭한 애플 리케이션 그들을 표시 할 수 있습니다.


46 - 완료
=========

그리고 이제 레슨 2에서 끝났습니다. Woohoo. 당신이 만든
에서 데이터를 전송할 수있는 것에 큰 단계
서버는 다운 그것을 모든 방법을 가져온다
장치. 귀중한 정보 지금 모든 가능성을 생각해
당신은 사용할 수 있도록 사용자에게 다운 가능성
자신의 손가락.그리고 그것은 매우 강력합니다. 영향에 관하여 말하면,
당신은 당신을 위해 뭘하려고하는지에 대해 생각했다
아직 최종 프로젝트? 당신이 원하는 어떤 주제를 선택할 수 있습니다.
클래스 토론회에 당신의 아이디어를 공유하고,
당신도 소셜 미디어에서 친구들과 공유 할 수 있습니다.
지금 베타에 오버 내가 빠른 낮잠을하면서
이 Done을​​ 베개에.나는 3 장에서 만나보세요.


47 - 2 단원 요약
===================

그래서 지금은 모의 데이터와 UI를 촬영 한
그리고 실제 데이터로 업데이트하는 방법을 배웠습니다. 당신
권한을 사용하는 방법을 배웠습니다 프로세스 시간이 걸리는 이동
UI 스레드, 그리고 기본에 도입되었습니다
네트워크 I / O의. 3 장에서 다시 참가,
우리는 더 많은 활동을 작성하고 탐색하는 방법을 배웁니다 어디에
그들 사이.하지만 먼저 내가 가지고 가도록 나와 함께 온다
당신의 Android 역사에 다른 항해


48 - Storytime 안드로이드 소비자 플랫폼
========================================

2013 년 7 월의 시점에서 1 년 반
만 명이 새로 Android 장치는 매일 활성화되어 있었다.그래서 그 작은 수를 믿는 것은 어렵다
몇 년 전, 나는 잠재적 인 개발자가 설명하면 모든 회의를 시작했습니다
무엇 안드로이드했고, 그것이 있었다는 것을 그들을 설득
플랫폼의 개발에 시간과 노력의 가치.
그것은 우리가 짝수로 공유되고있는 것이 2010 년까지이 아니었다
10 만 매일의 활성화 플랫폼의 성장을 설명하기 위해
그해 5 월.빠르게 성장했다
주위 억 이상의 Android 장치를 나타내며 2012 년
나는 나의 프리젠 테이션을 시작하지 않는 이유 인 세계,
방에서 아무도 Android 장치를 가지고 있는지 여부를 물어
더 이상. 나에게도 이러한 초기의 최대의 놀라움
날이 사람들을 설득하기 위해 얼마나 많은 노력을 필요로했다
모든 모바일 용으로 개발하는 것은 가치있는 투자 였음.사람들의 거대한 숫자는 가기 위하여 자신의 휴대 전화를 사용
메인으로 자신의 휴대 전화를 사용하여 온라인으로들을 많이
이렇게하는 방법. 퓨 리서치에 의한 하나의 연구
2013 년 인터넷 프로젝트는 휴대 소유자의 3 분의 2 가까이를 발견
온라인에 자신의 휴대 전화를 사용하고 이중 속도가 발견되었습니다.
2009 년에 그 전화 사용자의 3 분의 1은 주로 사용
자신의 휴대 전화는 온라인 취득한다.두 번째 그것에 대해 생각 해보세요.
이 휴대 전화는 항상 연결되어있는 포켓 용 컴퓨터가되고있다
인간의 지식의 합계가 사용할 수 있도록하는 클라우드
터치와 눈에 우리에게. 그건
사람들이 늘고 위해 그 생각해,
모바일에서 떨어져 에서다 때 온라인 취득하는 방법은 없습니다
당신의 책상. 이것은 실제로 그들의 기본으로 PC를 이동 사다
컴퓨팅 플랫폼입니다.변화는 매우 드라마틱와 동향이다
전적으로 의존하고있는 Google과 같은 때문에 클리어하는 것을 기업,
인터넷은 확인하고 모바일 최초의 정책을 가지고
구축하면 모바일 경험이 첫번째 고려 사항이다.
새로운 제품.이러한 경향은 더 젊은 사이에서 특히 현저하다
특히 휴대 전화를 사용하여 성장하는 사용자
아프리카와 아시아 등 신흥 시장에서 어디에
데스크톱 용 광대역 유비쿼터스을 지원하기위한 인프라가 없습니다
로 쉽게 사용할 수있다. 내가 직접 때, 나는 이것을 보았다
케냐 A를 방문하는 행운을했다
몇 년 전.유비쿼터스 전화와 열정, 재능있는 개발자
정말 익숙해 져 있었지만, 실제로 친 것을 나는 때였다
이 휴대 전화는 사람 연대의 중요한 부분이 있었다
일상 생활. 그냥 이메일을 확인 또는 Facebook에 게시되지 않은
그것은 식료품에서 버스를 모두 구입하는 [UNKNOWN을 사용하고 있었다
요금.모빌은 내가들은 생활의 일부 같았다
오히려 당신이 관심을 가지고있는 것을 나타 내기 위해서 누군가의 음료를 구입하는 것보다
그들이 호출 할 수 있도록 당신은 그들에게 전화 크레딧을 전송할
당신은 같은 느낌입니다.추이는
에 생활의 일부 하이테크 액세서리 스마트 폰
당신이 일을 위해 지불 방법 온라인으로 입수 주요 방법
심지어는 바람 방법으로 우리에게 큰 기회를 나타
개발자. 질문은 어떻게 세상을 변화하려고하고 있습니까?
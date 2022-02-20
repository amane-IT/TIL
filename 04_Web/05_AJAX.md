#AJAX
- Asynchronous JavaScript and XML
- 비동기로 자바스크립트를 요청하면 XML로 응답하는 방식
    - text, xml, json으로 응답 가능
    - 데이터만 전달 받는 것
- ※ 화면 갱신없이 데이터를 서버로 부터 가져와 처리하는 방법
    + 페이지 이동 없이 페이지가 변경된 것처럼 보임
- 사용자 입장에서 편리
- 구현 어려움 (동적으로 DOM 구성)

## 동기방식
- 클라이언트가 특정 페이지 요청
- 서버가 특정 페이지에 대한 응답을 보낼 때까지 기다림
- 응답을 보냄
- 응답을 화면에 뿌림
- 서버 중심 (Server Side Rendering)

-> 클라이언트는 응답을 받을 때까지 아무것도 못하고 기다리기만 함

## 비동기 방식
- HTML파일을 요청
- 클라이언트는 다음 코드를 수행
- 응답이 올 때까지 다른 것을 수행
- 응답을 받으면 화면에 뿌림
- 클라이언트 중심 (Client Side Rendering)

## getXMLHttpRequest()
- ActiveXObject() -> MS IE를 불러오는 함수
- XMLHttpRequeust()
  + 기타 웹 브라우저를 불러오는 함수
  + 표준을 따르는 브라우저는 이걸로 불러올 수 있음

## sendRequest(url, params, successcallback, errorcallback, method, dataType)
- 서버에 AJAX를 요청하는 함수
- url: 요청 주소
- params: 정보(데이터)
- method: GET(queryString) or POST(Request)
- successcallback: 서버의 데이터를 성공적으로 받으면 수행하기 위해 외부에서 만든 함수
- errorcallback: 서버의 데이터를 받는 것을 실패하면 수행
- dataType: 서버로 부터 받을 데이터 타입(json, xml, csv, text..)

### open(): 요청의 초기화, GET/POST 선택, 접속할 URL 입력...
### send(): 웹서버에 요청을 전송

<br>

---

## httpRequest 속성값
### readyState
- 현재 클라이언트의 상태
- 0(객체만 생성), 1(open 메소드 호출), 2(send 메소드 호출)
,<br> 3(데이터 일부만 받음), 4(데이터 전부 받음)
### status
- 서버가 반환하는 상태
- 200(OK), 403(접근 거부), 404(page not found), 500(서버오류)...

<br>

## GET VS POST
### GET
- URL에 변수를 포함시켜 요청
- 데이터를 Header에 포함하여 전송
- URL에 데이터가 노충되어 보안 취약
- 전송하는 길이 제한 있음
- 캐싱 가능

### POST
- URL에 변수 노출 없이 요청
- 데이터를 Body에 포함시킴
- 기본 보안 유지
- 전송 길이 제한 없음
- 캐싱 불가

#### 캐싱: 한번 접근 한 후, 재요청에 대비하여 빠르게 접근하기 위해 레지스터에 데이터를 저장해 놓는 것

---

# 데이터 전송 형식
## CSV
- 콤마로 값이 구분되는 문서
- 많은 양의 데이터 전송 시 유리
- 파일크기 작음, 짧음
- 각각의 데이터가 어떤 내용인지 파악하기 힘듦
- 값에 대한 정보가 없음
- 빅데이터 분야에서 많이 사용

### XML
- 태그로 데이터를 표현
- 태그로 데이터의 정보르 알 수 있음
- 값의 정보를 확실히 알 수 있음
- 부가 정보가 많아서 파일 용량이 큼

### JSON
- CSV와 XML의 단점 극복
- 대부분 AJAX사용
- 자바스크립트에서 사용하는 객체의 형식으로 데이터 표현

---

# Event 관리
- AJAX는 서버와 통신하는 과정이 웹 브라우저 내부에서 이루어짐
- 사용자가 진행상황을 알기 어려움
- SO, 진행상태를 보여주는 기능 구현
  + loadend: 요청이 완료되었을 때, 발생
  + loadstart: 데이터 로드 요청을 시작했을 떄 발생
  + 이 외) abort, error, load, progress, timeout...
  

## AJAX의 보안적 이슈
- 기존 예제는 하나의 서버에서 동작
  + 같은 서버 내부에서 작동하면 안전하다고 판단함
  
- 클라이언트가 다른 서버에서 접근 시, 위험하다고 판단
  + 동작하지 않음
- SOP(Same Origin Policy)
  + 같은 도메인을 가지고 있으면 수행
  + 다른 도메인에서 수행되면 CORS error
  
- ※ AJAX는 다른 도메인과의 통신이 기본적으로 불가능
 - Spring을 통해서 Servlet의 정책을 변경하면 가능

---

# 반응형 웹
- 모든 스마트 기기에서 접속 가능
    + 원래는 기기에 맞춰 디자인 코드가 따로 있어야 함
- 가로 모드에 맞춰 레이아웃 변경 가능
- 사이트 유지관리에 용이
- css만 수정하면 되는 것 = 반응형 웹

## 뷰포트(viewport)
- html에 작성된 meta 데이터 값
- 접속한 기기 화면에 맞춰 확대/축소 표시 가능
- 스마트 기기에서 실제 내용이 표시되는 영역

> < meta name="viewport" content={속성:값, ..., initial-scale=1.0 >
> - content: 뷰포트에 지정할 속성 지정
>   + width, height,
>   + user-scalable: 확대, 축소 가능 여부
>   + initial-scale: 초기 확대/축소 값...

<br>

--- 

# 부트스트랩
- 빠르고 쉬운 웹 개발을 위한 프론트엔드 프레임워크
- HTML / CSS 기반 디자인 템플릿 + 선택적 Javascript 플러그인 제공
- 빈응형 디자인을 쉽게 만들 수 있음

## 장점
- 사용하기 쉬움
- 반응형 기능
- 모바일 우선 접근 방식
- 브라우저 호환성

## Container
- .container 클래스: 반응형 고정 너비 컨테이너 제공
    + 좌우로 여백을 줘서 요소를 가운데에 몰아 놓은 것
- .container-fluid 클래스: 뷰포트 전체 너비에 걸쳐있는 전체 너비 컨텐츠 제공

## Grid System
- 플렉스 박스로 구축됨
- ※ 페이지에 최대 12개의 열을 허용
- num: 12개의 열 중 num개 만큼 차지하겠다는 뜻


| 클래스명 | 해당 픽셀 이상에서 적용됨 |
|:---:|:---:|
| .col-num | < 576px |
| .col-sm-num | ≥ 576px |
| .col-md-num | ≥ 768px |
| .col-lg-num | ≥ 992px |
| .col-xl-num | ≥ 1200px |

## 기타 속성
### container-fluid mt-1 mt-5
  + container-fluid 클래스를 사용하고 margin-top=0.25rem 과 margin-bottom=3rem 을 설정함
  + 화면 크기에 맞춰 여백의 비율이 깨지지 않게 함
  
<br>

#### rem: 루트 태그의 글꼴 크기의 상대적인 크기를 뜻함
  - 루트의 글자크기: 16px
  - 0.25rem: 4px
  - 3rem: 48px...

### Accordion
  + 화면을 줄였다가 늘렸다 할 수 있는 토글 기능 구현

### Carousel
  + 시간에 따라 움직이는 배너 같은 창을 만들 수 있음

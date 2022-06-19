# 탄소 물 발자국 기록 프로그램

## 프로젝트 개요
- 마신 물의 정보를 바탕으로 탄소 발자국을 기록할 수 있는 프로그램을 제작한다.
- 프로그램을 활용해 실제로 마신 물의 양을 기록하도록 하는 실험을 진행하고, 탄소 배출량 추이를 분석한다.

<hr>

## 프로그램 개요 및 차별성
- 사용자가 마신 물에 대한 정보를 쉽게 입력할 수 있도록, 모바일 환경을 지원하였다.
    - iOS, Android native app을 모두 구현하기는 현실적으로 어렵기 때문에, 접근성이 높은 웹 형태로 제작하였다.
    - bootstrap의 grid system을 활용하여 반응형 웹을 구현하여 다양한 크기의 모바일 기기에 대응하였다.
    - 모바일 환경에서 웹에 접속하였을 때 모바일 앱과 같은 느낌이 나도록 탭 기반의 레이아웃을 구성하였다.
  
- 프로그램을 통해 온라인 환경에서 실험을 진행할 때 얻을 수 있는 장점을 살리고자 하였다.
    - 랭킹 시스템을 통해 경쟁 심리를 유발하여 탄소 배출량을 줄일 수 있도록 유도하였다.
    - 과거의 기록까지 한 눈에 쉽 게 볼 수 있는 분석 페이지를 구현하여 사용자가 자신의 점수를 객관적으로 파악하는 것을 도왔다.
    - 모든 유저들의 기록을 바탕으로 현재의 평균값을 제공해 보다 인터랙티브한 질문을 구성할 수 있다.

<hr>

## 앱 기능 소개

0) 탭바

- 화면 하단에 3개의 탭을 만들어, 클릭을 통해 다른 섹션으로 이동할 수 있다.
- 현재 선택한 탭을 활성화하여 사용자가 선택된 탭을 직관적으로 알 수 있도록 하였다.

1) 발자국 기록
<img width="769" alt="image1" src="https://user-images.githubusercontent.com/41565118/174465943-d435a900-9233-4def-897c-c885453e8bd8.png">
<img width="769" alt="image2" src="https://user-images.githubusercontent.com/41565118/174465944-23625247-a7e9-4d0a-ae2b-209bda91be50.png">

- 사용자가 오늘 마신 물과 관련된 정보를 바탕으로, 탄소 발자국 값을 계산한다.
- 사용자가 선택한 물의 종류에 따라 다른 질문이 나타나도록 구현하였다.
- 사용자의 선택지에 따라 자동으로 탄소 발자국 값을 계산하여 저장한다. 
- (아직 구현하지 않았으나, 보고서에 써도 괜찮을 내용 -> 디자인은 다 나와있으니 기능 구현은 나중에 해도 괜찮음) 사용자가 마신 물의 사진을 업로드하면 OCR을 통해 자동으로 물의 종류와 용량을 인식해 자동으로 선택지를 선택한다.
  - 구현 예상 방식
  * 사용자가 오늘 마신 물의 사진을 올린 뒤, 직접 물의 종류 영역과 물의 용량 부분을 사각형으로 선택한다.
  * opencv 라이브러리를 활용해 이미지에서 선택한 부분을 잘라 OCR을 진행한다. 이 때, 물 용량의 경우 영어로만 이루어져 있기 때문에 아무 라이브러리나 사용해도 괜찮지만, 물의 종류의 경우 한글로 이루어져 있을 것이므로 한글 인식이 가능한 OCR 모델을 활용해야 한다. 두 부분에 다른 OCR을 모델을 활용할 이유는 없으므로 가장 유명하고, 한글을 지원하는 OCR 라이브러리인 pytesseract 라이브러리를 활용한다.
  * 라이브러리를 활용해 인식한 결과값을 바탕으로, 선택지를 자동으로 선택해 준다.

2) 체크리스트
<img width="769" alt="스크린샷 2022-06-19 오후 1 34 34" src="https://user-images.githubusercontent.com/41565118/174465999-745e9b83-e933-40ff-901b-63dbe2e4c240.png">

- 사용자가 선택한 값을 바탕으로, 점수를 계산한다.
    - 사용자가 획득한 점수를 나무 이미지를 통해 보여준다.
- 전체 사용자 점수의 평균을 계산해 매일 다른 평균값을 보여줌으로써 인터랙티브한 질문을 구성하였다.

3) 랭킹
<img width="769" alt="스크린샷 2022-06-19 오후 1 35 37" src="https://user-images.githubusercontent.com/41565118/174466018-a1dee9e6-d445-4f1e-8fff-afeae836c8b6.png">

- 사용자의 가장 최근 점수를 바탕으로, 순위를 보여준다.
- 유저의 점수를 텍스트 파일 형식으로 저장해 두고, 이를 파싱하여 활용한다.

- <img width="769" alt="스크린샷 2022-06-19 오후 1 37 25" src="https://user-images.githubusercontent.com/41565118/174466052-f4c5184d-4523-4434-8f39-f89bb061a326.png">

- 사용자의 이름을 누르면 최근 7회에 사용자가 얻은 점수의 추이를 분석하여 보여준다.

<hr>

### 추가로 구현해야 하는 것 및 구현하면 좋을 내용
1. SNS 로그인 기능
    - 프로그램을 활용할 때 자동으로 유저의 값을 저장하고 유저를 특정하려면 SNS 로그인 기능이 필요하다.
    - SNS 로그인 기능 중 카카오톡을 활용한다면, 유저가 특정 시간이 되었음에도 마신 물의 양을 기록하지 않은 경우 카카오톡 알림톡으로 기록을 유도할 수 있다.

2. 더욱 상세한 사용자 점수 분석
    - 현재는 사용자의 최근 7일간의 점수 추이와 가장 높은 점수를 기록한 날만을 보여주고 있다.
    - 사용자의 모든 점수가 기록되고 있기 때문에 이를 활용하면 사용자에게 더욱 도움이 되는 분석 결과를 제공할 수 있을 것이다.
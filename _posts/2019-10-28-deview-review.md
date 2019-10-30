---
layout: post
title:  "2019 데뷰 Day1 정리 (Deview summary)"
date:   2019-10-28 13:55:01 +0800
categories: [Conference]
tag: [DL, Conference]
---

* content
{:toc}


* 이미지 정리 



외산 클라우드 없이 AI 플랫폼 제공하기: features, training, serving, and AI Suite
====================================
AI Platform without using cloud - 현동석 (발표자료: https://deview.kr/2019/schedule/303#)

AI Platform 필요 이유: 보안, 비용, 요구사항

기존 구조
------------------------------------
![诫子书]({{ '/styles/images/deview/ai_prepared.png' | prepend: site.baseurl }})
네이버에서 이미 준비된 사항들:
- 분산 데이터 저장소
- 분산 데이터 처리
- 모델 학습 플렛폼
- 모델 서빙 플렛폼


데이터 전처리
------------------------------------
![诫子书]({{ '/styles/images/deview/ai_features.png' | prepend: site.baseurl }})
AiFeatures
- 어떤 식으로 데이터가 처리되었으면 좋겠다는 것만 정하면 데이터 전처리됨
- dump: Hive SQL을 통해 필요한 데이터 추출하여  HDFS에 저장
- analyze(Labs): 데이터  bias, average 등 확인, 분산환경의 주피터 노트북 인스턴스 사용 가능
- batch: pyspark + distributed NLP 
문제/팁: 
- Facet(데이터 가시화 툴)은 클라에서 처리하므로 엄청 느려짐
  다 볼 필요 없이 샘플링해서 보면 됨
  그런데 HDFS 파일이라 전체를 다 읽어야 샘플링 가능
  몇몇 row를 스킵하여 일부만 읽도록 함수 사용
- 처음에 코드 작성은 샘플링에서 작성하고, 파이썬 코드를 submit 해서 batch 모드에서 전체 데이터 처리
- nlp를 spark에서 분산처리할 때 다 설치해야하는 문제점 -> nlp api + throttling proxy 


모델 학습 
------------------------------------
![诫子书]({{ '/styles/images/deview/model_train.png' | prepend: site.baseurl }})
모델 연구시 데이터 캐싱하면 이득, 서비스할 때는 캐싱하지 않고 최소자원 사용
학습 자동화:
- 데이터를 HDFS에 저장해놓고 학습시 docker를 사용
- 그때그때 yarn이 자원관리를 하며 학습에 필요 자원 할당


데이터 서빙
------------------------------------
![诫子书]({{ '/styles/images/deview/model_serve.png' | prepend: site.baseurl }})
- yarn cluster위에서 돌아감 (알아서 스케일링 함)
- backend type을 선택해서 서빙 가능
- 사용자가 만든  모델 서빙 코드를 깃헙에 올려놓으면 -> 빌드 -> 배포 -> 사용자가 정의한 프론트앤드
- 예측 요청 로그도 남김


자동화: AI Suite
------------------------------------
![诫子书]({{ '/styles/images/deview/ai_suite.png' | prepend: site.baseurl }})
- 미리 정의한 dump, training 등의 기능을 드래그만 해서 사용 가능
- 모든 과정을 UI상의 크론 기능으로 스케줄링 가능
- 파이프라인 실행 과정 가시화 (dataflow 처럼)


기타 내용
------------------------------------
문의 내용
- 이미지 처리를 위해 다중 모델을 사용할 경우 어떻게 하나?
지금은 모델 하나하나 인스턴스를 만들어서 처리해야 한다.
- 이미지 데이터는 hdfs에 어떻게 저장되는가?
바이너리 파일 그대로 저장해서 사용함
- 아직 외부 서비스는 아니고 사내에서 사용되고 있는 서비스



문자인식(OCR), 얼마나 정확하지? (문자인식 성능을 정확하게 측정하는 방법)
====================================
Measuring OCR precise accuracy - 최찬규 (발표자료: https://deview.kr/2019/schedule/311#)

성능 평가가 왜 중요한가: 
- 문제점 파악하여 성능을 개선할 수 있기 때문
- 어떤 모델을 사용할지 선택
- 다른 연구 그룹과 성능 비교

기존 문자인식 성능평가 방법:
- 눈으로 직접, 시간 비용이 많고 평가 오류가 있음
- 컴퓨터로 자동 평가 시스템 (발표할 내용)

Optical Character Recognition 사용사례
- 파파고에서 이미지 번역에 사용중
- 그 외에 신용카드, 명함, 신분증 인식에 사용

문자인식 과정
- 문자 검출 (글자의 위치가 어딘지)
  평가: IoU
- 문자 인식 (Text Recognition)
  평가: WEN, 1-NED
- 전체 평가: End-to-End

문자 검출 평가 방법: IoU
- Ground Truth와 Prediction 박스가 얼마나 겹치는지 확인 (50%가 넘는지)

문자 인식 평가 방법: WEN(word based exactly matching)
- 정답과 예측 단어가 정확히 일치하는지 체크
- 단어대 단어로 평가하기 때문에 단어의 길이(문제의 난이도)가 반영되지 않음

문자 인식 평가 방법: 1-NED(Normalized Edit Distance)
- 두 단어간 편집거리 측정하여 긴 단어의 길이로 정규화

전체 평가 방법: End-to-End
- Cascade 방식으로 단계별 인식해서 넘겨줌

기존 방법의 문제점
- 정교한 성능 측정 불가 
    - 고유명사를 잘라지게 탐지/한글자 놓치고 탐지할 경우
    - 커브가 들어간 글자
- One-to-Many 문제
    - 하나의 박스가 여러개로 나뉘어 예측되는 경우 (split)
- Many-to-One 문제
    - 여러개가 하나의 박스로 인식 (merge)
- End-to-End 문제
    - IoU가 50%보다 낮아서 인식까지도 못가는 경우 발생

신규 평가 방법 (사진 참고)
- 예측박스가 정답박스 안에 있는 내용을 인식하는 경우를 탐지 (같은 글자를 앞쪽부터 하나씩 지워가는 방식)
  글자를 몇개나 맞췄는지 
  -> One-to-Many/ Many-to-one 문제도 이와같은 문제 해결 가능

문제점! 
- 엣지 케이스 (문자가 두줄로 되어있고, 같은 글자가 있는 경우
  -> one-to-one 우선
  naver는 naver, papago 둘다 걸치고 있으므로 1:1인 papago-papago 먼저 처리

결론: 신규 방법이 기존 문제점들을 다 커버함


신규 평가 검증 (공식 실험 데이터, 공식 검출기, 인식기를 사용하여 비교):
- 문제들이 얼마나 발생하는가?
  M2O, O2M 발생빈고 (사진참고)
- 기존 평가셋과 호환 되는가?
  기존 평가셋으로 성능차이 비교 (사진참고)
- 평가 방법이 믿을만 한가?
  3명의 평가자 모집하여 점수 부여
결론: 기존 평가방법보다 우수함

신규 평가 방법 장점 (사진참고)



질문:
- 문자단위로 인식할때 글자 순서가 뒤바뀌는 이슈 어떻게 대응하나?
  현재 알고리즘을 대응하면 100점이 나옴 하지만 이런 경우가 거의 없음
  글자가 비슷해서 생기는 경우는 있음 (T와 I)
- 띄어쓰기는 어떻게 대응하는지?
  아직 잘 대응 못하고있음
- 레이블링 데이터는 어떻게 만들었나?
  기존 평가셋가지고 그냥 사용함
- 크래프트라는 모델을 개발해서 사용중



모바일 얼굴인식, 엔진부터 DEVIEW에 적용하기까지
====================================
Mobile face recognition - 이승윤, 이연수 (발표자료:https://deview.kr/2019/schedule/312#)


사용자 인식이 중요
- 어떤 이미지가 가장 정확한가? (사진참조)
- ex) 얼굴 기울기 70~80도

Frame Handling
- 어떤 사진이 선명한지 탐지
- gyroscpe를 체크 (아이폰)
UI, UX 전처리 개편
- 카메라 인식 범위 넓게
- 화면 정면 보도록 가이드 제공
Face size
- 엔진을 위해 얼굴 사이즈 설정 (너무 크거나 작은 경우 제한)
- 얼굴이 잘리는 케이스 제한
- 여러명인 케이스 제한
	! 뒷사람이 얼굴이 더 크면 그사람으로 인식됨..
Face Status
- 얼굴 움직이는 경우 얼굴 움직임 감지
- 얼굴 기울기가 있는 경우 어느정도 각도까지 인식하여 똑바로 세움 얼굴 사이즈, 눈 각도를 재어 각도 탐지
- 눈을 감는 케이스  0.25 정도가 눈을 뜨고 있음 (서양인 눈에 대한 논문의 경우 주의 필요!)

Network
- 4가지 과정 암호화
- 인퍼런스 사이즈 최적화 (이미지 크기 줄이고, 압축하여 사용)



어디까지 깎아봤니?: 모바일 서비스를 위한 가벼운 이미지 인식/검출 딥러닝 모델 설계
====================================
한동윤 (발표자료:https://deview.kr/2019/schedule/321#)

모바일 서비스를 모델의 성능은 유지하면서 비용은 줄이는, 즉 모델을 최적화하는 방법들을 다룬 세션

용어 정리:
- backBone: pretrain된 모델 
- transfer learning: backbone의 layer과 추가 layer를 사용하여 학습시키는 방법
- finetuning: transfer learning 할 때 backbone의 파라미터는 고정하고 새로 추가된 layer의 파라미터를 튜닝하는 과정
- 모델 flop: operator들의 총 연산량

모델 학습 과정:


팁:
- 공개 모델은 model-zoo 에서 쉽게 찾을 수 있음
- 강력한 backbone을 사용해야 함 (미세한 성능 차이도 체감상 매우 큼)
- 모델의 flop이 작아질수록 대체적으로 속도도 빨라지지만, 그렇지 않은 경우도 있음
  Concatenation이나 depthwise-conv등은 플랫폼에 따라, 하드웨어에 따라 속도가 다름
- 가벼운 모델 트레이닝 시 Adam류 보다 SGD가 훨씬 좋음
- 가벼운 모델 트레이닝 시 training 커브에 유의해야 함 (후반에 역전되는 듯 하는 경향 발생 가능)
- 강련한 Regularization인 CutMix 도입 (https://github.com/clovaai/CutMix-PyTorch)

모델 설계 부분에서 feature 수가 부족한 layer에 feature를 추가하고, 많은 부분은 feature를 감소하여 성능을 개선했다고 하는데 왜 개선되었는지 모르겠음



[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

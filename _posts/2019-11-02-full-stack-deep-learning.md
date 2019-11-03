---
layout: post
title:  "Full Stack Deep Learning #2"
date:   2019-10-30 01:55:01 +0800
categories: [Lecture]
tag: [DL, Lecture]
---

* content
{:toc}


https://www.youtube.com/watch?v=25_kBogrzrs&t=2186s

Guest Lecture 1: Lukas Biewald - Full Stack Deep Learning
====================================

여러가지 이미지 인식 사용사례
------------------------

SNS에서 하이네캔 브랜드 이미지 조회

피부암 진단

코카콜라 뚜껑의 시리얼 코드를 자동으로 인식하여 당첨여부 확인

인공위성 이미지 인식

가짜 명품 핸드백 탐지

트랙터가 밭에서 자동으로 농작물을 제외한 잡초 제거

마트에서 물품 개수/위치를 체크하는 로봇

기계의 데이터를 통해 고장을 예측

![face_rec_steps]({{ '/styles/images/full_stack_dl/image_rec_startups.png' | prepend: site.baseurl }})



ML을 서비스에 적용할 때 어떤 문제를 직면하는가?
------------------------

ML은 디버깅이 어렵다
- 일반 딩과 다르게 ML에서 오탐이 되었을 때 코드만 본다고 바로 원인을 파악할 수 없음
- 누가 어떻게 학습데이터를 준비했는지부터 확인해야함

정확도가 어느정도가 적당한지 예측하기 어렵다 
- 7주가 지났는데도 정확도가 서서히 계속 증가한다면...?

ML은 예측불가하므로 매우 위험하다
- 이미지넷을 사용해서 이미지 분류는 매우 잘되지만, 하지만 로봇에 적용할때는 다름 (로봇은 사람이 보는 이미지와 같게 보지 않음)
- Tesla 트럭 인식 문제로 사망 사례

서비스에 사용되는 DL은 해킹에 취약하다
- 정지표지판을 약간만 수정해도 우회전 표지판으로 인식되므로 자동주행 차에 치명적일 수 있음

ML은 학습데이터가 있어야 한다
- 모델 튜닝, 모델 선택 등 보다 학습데이터를 증가하는 것이 정확도 증가에 더 큰 효과가 있었음
- 데이터 정재하는 것도 매우매우 중요 (아웃라이어, 잘못된 레이블 등 제거)
- 실제로 반 이상의 DS가 data 정재에 시간을 쓰고 있음
- Andrew Ng도 데이터가 많을수록 좋다고 함










[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

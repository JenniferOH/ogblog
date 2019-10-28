---
layout: post
title:  "2019 Deview day1 review"
date:   2019-10-28 13:55:01 +0800
categories: [Conference]
tag: [DL, Conference]
---

* content
{:toc}



<AI Platform without Cloud>
====================================
현동석
발표자료: https://deview.kr/2019/schedule/303#

AI Platform 필요 이유: 보안, 비용, 요구사항

데이터 전처리
------------------------------------
![诫子书]({{ '/styles/images/deview/ai_features.jpg' | prepend: site.baseurl }})
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
![诫子书]({{ '/styles/images/deview/model_train.jpg' | prepend: site.baseurl }})
모델 연구시 데이터 캐싱하면 이득, 서비스할 때는 캐싱하지 않고 최소자원 사용
학습 자동화:
- 데이터를 HDFS에 저장해놓고 학습시 docker를 사용
- 그때그때 yarn이 자원관리를 하며 학습에 필요 자원 할당


데이터 서빙
------------------------------------
![诫子书]({{ '/styles/images/deview/model_serve.jpg' | prepend: site.baseurl }})
- yarn cluster위에서 돌아감 (알아서 스케일링 함)
- backend type을 선택해서 서빙 가능
- 사용자가 만든  모델 서빙 코드를 깃헙에 올려놓으면 -> 빌드 -> 배포 -> 사용자가 정의한 프론트앤드
- 예측 요청 로그도 남김
문의 내용
- 이미지 처리를 위해 다중 모델을 사용할 경우 어떻게 하나?
지금은 모델 하나하나 인스턴스를 만들어서 처리해야 한다.
- 이미지 데이터는 hdfs에 어떻게 저장되는가?
바이너리 파일 그대로 저장해서 사용함


자동화: AI Suite
------------------------------------
![诫子书]({{ '/styles/images/deview/ai_suite.jpg' | prepend: site.baseurl }})
- 미리 정의한 dump, training 등의 기능을 드래그만 해서 사용 가능
- 모든 과정을 UI상의 크론 기능으로 스케줄링 가능
- 파이프라인 실행 과정 가시화 (dataflow 처럼)



[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
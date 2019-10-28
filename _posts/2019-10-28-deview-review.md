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
------------------------
현동석

AI Platform 필요 이유: 보안, 비용, 요구사항


데이터 전처리 
AiFeatures
- 어떤 식으로 데이터가 처리되었으면 좋겠다는 것만 정하면 데이터 전처리됨
- dump: Hive SQL을 통해 필요한 데이터 추출하여  HDFS에 저장
- analyze(Labs): 데이터  bias, average 등 확인, 분산환경의 주피터 노트북 인스턴스 사용 가능
- batch: pyspark + distributed NLP 
문제/팁: 
- Facet(데이터 가시화 툴)은 클라에서 처리하므로 엄청 느려짐 다 볼 필요 없이 샘플링해서 보면 됨 그런데 HDFS 파일이라 전체를 다 읽어야 샘플링 가능 몇몇 row를 스킵하여 일부만 읽도록 함수 사용
- 처음에 코드 작성은 샘플링에서 작성하고, 파이썬 코드를 submit 해서 batch 모드에서 전체 데이터 처리
- nlp를 spark에서 분산처리할 때 다 설치해야하는 문제점 -> nlp api + throttling proxy 


모델 학습 
모델 연구시 데이터 캐싱하면 이득, 제품시는 최소자원 사용
학습 자동화:
- 데이터를 HDFS에 저장해놓고 학습시 docker를 사용


데이터 서빙
- yarn cluster위에서 돌아감 (알아서 스케일링 함)
- backend type을 선택해서 서빙 가능
- 사용자가 만든  모델 서빙 코드를 깃헙에 올려놓으면 -> 빌드 -> 배포 -> 사용자가 정의한 프론트앤드가 뜸
- 예측 요청 로그도 남김


자동화 AI Suite
- 미리 정의한 dump, training 등의 기능을 드래그만 해서 사용 가능
- 모든 과정을 크론 스케줄로 실행 가능
- 파이프라인 실행 과정 가시화 (dataflow 처럼)



[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

---
layout: post
title:  "Face Recognition 시작하기 "
date:   2019-10-19 16:31:01 +0800
categories: [Deap Learning]
tag: [Image, DL, RaceRecognition]
---

* content
{:toc}


얼굴 인식을 처음 접하며 진행했던 내용 정리


얼굴 인식은 어떤 과정을 거치며 이루어 지나?
------------------------

얼굴 인식 알고리즘 중 유명한 논문 내용 참조 (https://arxiv.org/pdf/1604.02878.pdf)
1. 사진 속에서 사물을 인식하여 네모모양으로 사진속 사물들을 인식하는 단계
2. 인식된 사물들 중 죽복을 제거하는 단계
3. 사물들 중 얼굴이라고 할 수 있는 사물을 인식하는 단계

![face_rec_steps]({{ '/styles/images/face_rec_steps.png' | prepend: site.baseurl }})



[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

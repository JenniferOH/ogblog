---
layout: post
title:  "Kmeans 적정 K 찾기 & 분류 평가하기 Kmeans Finding proper K & Evaluation"
date:   2019-09-17 13:31:01 +0800
categories: [Machine Learning]
tag: [Clustering, Kmeans, ML]
---

* content
{:toc}


Kmeans를 사용하려 데이터를 잘 분류하려면 가장 중요한 요소는 적정 클러스터 개수(K)이다. 어떤 데이터는 클러스터 4개로 분류해야 가장 잘 분류되고, 어떤 데이터는 6개로 분류해야 가장 잘 분류될 수도 있다. 처음 Kmeans를 적용할 때 적정 K를 찾아야 하고, 만약 Kmeans를 지속적으로 사용할 경우 데이터마다 적절한 K는 다르므로 주기적으로 적정 K를 찾아서 모델을 업데이트 해줄 필요가 있을 것이다.

적정 K를 찾는 방법은 다양한데 그 중 간단한 세가지 방법에 대해 설명하고자 한다.
1. Sillouette Score
2. Inertia
3. DB(Davies Bouldin) Index


Sillouette Score				{#실루엣}
------------------------

![诫子书]({{ '/styles/images/jiezishu.jpg' | prepend: site.baseurl  }})



Inertia				{#이너시아}
------------------------

![诫子书]({{ '/styles/images/jiezishu.jpg' | prepend: site.baseurl  }})



DB(Davies Bouldin) Index				{#DB Index}
------------------------

![诫子书]({{ '/styles/images/jiezishu.jpg' | prepend: site.baseurl  }})


[诸葛亮](#)


夫君子之行，静以修身，俭以养德。非淡泊(澹泊)无以明志，非宁静无以致远。夫学须静也，才须学也。非学无以广才，非志无以成学。淫慢则不能励精，险躁则不能冶性。
年与时驰，意与日去，遂成枯落，多不接世，悲守穷庐，将复何及！


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

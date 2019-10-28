---
layout: post
title:  "Building Caffe in MacOS"
date:   2019-10-27 14:25:01 +0800
categories: [Deep Learning]
tag: [DL, Caffe]
---

* content
{:toc}


파이썬: python3.6.5 anaconda 
OS: Mojave 10.14.6


1. https://github.com/BVLC/caffe.git 설치

2. caffe 설치하기
caffe 패키지 설치 이슈
- 참고: https://caffe.berkeleyvision.org/install_osx.html
- 아래 주소에서 NDIVIA 툴킷 다운로드 
https://developer.nvidia.com/cuda-downloads?target_os=MacOSX&target_arch=x86_64&target_version=1013&target_type=dmgnetwork
- 툴킷 설치 후 아래 가이드대로 설정
https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html



3. https://caffe.berkeleyvision.org/gathered/examples/web_demo.html 따라하기
패키지 에러 발생
- 해결방안: 코드 import 부분 수정 
- 참고: https://github.com/attardi/deepnl/issues/31
- 문제되는 패키지: cPickle, cStringIO


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

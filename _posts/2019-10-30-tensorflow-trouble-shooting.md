---
layout: post
title:  "Tensorflow Trouble-shooting"
date:   2019-10-30 01:55:01 +0800
categories: [Tensorflow]
tag: [TF, trouble-shooting]
---

* content
{:toc}



Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX AVX2
------------------------

Tensorflow 학습 코드를 실행시키자 이와같은 에러 발생
환경:
- Macbook Pro Late 2015
- MacOS Mojave
- Anaconda3
- Python 3.6.5
해결방안: Tensorflow binary가 사용중인 CPU에서 지원하는 파일 포멧으로 패키징 되도록 아래 링크에서 재설치
- https://github.com/lakshayg/tensorflow-build/releases/download/tf-1.14-ubuntu18.04-py3.7/tensorflow-1.14.1-cp37-cp37m-macosx_10_9_x86_64.whl
  (python 3.7.4 환경을 다시 만들어서 tensorflow를 재설치하여 해결함)
참고:
- https://stackoverflow.com/questions/47068709/your-cpu-supports-instructions-that-this-tensorflow-binary-was-not-compiled-to-u
- https://stackoverflow.com/questions/41293077/how-to-compile-tensorflow-with-sse4-2-and-avx-instructions?rq=1






[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

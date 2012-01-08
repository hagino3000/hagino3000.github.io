======================================
「キネクトハッカーズマニュアル」正誤表
======================================

最終更新:2011年9月5日

--------------------------
4章 ドライバのセットアップ
--------------------------

Windows用SensorKinectについて、 `64bit Windows用のインストーラー <https://github.com/avin2/SensorKinect>`_ がリリースされました。
64bit版Windowsを利用している場合はSensorKinect, OpenNI, NITEの3つとも64bit版を使うのが良いでしょう。


------------------------
5章 OpenNIプログラミング
------------------------

5.2のコード
===========

2行目、 MacOSで実行する時にinclude失敗するので、次の通り修正してください。

::

  (誤)#include <iostream.h>
  (正)#include <iostream>

----------------------------------
8章 アプリケーションを作ってみよう
----------------------------------

8.3 KinectWeb.h
===============

18行目から21行目

::

  (誤)
  ofxOpenNIContext  recordContext;
  ofxDepthGenerator recordDepth;
  ofxImageGenerator recordImage;
  ofxUserGenerator  recordUser;

  (正)
  ofxOpenNIContext  context;
  ofxDepthGenerator depthGenerator;
  ofxImageGenerator imageGenerator;
  ofxUserGenerator  userGenerator;


図8.9のキャプション

::

  (誤)バックエンドの実行結果
  (正)フロントエンドの実行結果


------------------------------------------
9章 Kinectを使ったアプリケーション開発Tips
------------------------------------------

9.2 ハードウェアの操作
======================

(記載漏れ)
Windowsで動作させるにはlibusbをインストールしてドライバを有効にして実行してください。手順は補足ページを参照してください。

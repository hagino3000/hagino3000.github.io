========================================
「キネクトハッカーズマニュアル」補足資料
========================================

説明不足だった箇所や、本に載せた内容が既に古くなってしまった部分について補足します。

*最終更新: 2012-01-08*

----------------
大きく変わった点
----------------

SensorKinect for 64ビット版Windowsのリリース
============================================

WindowsへのOpenNIのインストールの箇所で **SensorKinectが32ビット版しか無いため** と記載しましたが、64ビット版Windows用のインストーラーがリリースされました。

64ビット版Windowsを使う場合はSensorKinect, OpenNI, NITE全て64ビット用バイナリを使いましょう。

  `avin2/SensorKinect - GitHub <https://github.com/avin2/SensorKinect>`_

OpenNIの進化
============

OpenNIのインストール手順に載せたバージョンはもうダウンロードページから手に入らないので、最新版を利用してください。SensorKinect, OpenNI, NITE 全て新しいバージョンがリリースされました。ボーントラッキングは執筆時点とは比べ物にならない位に使い易くなっています。

- ボーントラッキングに初期ポーズは不要になった。
- 上半身のみ、下半身のみ、頭と手のみのトラッキングが可能になった。
- 対応OSにAndroidが追加された。
- `APIリファレンス <http://openni.org/docs2/Reference/index.html>`_ がオンラインで参照できる様になった。
- AudioGeneratorが実装された(Windows版のみ動作確認済み)


OpenNIのダウンロードページが大きく変りました
============================================

OpenNIのダウンロードページの作りが大きく変っており、本に載せたURLで直接アクセスできなくなりました。

OpenNIのインストール手順にライセンスの入力がありましたが、現在の最新版では不要になりました。ライセンス番号自体はインストールスクリプトの中に記載されており、インストール時にライセンスの登録が自動で行なわれる様になりました。


Xtion pro liveの国内販売開始
============================

Kinect以外のモーションキャプチャデバイスとして **Xtion pro** を紹介しましたが、さらにビデオカメラとアレイマイクが追加された **Xtion PRO LIVE** が発売されました。Xtion Proと同じく5VのUSB給電で動作します(Kinectはチルトモーターが12V必要とするためUSB給電で動作しない)。家電量販店のパーツコーナーで購入できるとの事ですが、Amazonで注文するのが一番早いと思います。

`ASUSTeK Computer Inc. - Multimedia- ASUS Xtion PRO LIVE <http://www.asus.com/Multimedia/Motion_Sensor/Xtion_PRO_LIVE/>`_


.. figure:: images/xtion_pro_live.png
  :width: 480px
  :alt: Xtion Pro LIVE

  ASUS Xtion Pro LIVE

これを機に未実装だったOpenNIのオーディオ周りの部分の実装が進む事でしょう。

-------------------------
1. センサーと姿勢認識技術
-------------------------

深度センサーから得られるデータ
==============================

本文では **距離(深度)の画像データ** と記述しましたが具体的には11ビット1チャンネルのピクセルデータが得られます。取得サイズが640*480の場合は配列長307200のデータだと考えれば良いです。
11ビットのデータを距離単位に変換する方法ですが、本書ではOpenKinectのWikiを参考に次の数式を利用しました。

::

  距離(cm) = 100/(-0.00307 * ${11ビット生データ} + 3.33)

この数式では2.5メートル以内の場合の誤差は2cm以内, 4メートルより遠い箇所での誤差はl0cm以内になります。さらに正確な数式として次の物もあります。

::

  距離(cm) = 0.1236 * Tan(${11ビット生データ} / 2842.5 + 1.1863)

Light Codingに関するPrimeSense社の特許
======================================

参考

`DEPTH MAPPING USING PROJECTED PATTERNS <http://www.freepatentsonline.com/y2010/0118123.html>`_

LEDの使い道
===========

LEDの色が変えられます、としか書いてませんが、プログラムの状態(起動中、認識中、認識停止中)を表現するのに使ったりします。

姿勢認識技術に関するPrimeSense社の特許
======================================

手足の位置を検出するのに、ポーズ検出の後に二値化して輪郭抽出をしているとか書いてありますね。

  `EXTRACTION OF SKELETONS FROM 3D MAPS <http://www.freepatentsonline.com/y2011/0052006.html>`_


-----------------------------------
2. Kinectプログラミングを初める前に
-----------------------------------

Kinect SDK for Windowsの情報源
==============================

Kinect SDK for Windowsの情報源を載せてなかったのですが。Kinect SDKのフォーラムももちろんあります。 

  `Microsoft Developer Network > Forums Home > Kinect for Windows SDK Beta Forums <http://social.msdn.microsoft.com/Forums/en-US/category/kinectsdk>`_

日本マイクロソフトエヴァンジェリストの方々のブログに参考になる記事がいくつもあります。


  `Browse by Tags [kinect] - 川西 裕幸のブログ ｰ - Site Home - MSDN Blogs <http://blogs.msdn.com/b/hiroyuk/archive/tags/kinect/>`_

  `Browse by Tags [kinect] - “匠の国”、日本で、組込み全開!! - Site Home - MSDN Blogs <http://blogs.msdn.com/b/hirosho/archive/tags/kinect+sdk/>`_



-------------------------------
3. Kinectのドライバの種類と特徴
-------------------------------

.. Note::

  執筆時点での普及度を考えてOpenNIを最初に紹介しましたが、OpenNIの公式デバイスはXtion PROで、Kinectは非公式のハードウェアドライバが存在するからたまたま使える、という状況です。今更ですがKinectをMicrosoftのSDK以外で動作させるのはKinect自体のライセンス違反となりますのでご注意ください。


OpenNIの新バージョンが公開されました。 2012年1月1日時点でOpenNI v1.5.2.7 が最新です。

  `OpenNI Modules <http://www.openni.org/Downloads/OpenNIModules.aspx>`_



Kinect SDK for Windows Betaのバージョンアップがありました。対応言語がC++, C#, VB, F#となりました。

  `Microsoft Kinect SDK for Developers | Develop for the Kinect | Kinect for Windows <http://www.microsoft.com/en-us/kinectforwindows/>`_


-----------------------
5. OpenNIプログラミング 
-----------------------

OpenNIのコンセプトについては `OpenNIのドキュメント <http://openni.org/documentation>`_ に詳しく載っています。
この章ではとりあえずKinectを動かせる所まで最小の解説しましたが、クロスプラットフォーム、クロスデバイス、ミドルウェアの複数サポートを実現するための仕組みが盛り込まれています。OpenNIを使う場合はご一読する事をおすすめします。

またOpenNIのクロスプラットフォームAPIは本書のサンプルコードの至る所で使用しています。例えばメモリ操作の `xnOSMemCopy` , `xnOSMemSet` 。8章の3つめのアプリケーションではスレッドの作成に `xnOSCreateThread` を使いました。これらはWindowsでもMacOSでも動作させたいプログラムを書く時に便利です。

5.3 ユーザー検出の利用
======================

ユーザー検出機能とありますが、OpenNIのそれは単純な背景差分による実装の様で、犬だろうが猫だろうが動く物に検知します。故にユーザー検出中にKinectを動かしてしまうと正常に動作しません。

5.4 スケルトントラッキング
==========================

執筆時点ではNITEのボーントラッキングにはキャリブレーションポーズが必要でしたが、現在は不要です。ポーズ検出のフェーズが不要になったのでプログラムは次の通りになります。


*コールバック関数の定義*

.. code-block:: c++

  // コールバック関数とやりとりするデータ
  struct CalibrationCookie {
    xn::UserGenerator * user;
    xn::DepthGenerator * depth;
    CALIBRATION_STATUS lastStatus;
    XnChar * pose;
  };

  // 新たにユーザーを検出した時のコールバック
  void XN_CALLBACK_TYPE NewUser(xn::UserGenerator& generator, XnUserID userId, void* pCookie) {
    // ポーズ検出を開始する
    CalibrationCookie* cookie = (CalibrationCookie*)pCookie;
    cookie->lastStatus = USER_DETECTED;
      cookie->user->GetSkeletonCap().RequestCalibration(userId, TRUE);
  }

  // ユーザーの消失を検知した時のコールバック
  void XN_CALLBACK_TYPE LostUser(xn::UserGenerator& generator, XnUserID userId, void* pCookie) {
    CalibrationCookie* cookie = (CalibrationCookie*)pCookie;
    cookie->lastStatus = USER_LOST;
  }

  // キャリブレーションを開始した時のコールバック
  void XN_CALLBACK_TYPE StartCalibration(xn::SkeletonCapability& capability, XnUserID userId, void* pCookie) {
    CalibrationCookie* cookie = (CalibrationCookie*)pCookie;
    cookie->lastStatus = CALIB_STARTED;
  }

  // キャリブレーションが終了(成功 or 失敗)した時のコールバック
  void XN_CALLBACK_TYPE EndCalibration(xn::SkeletonCapability& capability, XnUserID userId, XnBool bSuccess, void* pCookie) {
    CalibrationCookie* cookie = (CalibrationCookie*)pCookie;
    if (bSuccess) {
      cookie->user->GetSkeletonCap().StartTracking(userId);
      cookie->lastStatus = CALIB_SUCCEEDED;
    } else {
      // 失敗、キャリブレーションからやりなおす
          cookie->user->GetSkeletonCap().RequestCalibration(userId, TRUE);
      cookie->lastStatus = CALIB_FAILED;
    }
  }


*コールバック関数の登録*

.. code-block:: c++

  // UserGeneratorの取得
  xn::UserGenerator user;
  rc = context.FindExistingNode(XN_NODE_TYPE_USER, user);
  errorCheck(rc);
  
  // cookieの作成
  XnChar pose[20] = "";
  CalibrationCookie cookie = {&user, &depth, JUST_GENERATED, pose};
  
  // コールバックの登録
  XnCallbackHandle userCallbacks, calibCallbacks;
  user.RegisterUserCallbacks(NewUser, LostUser, &cookie, userCallbacks);
  
  // SkeletonCapabilityの取得
  xn::SkeletonCapability skeletonCap = user.GetSkeletonCap();
  skeletonCap.GetCalibrationPose(pose);
  skeletonCap.RegisterCalibrationCallbacks(&StartCalibration, &EndCalibration, &cookie, calibCallbacks);
  skeletonCap.SetSkeletonProfile(XN_SKEL_PROFILE_ALL);


5.5 ログ出力について
====================

OpenNIのログ出力設定ですが、最初はInfoレベルまで出力しておいた方良いでしょう。
OpenNIを使い初めたばかりの頃は、謎の初期化時エラーに悩まされます。
xmlファイルが見つからないのか、デバイスが接続されていないのか、ジェネレータの作成でエラーになったのか、ログを詳細レベルまで出しておくとどの段階でエラーになったのか一目でわかって非常に助かります。

例えば5.4のコードを実行した時には次のログが出力されます。

::

      1015	[INFO]	OpenNI version is 1.1.0 (Build 39)-MacOSX (Apr 17 2011 01:52:18)
    171270	[INFO]	USB is initialized.
   1417441	[INFO]	Creating node 'Device1' of type Device: PrimeSense/SensorKinect/5.0.1.32...
   1425614	[INFO]	Module 'Device' configuration was loaded from file.
   2002691	[INFO]	Connected to USB device
   2002951	[INFO]	Property Device.USBPath was changed to 045e/02ae@36/6.
   2082962	[INFO]	Hardware versions: FW=5.1.4 (7) HW=4 Chip=2 Sensor=4 SYS=7
   3737911	[INFO]	Property Device.PhysicalDeviceName was changed to PrimeSense Sensor.
   3738198	[INFO]	Property Device.ID was changed to 0.
   3738216	[INFO]	Device sensor initialized
   3741650	[INFO]	Creating node 'Depth1' of type Depth: PrimeSense/SensorKinect/5.0.1.32...
   3742417	[INFO]	Creating stream 'Depth1' of type 'Depth'...
   3742900	[INFO]	Setting Device.ReadData to 1...
   3743615	[INFO]	Endpoints open
   3769760	[INFO]	Property Device.ReadData was changed to 1.
   3769815	[INFO]	Device.ReadData was successfully set.
   3773058	[INFO]	Property Depth1.FPS was changed to 30.
   3773297	[INFO]	Property Depth1.OutputFormat was changed to 1.
   3773308	[INFO]	Property Depth1.BytesPerPixel was changed to 2.
   3773314	[INFO]	Property Depth1.RequiredDataSize was changed to 614400.
   3773322	[INFO]	Property Depth1.ParamCoeff was changed to 4.
   3773406	[INFO]	Property Depth1.ShiftScale was changed to 10.
   3786063	[INFO]	Property Depth1.ConstShift was changed to 200.
   3786226	[INFO]	Property Depth1.ZPD was changed to 120.
   3786383	[INFO]	Property Depth1.ZPPS was changed to 0.104200.
   3786393	[INFO]	Property Depth1.LDDIS was changed to 7.500000.
   3805964	[INFO]	Property Depth1.Gain was changed to 30.
   3805995	[INFO]	Property Depth1.SupportedModesCount was changed to 9.
   3806006	[INFO]	Stream 'Depth1' was initialized.
   3806013	[INFO]	'Depth1' stream was created.
   3808857	[INFO]	Module 'Depth1' configuration was loaded from file.
   4719342	[INFO]	Creating node 'User1' of type User: PrimeSense/XnVSkeletonGenerator/1.3.1.4...
   5941238	[INFO]	Creating node 'Gesture1' of type Gesture: PrimeSense/XnVGestureGenrator/1.3.1.4...
   5975993	[WARNING]	Failed to set thread priority: Invalid argument
   5976015	[WARNING]	USB events thread: Failed to set thread priority to critical. This might cause loss of data...
  Warning: USB events thread - failed to set priority. This might cause loss of data...
   5976883	[INFO]	USB read thread was started.
   5976899	[INFO]	Property Depth1.ActualReadData was changed to 1.
   6479778	[INFO]	Property Depth1.State was changed to 1.
   6479808	[INFO]	Stream Depth1 is open.
   6480346	[INFO]	Setting Depth1.Mirror to 1...
   6594235	[INFO]	Property Depth1.FirmwareMirror was changed to 1.
   6594266	[INFO]	Property Depth1.Mirror was changed to 1.
   6594275	[INFO]	Depth1.Mirror was successfully set.


デバイスの接続、初期化、設定ファイルの読み込み etc... 細かく状況が出力されているのが分ります。
エラーが発生した時にはOpenNI APIの戻り値のXnStatusを見るよりもこちらを確認するのがおすすめです。


---------------------------------
6. コンピュータービジョンとOpenCV
---------------------------------

既にOpenCVを使っている方は読み飛ばしても大丈夫でしょう。


-------------------------
7. 主にopenFrameworksな章
-------------------------

openFrameworksの0.07stableがリリースされました。
これからopenFrameworksをはじめる方は0.07を利用した方が良いでしょう。

本文中でも少し触れていますがopenFrameworksは主にMacユーザーによってメンテされているので、openFrameworksを使うならばWindowsでやるよりもMacを使う事をお勧めします。

7.1.2. openFrameworksのプログラミングスタイル
=============================================

main関数の最後、

::

  ofRunApp(new testApp());

でnewしたまま終っているのが熟練したC++使いには猛烈に違和感を感じさせるらしいのですが、openFrameworksの流儀ではこのコードをコピペで持ってきて使うためそのままのコードを紹介しています。

-----------------------------------------
9. Kinectを使ったアプリケーション開発TIPs
-----------------------------------------

ブラウザからネイティブコードを呼び出す仕組みとしてNPAPIを紹介しましたが、現在はさらに使い易いPepper C APIが開発されている様です。

`Pepper C API - Native Client SDK - Gogle Code <http://code.google.com/intl/ja-JP/chrome/nativeclient/docs/reference/pepperc/>`_



Node.jsやCanvas周りの技術を一切の説明無しに使っていたので、非Web系な人向けに解説します。

Node.js
=======

サーバー用途に特化したJavaScriptの実行環境です。特徴はシングルスレッド、イベントループというアーキテクチャを採用している事、JavaScriptエンジンにV8を採用しており高速に動作する事が挙げられます。
ここ最近のサーバーサイドJavaScriptの盛り上がりを牽引する存在となっています。

WebSocket
=========

Webブラウザでソケット通信をするためのAPIです。これができる前まで、WebブラウザはステートレスなHTTP(Hyper Text Transfer Protocol)しか話せませんでした。ソケット通信を行なうにはFlashを使うしか無かったのですが、WebSocketの実装が進んだ事で気軽にソケット通信ができる様になりました。

WebSocketは生のTCPコネクションを張るわけでは無いため、TCPソケットライブラリを使ってやりとりする事はできません。

WebSocketでバイナリデータが扱える様になりました
===============================================

執筆時点ではWebSocketでバイナリデータを扱う事はできませんでしたが、2011年末にはバイナリが扱える様になっていました。私が動作確認したのは次のバージョンです。

- Chrome17 dev
- Node 0.6.3

使い方は筆者(西林)のブログでも詳解しましたので、参考にしてください。

`WebSocketでバイナリデータを送受信してみる - 電脳戦士ハラキリ -SE道とは死ぬ事と見つけたり- <http://d.hatena.ne.jp/hagino_3000/20111209/1323372153>`_

Canvas
======

Webブラウザでビットマップデータの描画ができるAPIです。
8章のサンプルアプリケーションではピクセルデータをブラウザまで渡して、Canvasで描画をしています。


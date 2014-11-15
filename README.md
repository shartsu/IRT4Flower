# IRT4Flower 

[国立釧路工業高等専門学校](http://www.kushiro-ct.ac.jp/) 平成23年度卒業研究にて制作した、webカメラに花の写真をかざすと、機械学習を用いて呈示されている花の品種をリア­ルタイムで識別してくれるシステム
論文題目: **『観光用リアルタイム画像認識システムの構築』**

## Features

- 識別を行う対象は北海道に咲く花の画像とし、画像データ内の花の色や形状の特徴からその花の品種が何であるのかを
コンピュータが自ら識別可能となることを目指した。
- 利用者がウェブカメラに対して花の画像を提示すると、当システム内でカメラ映像に映る花の特徴をリアルタイムに抽出し、その抽出情報に対して機械学習を連動させるリアルタイム識別を可能とした。
- これにより、利用者が手軽に自分が撮影した花の品種を特定できる環境を構築した。

## Specifications

当システムの実装にはカメラ映像の処理から機械学習で識別を行う部分まで一貫してOpenCVライブラリを用いた。そのため、システムは第一フェーズとしてカメラ映像の処理、第二フェーズとして第一フェーズで取得した情報を元にした機械学習による識別と、大まかに二つのフェーズへと分けられる。

![](https://raw.githubusercontent.com/shartsu/IRT4Flower/master/images/s1.png)

### 第一フェーズ

まず、第一フェーズとしてカメラ映像の中からターゲットとする花の画像 (以下、入力パターン) の色、形状などの特徴を抽出する。抽出する特徴としては

-  色相・彩度・明度 (HSV) に分割した花弁の色特徴 (3特徴)
- 凸包 (Convex Hull) 内の花弁の面積値を用いた形状特徴
-  花弁の重心から各頂点までの平均距離値を用いた距離特徴

の5特徴を挙げ、識別を行うこととした。

### 第二フェーズ

次に、カメラ映像から抽出した各特徴から入力パターンの品種を特定する。当システムは同一ライブラリで画像処理と機械学習を連動させているため、リアルタイムでの画像認識を可能としている。
識別を行う際に用いるアルゴリズムは、各学習パターンの中からユークリッド距離で近傍にあるk点の多数決で決定されるk最近傍決定則を用いた。
また、識別の際に必要となる学習パターンは、予め画像から特徴を抽出して教師ラベルを付与したものを使用し、1種類の花につき最低10パターン以上用意するものとする。

## Presentation Movie

- 最終発表にて公開したデモ動画

[![IMAGE ALT TEXT HERE](https://raw.githubusercontent.com/shartsu/IRT4Flower/master/images/s2.jpg)](https://www.youtube.com/watch?v=_XMsg-hkFDE)


## Prize
- 平成23年度[「情報処理学会 北海道支部長賞」](http://hokkaido.ipsj.or.jp/pukiwiki/index.php?%E6%94%AF%E9%83%A8%E9%95%B7%E8%B3%9E%E5%8F%97%E8%B3%9E%E8%80%85)を受賞し、同時に独立行政法人国立高等専門学校機構が発行する論文誌­「創造性を育む『卒業研究』集」に研究内容が掲載

## License
- CC by 3.0

## Acknowledgments
- [『観光用リアルタイム画像認識システムの構築』研究論文サマリ](https://github.com/shartsu/IRT4Flower/raw/master/Summary.pdf)
- [CiNii 雑誌 - 創造性を育む「卒業研究」集] (http://ci.nii.ac.jp/ncid/AA12148693)
- [OpenCV] (http://opencv.org/)
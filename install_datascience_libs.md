# データサイエンスに利用するライブラリをインストールする

## 注意! まだ書き途中
これは一応動きますが、まだ matplotlib の設定とか日本語ごか Mecab と Juman++ について書けていません。

## はじめに
ここでは[Jupyter を構築する](./make_jupyter_env.md)で作成した Dockerfile を改変して
データサイエンスでよく利用される次のライブラリやソフトをインストールしていきます。

- 処理をなるべく早くするために Cython
- データプリパレーションで有用な Pandas, scipy
- 機械学習フレームワークの tensorflow, scikit-learn, gensim
- web スクレイピングで使う requests, aiohttp, scrapelib, etc

## Dockerfile の改変
前回 %USERPROFILE%\Documents\docker\datascience に作成した Dockerfile を
テキストエディタで開き、26 行目あたりを次のとおり変更します。

- 変更前
```
RUN apt-get install -yq python3-pip python3-dev \
 && pip3 install jupyter
```

- 変更後
```
RUN apt-get install -yq python3-pip python3-dev \
 && pip3 install jupyter \
 && pip3 install cython pandas scipy matplotlib scikit-learn tensorflow gensim \
 && pip3 install requests aiohttp scrapelib lxml beautifulsoup4 feedparser
```

## 起動と停止
前回同様、楽しんでください。

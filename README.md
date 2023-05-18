# ブルーカーボン・ダイナミクスを可視化せよ！
#### 沖縄県沿岸の水深・水温等の環境条件のデータから、海草藻場の被度を予測しよう！

# 61th place solution 🥉

[link](https://signate.jp/competitions/936)

## 概要
海草藻場の被度（一定面積の地表面や海底面を覆う割合）を、環境変数や衛星画像をもとに推定する機械学習モデルを開発する

<br />

### 評価指標
RMSE

<br />

## やったこと
exp070 <br />
・変数 : 欠損率40%以下のもの　<br />
・欠損率15%~40%の変数をknnで穴埋め　<br />
・model : LightGBM <br />
&emsp; boostying : dart <br />
&emsp; n_estimators : startが5000で1foldごと+250 <br />
・交差検証 : TimeSplit(n=15) <br />
・seed average <br />

<br />
exp076 <br \>
・欠損率15%~40%の変数をknnで穴埋め <br />
・交差検証 : <br />
&emsp;TimeSplit(n=15) <br />
&emsp;nested crossvalidation <br />
&emsp;&emsp; inner cv : TimeSplit(n=3) <br />
&emsp;&emsp; outer cv : TimeSplit(n=8) <br />
・model : LightGBM, CatBoost　<br />
・stacking : Linear, Ridge, SVR　<br />
・被度文献、環境要因データ、時系列ランドサット、前年度のランドサット　<br />

![exp076イメージ図](exp076イメージ図.png "exp076イメージ図")




<br />
<br />

## 提出
| exp | cv | Public LB | Private LB |
----- | -- | --------- | ----------
70 | 0.1630 | 0.1691 | 0.1787
76 | 0.1234 | 0.1735 | 0.1867

<br />
<br />
<br />

### best submit
| exp | cv | public LB | private LB |
----- | -- | --------- | ----------
75 | 0.2490 | 0.1759 | 0.1595

<br />
・変数 : 欠損率40%以下のもの <br />
・欠損率15%~40%の変数をknnで穴埋め <br />
・model : LightGBM <br />
・seed avarage <br />
・交差検証 : 時系列に沿ってクロスバリデーション(学習データの期間の長さをそろえる) <br />
<br />

  | fold | train year | valid year |
  ------ | ---------- | ----------
  0 | 1999 ~ 2006 | 2009 
  1 | 2000 ~ 2009 | 2010
  2 | 2001 ~ 2010 | 2011
  3 | 2002 ~ 2011 | 2012
  4 | 2003 ~ 2012 | 2019
  5 | 2006 ~ 2019 | 2020 


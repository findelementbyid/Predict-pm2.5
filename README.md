# Predict-pm2.5

## Abstract

Course: Data Mining Research & Practice (NCTU)

This project is the 4th homework of this course.

The topic of this project is to handle the series data.

## Requirements

請使用10和11月資料當作訓練集，12月之資料當作測試集，

將前六小時的汙染物數據做為特徵，未來第一個小時/未來第六個小時的pm2.5數據為預測目標

使用兩種模型 Linear Regression 和 Random Forest Regression 建模並計算MAE



1. 資料前處理

 a. 取出10.11.12月資料

 b. 缺失值以及無效值以前後一小時平均值取代 (如果前一小時仍有空值，再取更前一小時)

 c. NR表示無降雨，以0取代

 d. 將資料切割成訓練集(10.11月)以及測試集(12月)

 e. 製作時序資料: 將資料形式轉換為行(row)代表18種屬性，欄(column)代表逐時數據資料

     **hint: 將訓練集每18行合併，轉換成維度為(18,61*24)的DataFrame(每個屬性都有61天*24小時共1464筆資料)

2. 時間序列

  a.預測目標

     1. 將未來第一個小時當預測目標

         取6小時為一單位切割，例如第一筆資料為第0~5小時的資料(X[0])，去預測第6小時(未來第一小時)的PM2.5值(Y[0])，下一筆資料為第1~6小時的資料(X[1])去預測第7 小時的PM2.5值(Y[1])  *hint: 切割後X的長度應為1464-6=1458

     2. 將未來第六個小時當預測目標

         取6小時為一單位切割，例如第一筆資料為第0~5小時的資料(X[0])，去預測第11小時(未來第六小時)的PM2.5值(Y[0])，下一筆資料為第1~6小時的資料(X[1])去預測第12 小時的PM2.5值(Y[1])  *hint: 切割後X的長度應為1464-11=1453

 b. X請分別取

     1. 只有PM2.5 (e.g. X[0]會有6個特徵，即第0~5小時的PM2.5數值)

     2. 所有18種屬性 (e.g. X[0]會有18*6個特徵，即第0~5小時的所有18種屬性數值)

 c. 使用兩種模型 Linear Regression 和 Random Forest Regression 建模

 d. 用測試集資料計算MAE (會有8個結果， 2種X資料 * 2種Y資料 * 2種模型)

# สอน Machine Learning - Linear Regression

หาค่าความสัมพันธ์ ระหว่าง ราคา BigMac ต่อ GDP ประเทศ

## Installation lib

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```
## 1. ขั้นเตรียมข้อมูล
โหลด dataset จาก github [ที่นี่](https://github.com/TheEconomist/big-mac-data/blob/master/output-data/big-mac-adjusted-index.csv)
หรือใช้ pandas ดึงข้อมูล
```python
url = 'https://raw.githubusercontent.com/TheEconomist/big-mac-data/master/output-data/big-mac-adjusted-index.csv'
df=pd.read_csv(url, parse_dates=['date'])
```
แสดงข้อมูลตัวอย่าง
```python
df.head()
```
วาดกราฟ scatter แสดงข้อมูล
```python
plt.scatter(x='GDP_bigmac', y='dollar_price', data=df)
```
เรียกใช้ lib skLearn เพื่อใช้ฟังก์ชั่น Linear Regression
```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
```
## 2.ขั้นเทรนนิ่ง
```python
X = df[['GDP_bigmac']] #expect 2D array
y = df['dollar_price']

model.fit(X,y)
```
## 3.ขั้นเทส
แสดงค่าความสัมพันธ์ต่าง ๆ
```python
model.score(X,y) #ค่า R-Squared
```
```python
model.intercept_ #จุดตัดแกน y
```
```python
model.coef_ #ค่าความชัน m
```
ขั้นเทส ด้วยสมการ y = mx + c
```python
model.coef_ * 9000 + model.intercept_
```
ตัวอย่าง
```python
model.predict([[9000]]) #เทสด้วยค่าเดียว
model.predict([[42500],[7500]]) #เทสด้วยหลายค่า
```
## ทำนาย
```python
predic_Val = model.predict(X)
```
วาดกราฟแสดงความสัมพันธ์ของข้อมูลทั้งหมด และวาดจุดตัดเส้นตรง
```python
plt.scatter(X, y, color='blue')
plt.plot(X,predic_Val,color='orange')
```
## ผลลัพธ์
![1](/media/1-form.png)
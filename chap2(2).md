## 데이터 시각화

### 히스토그램

자료의 분포 상태를 직사각형 모양의 막대 그래프로 나타낸 것 **(자료가 연속적일 경우)**

##### (데이터의 빈도에 따라 높이가 결정)

``` python
import matplotlib.pyplot as plt
import random
dice = []
for i in range(100) :
    dice.append(random.randint(1,10))#1부터 10까지의 숫자가 랜덤 dice리스트에 추가
plt.hist(dice, bins=10, color='black')#bins는 구간갯수를 설정하는 속성
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/75471684-e8641280-59d5-11ea-8666-f641a35b5ef0.JPG" alt="실행결과" width=50% height=50% />

```python
import csv
import matplotlib.pyplot as plt
f=open('seoul.csv')
data = csv.reader(f)
next(data)
jan = []
aug = []
plt.title('1월과 8월의 최고기온 분포도')
for row in data :
    if row[-1] != '':
        if row[0].split('-')[1] == '08' :
            aug.append(float(row[-1]))
        if row[0].split('-')[1] == '01' :
            jan.append(float(row[-1]))
plt.hist(jan, bins=100, color = 'b', label = 'january')
plt.hist(aug, bins=100, color = 'r', label = 'August')
plt.rcParams['axes.unicode_minus'] = False # 마이너스 기호 깨짐 방지
plt.rc('font', family = 'Malgun Gothic')
plt.legend()
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/75471687-e8fca900-59d5-11ea-88da-2cb33e5e72a2.JPG" alt="실행결과" width=50% height=50%/>

### 상자그림(boxplot)

가공하지 않은 자료를 그대로 이용하는 것이 아니라, 자료에서 얻어낸 **최댓값, 최솟값,** 

**상위1/4, 2/4(중앙),3/4**에 위치한 값을 보여줌

```python
import csv
import matplotlib.pyplot as plt
f=open('seoul.csv')
data = csv.reader(f)
next(data)
aug = []
jan = []
plt.title('1월과 8월의 최고기온 분포')
for row in data :
    if row[-1] != '':
        if row[0].split('-')[1] == '08' :
            aug.append(float(row[-1]))
        if row[0].split('-')[1] == '01' :
            jan.append(float(row[-1]))
plt.boxplot([jan,aug])#리스트로 구현하면 분리되서 표현가능
plt.rcParams['axes.unicode_minus'] = False # 마이너스 기호 깨짐 방지
plt.rc('font', family = 'Malgun Gothic')
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/75471691-e8fca900-59d5-11ea-90e4-acfd93f388fa.JPG" alt="실행결과" width=70% height=70%/>

##### 그래프 위아래의 동그라미들은 이상치 값을 표현한 것으로, 다른 수치에 비해 너무 크거나

##### 작은 값을 자동으로 나타낸 것

```python
import csv
import matplotlib.pyplot as plt
f=open('seoul.csv')
data = csv.reader(f)
next(data)
plt.title('월별 최고기온 데이터')
month = [[],[],[],[],[],[],[],[],[],[],[],[]]
#month리스트 안에 각 월의 데이터를 저장할 리스트 12개 생성 
for row in data :
    if row[-1] != '':
        month[int(row[0].split('-')[1])-1].append(float(row[-1]))#0~11번까지 인덱스에 월별 데이터(1월~12월) 저장
plt.boxplot(month)
plt.rcParams['axes.unicode_minus'] = False # 마이너스 기호 깨짐 방지
plt.rc('font', family = 'Malgun Gothic')
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/75471680-e732e580-59d5-11ea-8ebf-a497b0b7fc11.JPG" alt="실행결과" width=50% height=50%/>

```python
import csv
import matplotlib.pyplot as plt
f = open('seoul.csv')
data = csv.reader(f)
next(data)
day = []
for i in range(31):
    day.append([])#day리스트안에 31개 리스트 생성
for row in data:
    if row[-1]!='':
        if row[0].split('-').[1]==8:
            day[int(row[0].split('-').[2])-1].append(float(row[-1]))
            #0~30번까지 인덱스에 일별 데이터 저장
plt.style.use('ggplot')
plt.figure(figsize=(10,5), dpi=300)#그래프의 크기를 가로10, 세로5로 지정
plt.boxplot(day, showfilters=False)
plt.rcParams['axes.unicode_minus']=False
plt.show()
```

boxplot의 **showfilters속성** - 이상치 값을 보이지않게함

<img src="https://user-images.githubusercontent.com/58063806/76705121-10b37700-6721-11ea-8c0f-8f9fd62a70e4.JPG" alt="실행결과" width=80% />
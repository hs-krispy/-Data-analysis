### 성별에 따른 데이터

'행정구역', '2019년01월_남_ 총인구수', '2019년01월_남_ 연령구간인구수', '2019년01월_남_ 0세'와 같이 **남성 데이터가 먼저나온 후 여성의 데이터가 나옴**

``` python
import csv
f = open('gender.csv')# 남성 데이터가 먼저나오고 그 다음 여성 데이터가 나옴
data = csv.reader(f)
m = [] #남성 데이터
f = [] #여성 데이터
for row in data:
    if '신도림' in row[0]:
        for i in range(101):
            m.append(int(row[i+3]))
            f.append(int(row[-(i+1)]))# 여성의 100세 이상 인구수 ~ 0세까지
f.reverse() #리스트의 값을 역순으로 재배열(0세~100세 이상으로 만들기위해)
```

여성의 인구가 뒤에 나오므로 뒤부터 넣어주고 마지막에 뒤집어 주는 방식

``` python
import csv
f = open('gender.csv')# 남성 데이터가 먼저나오고 그 다음 여성 데이터가 나옴
data = csv.reader(f)
m = [] #남성 데이터
f = [] #여성 데이터
for row in data:
    if '신도림' in row[0]:
        for i in row[3:104]:
            m.append(-int(i))# 남여의 그래프가 겹치는 것을 방지하기위해 -를 취해줌
        for i in row[106:]:
            f.append(int(i))
```

위와 같이 범위를 직접 지정해줘도 가능

``` python
import matplotlib.pyplot as plt
plt.rc('font', family='Malgun Gothic')
plt.rcParams['axes.unicode_minus'] = False
plt.title('신도림 지역의 남녀 성별 인구 분포')
plt.barh(range(101), m, label='남성')
plt.barh(range(101), f, label='여성')
plt.legend()
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/76067302-7c376f00-5fd2-11ea-9771-71f1ae8fb202.JPG" alt="실행결과" width=60% height=60%/>

``` python
import csv
f = open('gender.csv')
data = csv.reader(f)
area = input('찾고 싶은 지역을 입력하세요: ')
m = []
f = []
for row in data:
    if area in row[0]:
        for i in row[3:104]:
            m.append(-int(i.replace(',','')))
        for i in row[106:]:
            f.append(int(i.replace(',','')))
import matplotlib.pyplot as plt
plt.rc('font', family='Malgun Gothic')
plt.rcParams['axes.unicode_minus'] = False
plt.title(area + '지역의 남녀 성별 인구 분포')
plt.barh(range(101), m, label='남성')
plt.barh(range(101), f, label='여성')
plt.legend()
plt.show()
```

**원하는 지역을 입력받아 해당 지역의 성별에 따른 인구 데이터**를 얻어 올 수 있다.

<img src="https://user-images.githubusercontent.com/58063806/76067300-7b9ed880-5fd2-11ea-9f37-276029c9f1b0.JPG" alt="실행결과" width=60% height=60%/>
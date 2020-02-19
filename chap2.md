## 데이터 시각화

### matplotlib 라이브러리

파이썬에서 2D형태의 그래프, 이미지 등을 그릴 때 사용

``` python
import matplotlib.pyplot as plt (plt로 축약해서 사용)
```

으로 직선 또는 꺾은선 형태의 그래프를 그리는데 사용되는 pyplot모듈을 사용

### 기본그래프

``` python
import matplotlib.pyplot as plt
plt.title('plotting')#그래프에 제목을 넣어줌
plt.plot([1, 2, 3, 4], [12, 43, 25, 15])#앞의 리스트가 x축 뒤의 리스트가 y축 의미
plt.show()
```

##### plt.plot([a,b,c,d]))와 같이 리스트를 하나만 사용하면 y축을 의미하며 x축과 y축의 데이터개수가 동일해야함

<img src="https://user-images.githubusercontent.com/58063806/74843870-e532ac00-536f-11ea-8cb6-55b9808df401.JPG" alt="기본그래프" width=40% height=40% />

### 그래프에 옵션추가

``` python
import matplotlib.pyplot as plt
plt.title('marker')
plt.plot([10, 20, 30, 40], 'r.--', label='circle')
#'r.--'과 같이 색상, 마커모양, 선모양 순서대로 한번에 가능
plt.plot([40, 30, 20, 10], 'g^:', label='triangle up')
plt.legend()#범례표시
plt.show()
```

##### 범례의 위치는 자동으로 결정되지만 plt.legend(loc = 5)와 같이 직접지정가능

##### 위치

##### 2 	9	1

##### 6	10	5,7

##### 3	8	4

<img src="https://user-images.githubusercontent.com/58063806/74844071-40649e80-5370-11ea-81ad-5ada989af19a.JPG" alt="옵션이 추가된 그래프" width=40% height=40% />

### 데이터 시각화

``` python
import csv
import matplotlib.pyplot as plt
f = open('seoul.csv')
data = csv.reader(f)
next(data)
result = [] #필요로하는 데이터를 넣을 리스트
for row in data :
    if row[-1] != '' :
        if row[0].split('-')[1] == '08' :
            #리스트의 인덱싱 -를 기준으로 나눔(년 - 월 - 일)
            result.append(float(row[-1]))
plt.plot(result, 'hotpink')
plt.show()
```

##### 리스트 슬라이싱을 이용해서 8월에 해당하는 데이터들을 가져옴

<img src="https://user-images.githubusercontent.com/58063806/74846596-11e8c280-5374-11ea-8178-0a72d09701d6.JPG" alt="8월의 최고기온 데이터" width=40% height=40% />

``` python
import csv
import matplotlib.pyplot as plt
f = open('seoul.csv')
data = csv.reader(f)
next(data)
high = []
low = []
plt.title('내 생일의 기온 변화 그래프')
for row in data :
    if row[-1] != '' and row[-2] != '' : #최고기온과 최저기온이 있는 데이터만
            if 1983 <= int(row[0].split('-')[0]) and row[0].split('-')[1] == '10' and row[0].split('-')[2] == '01' :
                high.append(float(row[-1]))
                low.append(float(row[-2]))
plt.plot(high, 'r.--', label = '최고기온')
plt.plot(low, 'b.--', label = '최저기온')
plt.legend()
plt.rc('font', family = 'Malgun Gothic')# 한글폰트 설정하면서 맑은 고딕으로 바꾸기
plt.rcParams['axes.unicode_minus'] = False # 마이너스 기호 깨짐 방지
plt.show()
```

``` python
if 1983 <= int(row[0].split('-')[0]) and row[0].split('-')[1] == '10' 
and row[0].split('-')[2] == '01' :
```

##### 이 부분은 row[0]이 의미하는 날짜데이터를 -를 기준으로 슬라이싱해서 1983년([0]번째요소)이후 부터 10월([1]번째요소) 1일([2]번째요소)을 의미함

##### 또한 그래프 제목으로 한글을 넣으려면 `plt.rc()`를 통해서 폰트를 설정해줘야함

<img src="https://user-images.githubusercontent.com/58063806/74846599-1319ef80-5374-11ea-97f0-df804039942e.JPG" alt="1983년 이후 10월 1일 최고와 최저기온" width=40% height=40% />
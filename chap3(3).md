### 파이차트

pie() 함수는 **전체 데이터 중 특정 데이터의 비율**을 보기 쉽게 표현하기 위해 사용 

``` python
import matplotlib.pyplot as plt
size = [2441, 2312, 1031, 1233]
plt.axis('equal') #파이차트를 동그란 원으로 표현
plt.pie(size)
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/76631103-74546d80-6584-11ea-8b44-4ea93fb6d31a.JPG" alt="실행결과" width=40% />

해당 그래프만으로는 각 부분이 무엇을 의미하는지 알기어려움

``` python
import matplotlib.pyplot as plt
plt.rc('font', family='Malgun Gothic')
size = [2441, 2312, 1031, 1233]
label = ['A형', 'B형', 'AB형', 'O형']
plt.axis('equal')
plt.pie(size, labels=label, autopct='%.1f%%')# 소수점 아래 첫번째 자리까지 표시
plt.legend()
plt.show()
```

**labels속성** -  각 부분이 무엇을 의미하는지 나타내는 레이블(label)을 추가

**autopct(auto percent)속성** - 비율을 자동으로 계산해서 표시함

<img src="https://user-images.githubusercontent.com/58063806/76631096-728aaa00-6584-11ea-8d96-7f25f3b781fc.JPG" alt="실행결과" width=60% />

``` python
import matplotlib.pyplot as plt
plt.rc('font', family='Malgun Gothic')
size = [2441, 2312, 1031, 1233]
label = ['A형', 'B형', 'AB형', 'O형']
color = ['darkmagenta', 'deeppink', 'hotpink', 'pink']
plt.axis('equal')
plt.pie(size, labels=label, autopct='%.1f%%', colors=color, explode=(0,0,0.1,0))
#AB형 강조
plt.legend()
plt.show()
```

**colors속성** - 각 부분에 대해 색을 정해줌

**explode속성** - 특정 부분을 돌출되게 만들어줌(0은 돌출안되게), 특정 부분을 강조해주는 효과

<img src="https://user-images.githubusercontent.com/58063806/76631099-73bbd700-6584-11ea-950b-68097fe5903f.JPG" alt="실행결과" width=50% />

### 파이차트를 이용한 인구 비율

``` python
import csv
f = open('gender.csv')
data = csv.reader(f)
size = []
name = input('찾고 싶은 지역의 이름 : ')
for row in data:
    if name in row[0]:
        m = 0
        f = 0
        for i in range(101)
        	m += int(row[i+3].replace(',',''))
            f += int(row[i+106].replace(',',''))
       	break
size.append(m)# 남성 인구 데이터 추가
size.append(f)# 여성 인구 데이터 추가
print(size)
import matplotlib.pyplot as plt
plt.rc('font', family='Malgun Gothic')
color = ['crimson', 'darkcyan']
plt.axis('equal')
plt.pie(size, labels=[남, 여], colors = color, autopct="%.2%%", startangle=90)
#소수점 두자리까지
plt.title(name + ' 지역의 남녀 성별 비율')
plt.show()
```

**startangle속성** - 파이차트의 시작 각도를 정함(90도로 설정하면 반시계방향으로 90도 이동하며, 

12시 정각에서 마지막 부분의 값부터 그래프를 시작함)

EX) 남, 여 순이지만 12시정각에서 여자 데이터부터 시작

<img src="https://user-images.githubusercontent.com/58063806/76631368-f2b10f80-6584-11ea-807e-92839ff83fb9.JPG" alt="실행결과" width=50% />

###  산점도

산점도는 가로축과 세로축을 기준으로 두 요소가 서로 어떤 관계를 맺고 있는지를 파악하기 쉽게 나타낸 그래프

``` python
import matplotlib.pyplot as plt
plt.scatter([1,2,3,4], [10,30,20,40], c=['red', 'blue', 'green', 'gold'], s=[100,200,250,300])
plt.show()
```

c(color)속성 - 각 점의 색상을 정함

s(size)속성 - 각 점의 크기를 정함

<img src="https://user-images.githubusercontent.com/58063806/76937410-1afb8e00-6938-11ea-90ff-0f3b2928a764.JPG" alt="실행결과" width=60% />

``` python
import matplotlib.pyplot as plt
plt.scatter([1,2,3,4], [10,30,20,40], c=range(4), cmap='jet', s=[100,200,250,300])
#jet컬러맵 - 무지개색과 비슷
plt.colorbar()
plt.show()
```

c=range(4) : 4개의 점들을 각각 다른색으로 표현하기 위해서 사용

cmap속성 - 컬러바에 사용될 색상의 종류를 정할 수 있음

<img src="https://user-images.githubusercontent.com/58063806/76937411-1b942480-6938-11ea-8768-10216c64687d.JPG" alt="실행결과" width=60% />

``` python
import csv
f = open('gender.csv')
data = csv.reader(f)
m = []
f = []
name = input('궁금한 동네 입력 : ')
for row in data:
    if name in row[0]:
        for i in range(3, 104):
            m.append(int(row[i].replace(',','')))
            f.append(int(row[i+103].replace(',','')))
        break
import matplotlib.pyplot as plt
plt.scatter(m, f, c=range(101), alpha=0.5, cmap='jet')
plt.colorbar()
plt.plot(range(max(m)), range(max(m)), 'g')# 남성 인구중 가장 큰 값을 기준
plt.show()
```

alpha속성 - 투명도를 조절할 수 있으며 0에 가까울수록 투명하고 1에 가까울수록 불투명하다

##### plt.plot()으로 남성 인구수 중 가장 큰 값을 기준으로 y=x 형태의 직선 (**추세선**)을 만들어서 **해당 나이대에서**

**어떤 성별의 인구가 더 많은지** 보기 쉽게함

<img src="https://user-images.githubusercontent.com/58063806/76938215-96117400-6939-11ea-84d6-75241e98e35c.JPG" alt="실행결과" width=60% />

``` python
import csv
import math
f = open('gender.csv')
data = csv.reader(f)
m = []
f = []
size = []
name = input('궁금한 동네 입력 : ')
for row in data:
    if name in row[0]:
        for i in range(3, 104):
            m.append(int(row[i].replace(',','')))
            f.append(int(row[i+103].replace(',','')))       				
            size.append(math.sqrt(int(row[i].replace(',',''))+int(row[i+103].replace(',',''))))
        break
import matplotlib.pyplot as plt
plt.style.use('ggplot')
plt.rc('font', family='Malgun Gothic')
plt.figure(figsize=(10,5), dpi=300)
plt.title(name+' 지역의 성별 인구 그래프')
plt.scatter(m, f, c=range(101), alpha=0.5, cmap='jet', s=size)
plt.colorbar()
plt.plot(range(max(m)), range(max(m)), 'g')
plt.xlabel('남성 인구수')# x축에 레이블 추가
plt.ylabel('여성 인구수')# y축에 레이블 추가
plt.show()
```

size리스트에 각 연령의 남성과 여성 인구수를 합친 값을 넣어주고 그 값의 크기에 따라 점들의 색을 결정

(color속성에 점들의 크기가 들어가있는 size리스트를 넣어주면 크기에 따라 점들의 색 표현가능)

- 남녀인구수의 합에 sqrt로 제곱근을 취해주지 않았을때 (점들의 크기가 너무 커져서 그래프가 이상해짐)

<img src="https://user-images.githubusercontent.com/58063806/76937413-1b942480-6938-11ea-98b5-797ad2170948.JPG" alt="실행결과" width=80% />

- 남녀인구수의 합에 sqrt로 제곱근을 취해주었을 때

<img src="https://user-images.githubusercontent.com/58063806/76937407-19ca6100-6938-11ea-9e8a-38763642265c.JPG" alt="실행결과" width=80% />




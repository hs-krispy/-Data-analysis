## 가장 비슷한 인구 구조를 가진 지역

``` python
import csv
import numpy as np
import matplotlib.pyplot as plt
f = open('age.csv')
data = csv.reader(f)
next(data)
home = []
name = input('인구 구조가 알고 싶은 지역의 이름(읍면동 단위)을 입력해주세요: ')
for row in data:
    if name in row[0]:
        home = np.array(row[3:], dtype=int)# 0세~100세이상 인구수
print(home)
plt.rc('font', family='Malgun Gothic')
plt.title(name+' 지역의 인구 구조')
plt.plot(home)
plt.show()
```

위와 같이 알고자하는 지역의 연령대별 인구수를 구하고 그래프로 나타낼 수 있다.

<img src="https://user-images.githubusercontent.com/58063806/78647900-2b2ed980-78f6-11ea-9895-c907db20198f.JPG" alt="실행결과" width=60% />

### 인구 비율의 차이

``` python
import csv
import numpy as np
import matplotlib.pyplot as plt
f = open('age2.csv')
data = csv.reader(f)
next(data)
data = list(data) # data 리스트화
name = input('인구 구조가 알고 싶은 지역의 이름(읍면동 단위)을 입력해주세요: ')
for row in data:
    if name in row[0]:
        home = np.array(row[3:], dtype=int)/int(row[1]) 
for row in data:
    away = np.array(row[3:], dtype=int)/int(row[1])
    print(np.sum(home-away))# 각 연령별 인구비율 차를 다 더함(전 연령의 인구비율 차)
```

알고자 하는 지역과 다른 지역 사이의 **전 연령의 인구비율 차**를 구할 수 있다.

``` python
home = np.array(row[3:], dtype=int)/int(row[1]) 
```

위의 방법으로 **해당 지역의 전체 인구수(row[1])**로 각 **연령대별 인구수(row[3:])**로 나누어서 해당 지역의 각 연령대별 인구비율을 알아낼 수 있다.

이때 data를  `data = list(data)`로 리스트화 시켜주지 않으면 첫번째 for문에서 이미 data를 다 읽었기 때문에 두번째 for문에서는 읽을 수 있는 data가 없게된다. 

<img src="https://user-images.githubusercontent.com/58063806/78647907-2cf89d00-78f6-11ea-9ec4-3a00de50e0fe.JPG" alt="실행결과" width=60% />

``` python
import csv
import numpy as np
import matplotlib.pyplot as plt
f = open('age2.csv')
data = csv.reader(f)
next(data)
data = list(data)
rate = 1 # 인구비율의 차를 넣을 변수
name = input('인구 구조가 알고 싶은 지역의 이름(읍면동 단위)을 입력해주세요: ')
for row in data:
    if name in row[0]:
        home = np.array(row[3:], dtype=int)/int(row[1])
for row in data:
    away = np.array(row[3:], dtype=int)/int(row[1])
    if(rate > np.sum(home-away)):
        rate = np.sum(home-away) # 지역간의 인구비율 차이 갱신(차이가 가장 적은 지역 찾기위함)
        area = row[0] # 해당 지역의 이름
        result = away # 결과를 result에 저장
print(rate, area)
plt.figure(figsize=(10, 5), dpi=100)
plt.style.use('ggplot')
plt.plot(home, label=name)
plt.plot(result, label=area)
plt.rc('font', family='Malgun Gothic')
plt.legend()
plt.show()
```

이제 실제로 원하는 지역과 가장 인구 구조가 비슷한 지역을 구한다.

rate변수가 0에 가까울수록 가장 인구 구조가 비슷하다고 볼 수 있다. **(인구비율의 차가 가장 적으므로)**

<img src="https://user-images.githubusercontent.com/58063806/78647909-2d913380-78f6-11ea-9837-d68df31a48cb.JPG" alt="실행결과" width=80% />

하지만 위와 같이 원하던 것과 다른 결과가 나오게된다.

그 이유는 rate변수를 보면 알 수 있는데 이것이 음수가 되는 경우들이 있기 때문이다.

``` python
import csv
import numpy as np
import matplotlib.pyplot as plt
f = open('age2.csv')
data = csv.reader(f)
next(data)
data = list(data)
rate = 1 
name = input('인구 구조가 알고 싶은 지역의 이름(읍면동 단위)을 입력해주세요: ')
for row in data:
    if name in row[0]:
        home = np.array(row[3:], dtype=int)/int(row[1])
for row in data:
    away = np.array(row[3:], dtype=int)/int(row[1])
    if(rate > np.sum(abs(home-away)) and name not in row[0]): 
        # 음수값이 안나오도록 절대값, 알고자하는 지역은 제외
        rate = np.sum(abs(home-away)) 
        area = row[0] 
        result = away
print(rate, area)
plt.figure(figsize=(10, 5), dpi=100)
plt.style.use('ggplot')
plt.plot(home, label=name)
plt.plot(result, label=area)
plt.rc('font', family='Malgun Gothic')
plt.legend()
plt.show()
```

해결방법으로 각 연령별 인구비율 차를 구할때 **절대값을 취해서 음수가 나오는 것을 방지**한다.

또한 **알고자하는 지역이 또 나오는 것을 방지**하기 위해 해당 지역은 제외시킨다.

``` python
if(rate > np.sum(abs(home-away)) > 0):
```

전국에 **인구 구조가 완전히 똑같은 지역이 없다고 가정**했을때 위와 같은 방식으로도 코드를 작성할 수 있다. 

<img src="https://user-images.githubusercontent.com/58063806/78648077-721ccf00-78f6-11ea-8547-806a54df2b12.JPG" alt="실행결과" width=80% />
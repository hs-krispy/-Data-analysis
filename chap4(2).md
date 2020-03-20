## 지하철 시간대별 데이터

``` python
import csv
f = open('subwaytime.csv')
data = csv.reader(f)
for row in data:
    print(row)
```

**3번 인덱스까지는 지하철에 대한 정보**가 나오고 **4번부터는 4시~다음날 3시까지의 1시간동안의 시간**이 나옴 

<img src="https://user-images.githubusercontent.com/58063806/77179507-ea6c4d80-6b0b-11ea-8ddb-6822c657f125.JPG" alt="실행결과" width=100% />

### 출근 시간의 승하차 인원정보

이러한 데이터들을 이용하면 출근 시간에 얼마나 많은 인원들이 지하철을 타고 내리는지 알아볼 수 있다.

``` python
import csv
f = open('subwaytime.csv')
data = csv.reader(f)
next(data)
next(data)
result = []
for row in data:
    row[4:] = map(int, row[4:])
    # int()를 4번째 인덱스~마지막 인덱스(4시~다음날 3시까지의 1시간동안의 시간)에 적용 
    result.append(row[10]+row[12]+row[14])# 7+8+9시 탑승인원수, sum(row[10:15:2])로도 가능
    #result.append(sum(row[11:16:2])) 7+8+9시 하차인원수
import matplotlib.pyplot as plt
result.sort()
plt.style.use('ggplot')
plt.bar(range(len(result)), result)
plt.show()
```

map()함수 - 첫번째 인자에는 일괄 적용할 함수이름, 두번째 인자에는  함수를 적용할 데이터

<img src="https://user-images.githubusercontent.com/58063806/77179510-eb04e400-6b0b-11ea-9bc7-1dab91a890fa.JPG" alt="실행결과" width=60% />

<img src="https://user-images.githubusercontent.com/58063806/77179511-eb9d7a80-6b0b-11ea-8c0d-f5555508786c.JPG" alt="실행결과" width=60% />

### 시간대별 승하차 인원이 가장 많은 역 정보

특정 시간대에서 더 나아가 모든 시간대에서 승하차 정보를 이용할 수 있다.

 ``` python
import csv
f = open('subwaytime.csv')
data = csv.reader(f)
next(data)
next(data)
m = [0]*24
s = ['']*24
for row in data:
    row[4:] = map(int, row[4:])
    for i in range(24):
        a = row[i*2+4]# 각 시간대별 승차 데이터(4, 6, 8...)
       # b = row[(i+1)*2+3] 각 시간대별 하차 데이터(5, 7, 9...)
        if a >= m[i]:
            m[i] = a
            s[i] = row[3]+'('+str(i+4)+'시)' #보기 쉽게 시간까지 추가
import matplotlib.pyplot as plt
plt.bar(range(24), m)
plt.title('시간대별 승차인원이 가장 많은 역')
plt.xticks(range(24), s, rotation=90)# x축, rotation은 데이터들을 반시계방향으로 value만큼 회전
plt.style.use('ggplot')
plt.rc('font', family='Malgun Gothic')
plt.show()
 ```

ticks()함수 - 첫번째 인자에는 수치 리스트, 두번째 인자에는 첫번째 인자인 수치 리스트를 대체할 리스트

<img src="https://user-images.githubusercontent.com/58063806/77179495-e8a28a00-6b0b-11ea-9553-cd670d8de8f5.JPG" alt="실행결과" width=60% />

<img src="https://user-images.githubusercontent.com/58063806/77179500-e93b2080-6b0b-11ea-91c9-0bfd03a49648.JPG" alt="실행결과" width=60% />

### 시간대별 승하차 인원 추이

해당 시간대에 얼마나 많은 인원들이 타고 내리는지 한눈에 보기쉽게 표현할 수 있다.

``` python
import csv
f = open('subwaytime.csv')
data = csv.reader(f)
next(data)
next(data)
sin = [0]*24
sout = [0]*24
for row in data:
    row[4:] = map(int, row[4:])
    for i in range(24):
        sin[i] += row[i*2+4] # 모든 역에 대한 승차인원의 총합
        sout[i] += row[(i+1)*2+3] # 모든 역에 대한 하차인원의 총합
import matplotlib.pyplot as plt
plt.plot(range(24), sin, label='승차인원')
plt.plot(range(24), sout, label='하차인원')
plt.xticks(range(24), range(4,28))
plt.style.use('ggplot')
plt.legend()
plt.rc('font', family='Malgun Gothic')
plt.title('지하철 시간대별 승하차 인원 추이')
plt.show()
```

1e7은 1x10^7을 의미(1000만명)

<img src="https://user-images.githubusercontent.com/58063806/77179506-e9d3b700-6b0b-11ea-8d8d-b359c03154df.JPG" alt="실행결과" width=60% />

위의 그래프에서 출근시간대에는 7-9시에 승차 인원이 가장 많고, 8-9시에 하차 인원이 가장 많은 것

퇴근시간대에는 18-19시에 승차 인원이 가장 많고, 17-19시에 하차 인원이 가장 많은 것을 알 수 있다. 
## 지하철 유무임별 데이터

[대중교통 데이터 내려받기](https://pay.tmoney.co.kr/ncs/pct/ugd/ReadTrcrStstList.dev)에서 지하철 이용현황을 다운하고 '작업일시' 데이터 열을 삭제하고 csv파일로 변환

``` python
import csv
f = open('subwayfee.csv')
data = csv.reader(f)
for row in data:
    print(row)
```

<img src="https://user-images.githubusercontent.com/58063806/77044069-1ef3e280-6a02-11ea-92cc-63dac68b4a01.JPG" alt="실행결과" width=70% />

### 유임승차 비율이 가장 높은 역

**유임승차 비율 - 유임승차 인원/전체승차(유임+무임승차) 인원**

``` python
import csv
f = open('subwayfee.csv')
data = csv.reader(f)
next(data)
for row in data:
    for i in range(4, 8):
        row[i] = int(row[i])
    if row[6]==0:
        print(row)
```

무임승차 인원이 0인 역들이 있는지 확인해야한다.(**0으로 나누면 안됨**)

<img src="https://user-images.githubusercontent.com/58063806/77044073-1f8c7900-6a02-11ea-9364-877129551b7a.JPG" alt="실행결과" width=60% />

``` python
import csv
f = open('subwayfee.csv')
data = csv.reader(f)
next(data)
m = 0 # 최대 유임승차 비율을 저장할 변수
rate = 0 # 유임승차 비율을 저장할 변수
for row in data:
    for i in range(4, 8):
        row[i] = int(row[i])
    if row[6]!=0 and (row[4]+row[6])>10000:#전체승차인원이 10000명 넘는경우
        rate = row[4] / (row[4]+row[6])
        if rate >= m:
            m = rate
            station = row[3] # 유임승차 비율이 최대일때 역이름
            line = row[1] # 유임승차 비율이 최대일때 역의 호선을 알려줌
print(line, station, round(m*100, 2))
```

row[4]~row[7] - 차례로 각 역의 유임승차, 유임하차, 무임승차, 무임하차 정보 (**int형으로 바꾸어주어야함**)

<img src="https://user-images.githubusercontent.com/58063806/77044074-20250f80-6a02-11ea-96c8-3837ac98ce09.JPG" alt="실행결과" width=50% />

### 유무임 승하차 인원이 가장 많은 역

``` python
import csv
f = open('subwayfee.csv')
data = csv.reader(f)
next(data)
m = [0] * 4 # 0으로 초기화된 크기 4배열
station = [''] * 4 # ''로 초기화된 크기 4배열 
label = ['유임승차', '유임하차', '무임승차', '무임하차']
for row in data:
    for i in range(4,8):
        row[i] = int(row[i])
        if row[i] >= m[i-4]:
            m[i-4] = row[i]
            station[i-4] = row[3]+' '+row[1]
for i in range(0,4):
    print(label[i]+' : '+station[i], m[i])
```

유임승차부터 무임하차까지 각각의 정보들의 최댓값과 그 때의 역을 찾음

<img src="https://user-images.githubusercontent.com/58063806/77044066-1dc2b580-6a02-11ea-8a8f-528d80cbdd72.JPG" alt="실행결과" width=50% />

### 역들의 유무임 승하차 비율 (파이차트)

각각의 역들에 대한 데이터의 비율들이 한 눈에 들어와야하므로 파이차트가 적당

```python
import csv
import matplotlib.pyplot as plt
plt.rc('font', family='Malgun Gothic')
f = open('subwayfee.csv')
data = csv.reader(f)
next(data)
label = ['유임승차', '유임하차', '무임승차', '무임하차']
c=['#14CCC0', '#389993', '#FF1C6A', '#CC14AF'] #색상 지정
for row in data:
    for i in range(4,8):
        row[i] = int(row[i])
    plt.title(row[3]+' '+row[1])
    plt.pie(row[4:8], labels=label, colors=c, autopct="%.1f%%")# 소수점 한자리까지
    plt.savefig(row[3]+' '+row[1]+'.png')# row[3]+' '+row[1]+'.png'이 파일이름
    plt.axis('equal')
    plt.show()
```

savefig() 함수 - 그래프를 이미지로 저장함

아래와 같은 파이차트가 각 역마다 생성되서 컴퓨터에 저장된다.

<img src="https://user-images.githubusercontent.com/58063806/77545494-d6e72b00-6eed-11ea-9a33-1818bac6bbd9.JPG" alt="실행결과" width=50% />
## 기온 공공데이터

### 파일 불러오기 & 출력

```python
import csv #csv 모듈을 불러옴
f = open('seoul.csv', 'r', encoding='cp949') #csv파일을 open()함수로 열어서 f에 저장
data = csv.reader(f, delimiter=',')
#f를 reader()함수에 넣어 data라는 csv reader객체 생성
print(data)#data 출력
f.close()#파일 닫음
```

csv데이터를 읽는 코드이다.

```python
import csv
f = open('seoul.csv', 'r', encoding='cp949')
data = csv.reader(f, delimiter=',') #delimiter=','는 기본지정값이므로 생략이 가능
for row in data:
    print(row)
f.close()
```

<img src="https://user-images.githubusercontent.com/58063806/74665594-5b55d800-51e3-11ea-9df3-e71458eccd43.JPG" alt="1" width=40% height=40% />

다음과 같이 리스트의 형태로 결과가 출력

### next() 함수

```python
import csv
f = open('seoul.csv')
data = csv.reader(f)
header = next(data) 
#next() 함수는 첫번째 데이터 행을 읽어오면서 데이터의 탐색위치를 다음 행으로 이동시킴
print(header)
print()
for row in data :
    print(row)
f.close()
```

<img src="https://user-images.githubusercontent.com/58063806/74665600-5c870500-51e3-11ea-9681-52559c477e47.JPG" alt="2" width=40% height=40% />

다음과 같이 첫번째 데이터 행 출력후 데이터 탐색은 다음 행 부터 이루어지는 것을 알 수 있다.

### 서울의 최고온도 구하기

```python
import csv
max_temp = -999 #최고 기온 값을 저장할 변수
max_data = '' #최고 기온이 가장 높았던 날짜를 기록할 변수
f = open('seoul.csv')
data = csv.reader(f)
header = next(data)
for row in data :
    if(row[-1] == '') :
        row[-1] = -999
    row[-1] = float(row[-1]) #문자열 형식을 실수형으로 변환 후 다시 넣어줌
    if(max_temp < row[-1]) :
        max_temp = row[-1]
        max_date = row[0]
f.close()
print('기상 관측 이래 서울의 최고 기온이 가장 높았던 날은',max_date+'로,', max_temp,'도 였습니다.')
```

<img src="https://user-images.githubusercontent.com/58063806/74665601-5d1f9b80-51e3-11ea-8eae-270ecef5e7c4.JPG" alt="3" width=50% height=50% />

리스트의 형태이므로 인덱싱을 통해 특정값 구할수있음






## 인구 공공데이터

[행정안전부 홈페이지](http://27.101.213.4/index.jsp#)에서 csv파일 다운

``` python
import csv
f = open('age.csv')
data = csv.reader(f)
header = next(data)
print(header)
```

['행정구역', '2019년02월_계_총인구수', '2019년02월_계_연령구간인구수', '2019년02월_계_0세', ....]과 같이

**행정구역, 해당 기간 총 인구수, 해당 기간 연령구간 인구수에 이어 0~100세 이상의 연령별 인구수**가 나타난다.

``` python
import csv
f = open('age.csv')
data = csv.reader(f)
for row in data :
    if '서울특별시 구로구 신도림동(1153051000)' == row[0] :
        print(row)
```

행정구역이 '서울특별시 구로구 신도림동(1153051000)'에 해당하는 지역의 인구정보만 출력

``` python
if '신도림' in row[0] : # row[0]안에 신도림이 포함되면 출력
```

매번 일일이 다 치기에 어려움이 따르므로 위와 같이 사용가능

``` python
import csv
import matplotlib.pyplot as plt
plt.style.use('ggplot') #격자 무늬 스타일
f = open('age.csv')
data = csv.reader(f)
result = []
area = input('인구 구조가 알고 싶은 지역의 이름(읍면동 단위)을 입력해 주세요 : ')
for row in data :
    if area in row[0] :
        for i in row[3:] : #0~100세 이상의 인구수
            result.append(int(i.replace(',','')))
            # 정수형 변환을 위해 ,를 빈문자로 바꿔주어야함
plt.title(area + ' 지역의 인구 구조')
plt.rc('font', family = 'Malgun Gothic')
plt.plot(result)
plt.show()
```

area변수에 지역의 이름을 입력받아서 그 지역에 해당하는 인구 구조를 그래프로 표현

꺾은선 그래프로 표현 - 어떤 연령의 사람들이 많고 적은지 한눈에 알 수 있음

<img src="https://user-images.githubusercontent.com/58063806/75992214-ffa58180-5f3a-11ea-889a-427a554c4bc2.JPG" alt="실행결과" width=60% height=60% />

### 막대그래프

``` python
import matplotlib.pyplot as plt
plt.bar([0, 3, 2, 1, 6, 10], [1, 2, 3, 5, 6, 7])# 막대그래프를 표현(막대의 길이는 데이터의 크기)
plt.rcParams['axes.unicode_minus'] = False # 마이너스 기호 깨짐 방지
plt.show()
```

bar은 막대그래프를 표현하고, 첫번째 인자는 **막대를 표시할 위치**를 두번째 인자는 **막대의 높이**를 의미

<img src="https://user-images.githubusercontent.com/58063806/75992208-fe745480-5f3a-11ea-955c-c37c1de37eb0.JPG" alt="실행결과" width=60% height=50%/>

``` python
import csv
f = open('age.csv')
data = csv.reader(f)
result = []
for row in data :
    if '신도림' in row[0] :
        for i in row[3:] :
            result.append(int(i))
import matplotlib.pyplot as plt
plt.bar(range(101), result)
plt.show()
```

막대그래프 - 연령이 같은 사람들의 정보를 보다 정확히 파악가능, 성비를 기준으로 한다면 지역별 성비 확인 수월

<img src="https://user-images.githubusercontent.com/58063806/75992213-ff0ceb00-5f3a-11ea-8e33-329040f214e4.JPG" alt="실행결과" width=60% height=60% />

bar대신 **barh를 사용하면 수평 막대그래프** 사용가능

이때는 **range(101)이  y축이 되고, result가 x축**이 된다.
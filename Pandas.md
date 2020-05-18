## Pandas 라이브러리

파이썬을 활용한 데이터 분석에서 가장 많이 활용되는 라이브러리

Series - **1차원 배열 형태**의 데이터 구조

DataFrame - **2차원 배열 형태**의 데이터 구조

DataFrame은 행을 구분해주는 index와 열을 구분해주는 column으로 구성

인덱스를 별도로 지정해주지 않으면 디폴트는 정수

```  python
import pandas as pd
index = pd.date_range('1/1/2000', periods=8)
print(index)
```

날짜 형태로 된 8개의 인덱스 생성

<img src="https://user-images.githubusercontent.com/58063806/82233053-5d5a3f00-996a-11ea-8351-2a788c801c3c.JPG" alt="실행결과" width=70%/>

``` python
import pandas as pd
import numpy as np
index = pd.date_range('1/1/2000', periods=8)
df = pd.DataFrame(np.random.rand(8, 3), index=index, columns=list('ABC'))
df
# print(df['A'])와 같이 사용하면 A열에 해당하는 정보만 출력가능(Series 구조 형태로 출력)
```

위에서 생성한 index를 적용하고 column은 A, B, C로 적용해서 데이터 프레임 생성

<img src="https://user-images.githubusercontent.com/58063806/82233055-5df2d580-996a-11ea-9ea4-a7a05a334306.JPG" width=40%/>

```python
import pandas as pd
import numpy as np
index = pd.date_range('1/1/2000', periods=8)
df = pd.DataFrame(np.random.rand(8, 3), index=index, columns=list('ABC'))
df2 = df[df['B'] > 0.4]
# df2.T  데이터 프레임의 행과 열을 바꿔줌
```

마스크 기능을 이용해서 **B열의 값이 0.4보다 크다는 조건이 True인 데이터**로만 이루어진 데이터 프레임 df2 생성

데이터 프레임뒤에 .T를 붙여주면 행과 열을 바꿈

<img src="https://user-images.githubusercontent.com/58063806/82233057-5df2d580-996a-11ea-9871-534c9b81b154.JPG" alt="실행결과" width=50% />

```python
import pandas as pd
import numpy as np
index = pd.date_range('1/1/2000', periods=8)
df = pd.DataFrame(np.random.rand(8, 3), index=index, columns=list('ABC'))
df['D'] = df['A'] / df['B'] # A열의 값을 B열의 값으로 나눈 값을 D열에 저장
df['E'] = np.sum(df, axis=1) # 각 행의 값들을 더한 값을 E열에 저장
df = df.sub(df['A'], axis=0) # 전체 데이터를 A열의 값으로 뺌
df = df.div(df['C'], axis=0) # 전체 데이터를 C열의 값으로 나눔
df.to_csv('test.csv') 
df.head() # 많은 데이터 중 처음 5개의 데이터만 확인하고 싶을 때 사용
```

2차원 데이터일 경우 pandas에서는 기본적으로 **행 방향(↓)**을 축으로 계산

**axis = 0이면 행 방향, axis = 1이면 열 방향(→)을 축으로 설정**

to_csv() - 데이터 프레임을 csv파일로 저장

<img src="https://user-images.githubusercontent.com/58063806/82233044-5b907b80-996a-11ea-8fee-76241eb067b7.JPG" width=50%/>

<img src="https://user-images.githubusercontent.com/58063806/82233051-5cc1a880-996a-11ea-969d-0c48464f21d2.JPG" width=60%/>

<img src="https://user-images.githubusercontent.com/58063806/82233488-11f46080-996b-11ea-90e1-4eaf0458fde2.JPG" width=55%/>

<img src="https://user-images.githubusercontent.com/58063806/82233490-13258d80-996b-11ea-9e7a-69ecafc02795.JPG" width=55%/>
## Pandas를 이용한 인구 구조 분석

우선 각 연령대별 인구수를 총 인구수로 나눠서 비율로 환산시킴

``` python
import pandas as pd
df = pd.read_csv('age.csv', encoding='cp949', index_col=0)
df = df.div(df['총 인구수'], axis=0)  
del df['총 인구수'], df['연령구간인구수'] # 총 인구수와 연령구간인구수 열 삭제
name = input('원하는 지역의 이름을 입력하세요 : ')
a = df.index.str.contains(name) # 데이터 프레임의 인덱스 문자열에 원하는 문자열이 포함된 행 찾음
# True, False로 반환
df2 = df[a]
df2
```

<img src="https://user-images.githubusercontent.com/58063806/82474536-23be3b00-9b06-11ea-8fcb-56b459898f20.JPG" alt="실행결과" width=100% />

``` python
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('age.csv', encoding='cp949', index_col=0)
df = df.div(df['총 인구수'], axis=0) 
del df['총 인구수'], df['연령구간인구수'] 
name = input('원하는 지역의 이름을 입력하세요 : ')
a = df.index.str.contains(name)
df2 = df[a]
plt.rc('font', family='Malgun Gothic')
df2.T.plot() # 행의 정보들을 Y축으로 설정해서 그래프화
plt.show()
```

df2.T 출력

행과 열이 바뀐 것을 볼 수 있음

<img src="https://user-images.githubusercontent.com/58063806/82474537-23be3b00-9b06-11ea-86a1-9a38dea9a37e.JPG" alt="실행결과" width=30%/>

<img src="https://user-images.githubusercontent.com/58063806/82474539-2456d180-9b06-11ea-8f95-4085fa068493.JPG" width=50% />

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
df = pd.read_csv('age.csv', encoding='cp949', index_col=0)
df = df.div(df['총 인구수'], axis=0)  
del df['총 인구수'], df['연령구간인구수'] 
name = input('원하는 지역의 이름을 입력하세요 : ')
a = df.index.str.contains(name)
df2 = df[a]
x = df.sub(df2.iloc[0], axis=1) # 0 행 데이터(인구 비율)를 열 방향으로 뺌
y = np.power(x, 2) # 제곱
z = y.sum(axis=1) # 해당 지역과 인구 구조 유사도(숫자가 작을수록 유사함)
# print(z)
i = z.sort_values().index[:5] # 인구 구조가 가장 유사한 5개 지역
#print(df.loc[i])
df.loc[i].T.plot()
# 위의 코드들을df.loc[np.power(df.sub(df2.iloc[0],axis=1),2).sum(axis=1).sort_values().index[:5]].T.plot()로 변경가능
plt.rc('font', family='Malgun Gothic')
plt.show()
```

iloc은 **위치 정수를 기반으로 데이터에 접근**하는 방식

loc은 **label(레이블)을 기반으로 데이터에 접근**하는 방식

z(유사도) 출력

<img src="https://user-images.githubusercontent.com/58063806/82474541-24ef6800-9b06-11ea-9ec7-3fa82fe57595.JPG" width=30% />

df.loc[i] 출력

인구 구조가 가장 유사한 5개 지역의 인구 정보

<img src="https://user-images.githubusercontent.com/58063806/82474533-2325a480-9b06-11ea-8b3d-2b8a41f8c587.JPG" width=100% />

**그래프의 형태(인구 구조)가 비슷**하게 나오는 것을 볼 수 있음

<img src="https://user-images.githubusercontent.com/58063806/82474528-21f47780-9b06-11ea-93f2-0f5aba0c2730.JPG" width=50% />
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
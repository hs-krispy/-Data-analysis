## Numpy 라이브러리

numpy라이브러리 - 행렬이나 다차원 배열을 쉽게 처리할 수 있도록 지원하며 수치 계산을 위해 효율적으로 구현된 기능들을 제공

``` python
import matplotlib.pyplot as plt
import numpy as np
t = np.arange(0., 5., 0.2)
plt.plot(t, t, 'r--', t, t**2, 'bs', t, t**3, 'g^')
plt.show()
```

```python
import matplotlib.pyplot as plt
t = []
p2 = []
p3 = []
for i in range(0, 50, 2):
    t.append(i/10)
    p2.append((i/10)**2)
    p3.append((i/10)**3)
plt.plot(t, t, 'r--', t, p2, 'bs', t, p3, 'g^')
plt.show()
```

위 두개의 코드에서 아래와 같은 동일한 결과가 나오는데 numpy라이브러리를 사용한 코드는 반복문이 없어서

더 간결하게 보임

<img src="https://user-images.githubusercontent.com/58063806/77314665-70c1a300-6d49-11ea-8130-3634e78aa538.JPG" alt="실행결과" width=60% />

### Random

``` python
import numpy as np
print(np.random.choice(6, 10))
print(np.random.choice(10, 6, replace=False))
print(np.random.choice(6, 10, p=[0.1, 0.2, 0.3, 0.2, 0.1, 0.1]))
```

##### 실행결과

```
[2 3 4 0 0 4 3 4 0 5]
[4 7 2 1 9 6]
[3 0 3 5 3 3 5 3 5 2]
```

맨 위 부터 순서대로 

- 0~5까지의 랜덤한 수를 10개 뽑음
- 0~9까지의 중복없는 랜덤한 수를 6개 뽑음
- 0~5까지의 숫자에 각각 확률을 부여해서 10개를 뽑음

``` python
import matplotlib.pyplot as plt
import numpy as np
dice = np.random.choice(6, 1000000, p=[0.1, 0.2, 0.3, 0.2, 0.1, 0.1])
plt.hist(dice, bins=6)
plt.show()
```

아래와 같이 뽑는 숫자의 수를 늘려주면 확률대로 그래프가 나타남

<img src="https://user-images.githubusercontent.com/58063806/77314668-70c1a300-6d49-11ea-89e7-6bd0ba2d898b.JPG" alt="실행결과" width=60% />

```python
import matplotlib.pyplot as plt
import numpy as np
x = np.random.randint(10, 100, 200)# 10~100까지의 랜덤한 정수 200개 생성
y = np.random.randint(10, 100, 200)
size = np.random.rand(100)*100
plt.scatter(x,y,s=size,c=x,cmap='jet',alpha=0.7)
plt.colorbar()
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/77314671-715a3980-6d49-11ea-81c9-02521e878581.JPG" alt="실행결과" width=60% />

### Numpy array

``` python
import numpy as np
a = np.array([1,2,'3',4])
print(a)
```

numpyarray에는 **한 가지 타입의 데이터만 저장이 가능**하므로 위의 결과는 모두 문자타입으로 변환되어서`['1','2','3','4']`가 나옴

또한 배열에 **연산이나 함수를 적용시키면 배열의 모든 값들이 한꺼번에 계산**됨

``` python
import numpy as np
a = np.zeros(10)# 0으로 초기화된 크기가 10인 배열 생성
b = np.ones(10)# 1로 초기화된 크기가 10인 배열 생성
c = np.eye(3)# 3행 X 3열의 단위 배열 생성
print(a)
print(b)
print(c)
```

##### 실행결과

```
[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
[1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

.zeros()함수 - 인자로 받은 크기만큼 0으로 초기화된 배열을 생성

.ones()함수 - 인자로 받은 크기만큼 1로 초기화된 배열을 생성

.eye()함수 - 인자로 받은 크기*크기의 배열 생성(NxN배열)

**위 함수들은 0또는 1로 배열을 채우고 싶을때 유용함**

``` python
import numpy as np
print(np.arange(3))
print(np.arange(3,7))
print(np.arange(3,7,2))
print(np.linspace(1, 2, 11))
```

##### 실행결과

```
[0 1 2]
[3 4 5 6]
[3 5]
[1.  1.1 1.2 1.3 1.4 1.5 1.6 1.7 1.8 1.9 2. ]
```

- 0~2 까지 정수 생성
- 3~6 까지 정수 생성
- 3부터 2의 간격으로 6까지 정수 생성
- 1~2 까지를 11개의 구간으로 나눈 실수 생성

``` python
import matpltolib.pyplot as plt
import numpy as np
a = np.arange(-np.pi, np.pi, np.pi/10)
plt.plot(a, np.sin(a))
plt.plot(a, np.cos(a))
plt.plot(a+np.pi/2, np.sin(a))
# a배열에 모든 값에 π/2가 더 해지면서 sin함수의 평행이동을 의미함
plt.show()
```

<img src="https://user-images.githubusercontent.com/58063806/77314672-71f2d000-6d49-11ea-982b-496625caf41e.JPG" alt="실행결과" width=55% />

### Mask

``` python
import numpy as np
a = np.arange(-5, 5)# -5~4까지의 정수 생성
print(a<0)
print(a[a<0])
mask1 = abs(a)>3
mask2 = abs(a)%2==0
print(a[mask1+mask2])# mask1 or mask2를 만족하는 값 출력
print(a[mask1*mask2])# mask1 and mask2를 만족하는 값 출력
```

##### 실행결과

```
[ True  True  True  True  True False False False False False]
[-5 -4 -3 -2 -1]
[-5 -4 -2  0  2  4]
[-4  4]
```

mask는 배열내의 **몇 부분을 유지하거나 제어하기위해 사용**함

```python
import matplotlib.pyplot as plt
import numpy as np
x = np.random.randint(-100, 100, 1000)# -100~100까지의 랜덤한 정수를 1000개 생성
y = np.random.randint(-100, 100, 1000)
size = np.random.rand(100)*100
maks1 = abs(x) > 50
mask2 = abs(y) > 50
x = x[mask1+mask2]# x값이나 y값의 절댓값이 50보다 작거나 같은 값들을 제외
y = y[mask1+mask2]# x값이나 y값의 절댓값이 50보다 작거나 같은 값들을 제외
plt.scatter(x, y, s=size, c=x, cmap='jet', alpha=0.7)
plt.colorbar()
plt.show()
```

x값이나 y값의 절댓값이 50보다 작거나 같은 값들을 제외시켰으므로 가운데 부분이 뚫려있음

<img src="https://user-images.githubusercontent.com/58063806/77314663-6f907600-6d49-11ea-9726-07b97bbff98b.JPG" width=60% />
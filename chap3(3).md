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


# NAVER-BoostCamp-AI-Tech-TIL
<details>
<summary><b>WEEK1</b></summary>
<details>

<summary>Day1 Review</summary>


<span style="font-size:150%">**완료한 사항**</span>  


    🙂Github에 NAVER-BOOSTCAMP-AI-TECH 관련 TIL DAY 1 업로드  

    🙂python 기초 문법 30% 학습  

    🙂(피어세션) 데이터 전처리 100문제 중 chapter1 완료  

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃python 기초 문법 끝내기    

#  

<span style="font-size:150%">**새롭게 알게된 내용**</span>  

**1.**
기존에 할당된 변수 a에 대해서 아래와 같은 작업을 실행하는 경우
```python
a = [1,2,3]
b = a
```
b와 a는 같은 주소값을 가리키게 되어 a의 값을 수정 시 b의 값도 변하는 효과가 있다.


따라서 b에 단순히 a의 값을 copy 하고 싶으면
```python
b = a[:]
```
위에 해당하는 작업을 수행해야 한다.

***

**2.**
2차원 배열에서는 

     b=a[:]
와 같은 작업이 불가능하다.


따라서 
   
    import copy
        
내부의 deepcopy라는 함수를 이용하여 

    b = copy.deepcopy(a)

와 같은 작업을 수행해야 한다.
***    

#  

<span style="font-size:150%">**내일 목표**</span>  

    💪Numpy학습 진행  


#  

<span style="font-size:150%">🚩**DAY 1 소감**</span>

- 피어세션에서 팀원들과 같이 데이터 전처리 공부를 하기로 결정했다! 공부하기 좋은 내용을 팀원 한 분이 제시해주셔서 도움이 많이 될 것 같다.
- python 이나 컴퓨터의 기초가 되는 내용들을 학습했는데, 잘 안 다고 생각한 내용들이 생각보다 모르는 부분이 많아서 더욱 꼼꼼하게 공부해야겠다는 생각이 들었다. 
</details>

<details>

<summary>Day2 Review</summary>


<span style="font-size:150%">**완료한 사항**</span>  


    🙂python module & project와 관련된 내용까지 학습 완료  

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  


    🙃데이터 전처리 chapter 2


#  

<span style="font-size:150%">**새롭게 알게된 내용**</span>  

## 1. 모듈과 패키지를 만들었을 때 내부 함수가 잘 구현되었는지 확인하기
함수 패키지를 example.py 파일로 작성한 뒤 해당 파일에
```python
if __name__ == '__main__':
    print(...result...)
    print(...result...)
    print(...result...)
```
과 같이 작성하게 된다면, 파이썬 파일을 아래와 같이 터미널에서 실행했을 때

```python
import example
```
>> 아무것도 출력되지 않음

아무것도 출력되지 않는다.

하지만, 아래와 같이
```python
def d1():
    ...

def d2():
    ...
...
#if __name__ == '__main__':
print(...result...)
print(...result...)
print(...result...)
```
코드를 작성하고 
```python
import example
```
example.py를 import 하게 된다면
>> ...result...  
>> ...result...  
>> ...result...

와 같이 실행된다.

**만약 if __ name __ == '__ main __': 내부에 출력 예시값을 확인하고 싶다면, 터미널에서 아래와 같이 입력하시라**
```python
python example.py
```
>> ...result...  
>> ...result...  
>> ...result...

다음과 같이 if __ name __ == '__ main __': 안의 예시 코드들이 실행된다.

## 2. Call by object reference
파이썬의 함수에 인자를 넘길 때 ***객체의 주소***가 함수로 전달되는 방식으로 실행된다.

### (1) 객체의 주소가 함수로 전달되지 않는 경우 
```python
def swap(a,b):
    tmp = a
    a = b
    b = a
```
라는 함수를 아래와 같이 실행하게 된다면
```python
arr = [1,2,3,4,5]
swap(arr[0],arr[1])
print(arr)
```
>>[1 ,2 ,3 ,4 ,5]  

와 같이 출력됨을 알 수 있다.

### (2) 객체의 주소가 함수로 전달되는 경우
#### (2) - 1
```python
def swap_offset(location_1,location_2):
    tmp = arr[location_1]
    arr[location_2] = arr[location_1]
    arr[location_1] = tmp
```
라는 함수를 아래와 같이 실행하게 된다면
```python
arr = [1,2,3,4,5]
swap_offset(0,1)
print(arr)
```
>> [2 ,1 ,3 ,4 ,5]  

와 같이 arr의 주소값이 함수에 전달되어 arr의 값이 변화됨을 알 수 있다.

#### (2) - 2
```python
def swap_standard(list_name,location_1,location_2):
    tmp = list_name[location_1]
    list_name[location_2] = list_name[location_1]
    list_name[location_1] = tmp
```
라는 함수를 아래와 같이 실행하게 된다면
```python
arr = [1,2,3,4,5]
swap_standard(arr,0,1)
print(arr)
```
>> [2 ,1 ,3 ,4 ,5]

와 같이 arr의 주소값이 함수에 전달되어 arr의 값이 변화됨을 알 수 있다.

<U> 따라서 코드를 작성할 때 
1. 함수 내부에서는 외부와 같은 객체명을 사용해서는 안되며
2. 함수에 객체를 전달 받았을 때는 함수에서 해당 객체를 복사하여 사용한다.
</U>

&nbsp;

## 3. function type hint
아래와 같이 함수를 정의할 때
```python
def example(num1:str, num2:int) -> str:
    """_summary_

    Args:
        num1 (str): _description_
        num2 (int): _description_

    Returns:
        str: _description_
    """    
    ...

```
와 같이 def 함수명(파라미터 : 자료형) -> return type(return 값이 없을 때는 None으로 입력)의 형태로 함수에 입력하는 파라미터를 미리 지정해주는 것을 ***function type hint*** 라고 한다.

function type hint의 장점은  
1. 사용자에게 함수의 인터페이스를 명확히 알려줄 수 있다.  
2. 함수를 문서화 할 때 파라미터에 대한 정보를 명확히 알 수 있다.
3. 시스템의 안정성을 확보할 수 있다.
***

<span style="font-size:150%">**내일 목표**</span>  

    💪오늘 완료하지 못한 학습 정리  


#  

<span style="font-size:150%">🚩**DAY 2 소감**</span>

- 코어타임 내에 학습리뷰도 완료할 수 있도록 노력하자
- 피어세션 때 내가 겪은 에러에 대해서도 공유할 수 있도록 내용에 대해서 정리하자


</details>

<details>

<summary>Day3 Review</summary>
<span style="font-size:150%">**완료한 사항**</span>  


    🙂pythonic_code 학습 내용정리 완료

    🙂Matrix와 관련된 내용까지 학습 완료   

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃python_datastructure ~ matrix까지 학습정리
    

#  


<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span> 
# split & join

## split
### 개요
- string type의 데이터에 대해 특정값을 기준으로 구분지어 리스트에 저장할 때 사용
### 구현  
- <code class="language-plaintext highlighter-rouge">.split()</code>을 이용
- **unpacking도 가능** 
### 예시
```python
#공백 기준으로 나누기
ex_1 = "a b c d e f g h"
ex_1.split()  #['a','b','c','d','e','f','g','h']

#"k"를 기준으로 나누기
ex_2 = "akbkckdkekfkgkh"
ex_2.split('k')  #['a','b','c,'d','e','f','g','h']

#unpacking
ex_3 = "i like an apple"
a,b,c,d = ex_3.split() # a = 'i', b = 'like', c = 'an', d = 'apple' 
```

## join
### 개요  
- string type으로 구성된 리스트를 특정값을 중간에 합하여 하나의 문자열로 재구성 할 때 사용
### 구현 
-  <code class="language-plaintext highlighter-rouge">'특정값'.split(리스트명)</code>을 이용
### 예시
```python
# 단순 연결
ex_1 = ['i', 'like', 'an', 'apple']
result = ''.join(ex_1) #result = ilikeanapple

# k를 리스트 요소 사이에 추가하여 연결
ex_1 = ['i', 'like', 'an', 'apple']
result = 'k'.join(ex_1) #result = iklikekankapple

# 공백으로 연결
ex_1 = ['i', 'like', 'an', 'apple']
result = ' '.join(ex_1) #result = i like an apple
```
# list handling
### 개요  
- 리스트에 대한 다양한 handling 기법들을 다룬다.
- 세상에는 다양한 사람들이 작성한 코드가 존재하기에, 다양한 사용법에 대해 알 필요가 있다. 
### 예시
```python
# 1-1. for문 1개
# 어떤 교수님이 모기업 재직 중 해당 코드 작성법을 몰라 상사에게 깨졌다는 이야기가 있다.
a = [i for i in range(10)] # a = [0,1,2,3,4,5,6,7,8,9]


# 1-2. for문 1개 + 조건문
a = [i for i in range(10) if i>5] # a = [6,7,8,9]


# 2-1. for문 2개
a = "dog"
b = "cat"
result = [i+j for i in a for j in b] # ['dc', 'da', 'dt', 'oc', 'oa', 'ot', 'gc', 'ga', 'gt']


# 2-2. for문 2개 + 조건문
a = "dog"
b = "cat"
result = [i+j for i in a for j in b if a!='dog'] # result = [] , a가 'dog'가 아닌 경우에만 실행


# 2-3. 리스트 [] 안에 조건문이 if 면 for문 뒤에 작성해도 되지만, if else 구문으로 구성하려면 {(1)for문 앞에 작성 (2) 리스트에 입력할 변수를 조건문 앞뒤로 입력 }해야하는 것에 주의
a = "dog"
b = "cat"
result = [i+j if a!='dog' else i+j for i in a for j in b] # ['dc', 'da', 'dt', 'oc', 'oa', 'ot', 'gc', 'ga', 'gt']


# 3. 2 dimenstional array일 경우도 가능
a = "dog"
b = "cat"
#j에 대한 for문이 바깥에 존재하므로 바깥 for문으로 이해
# a 변수에 저장된 내용은 0번째 요소만 계속 반영되는 특징
result = [[i+j for i in a]for j in b] #[['dc', 'oc', 'gc'], ['da', 'oa', 'ga'], ['dt', 'ot', 'gt']]
```

# enumerate & zip
## enumerate
### 개요  
- 리스트 요소에 대해 차례대로 인덱스를 부여해주는 함수
- 문자열도 <code class="language-plaintext highlighter-rouge">.split()</code>을 이용하여 리스트로 변형해서 사용할 수 있다.
### 구현  
- <code class="language-plaintext highlighter-rouge">enumerate(리스트명)</code>
### 예시
```python
# 리스트일 경우
ex = ['a','b','c','d']
for i,j in enumerate(ex):
    print(i,j) # 0 'a';1 'b';3 'c';4 'd'

# 문자열일 경우
ex = "a b c d"
ex_dic = {i:j for i,j in enumerate(ex.split())} # {0: 'a', 1: 'b', 2: 'c', 3: 'd'}
```

## zip
### 개요  
- 리스트나 튜플 같은 시퀀스 데이터의 같은 오프셋에 있는 데이터를 함께 추출
### 구현  
- <code class="language-plaintext highlighter-rouge">zip(list1 , list2, ...)</code>
### 예시
```python
#ex1
a = ['d','o','g']
b = ['c','a','t']

for i in zip(a,b):
    print(i) # ('d', 'c');('o', 'a');('g', 't'), 튜플 형태로 묶어서 i에 저장

#ex2
a = ['d','o','g']
b = ['c','a','t']
result = [i+j for i,j in zip(a,b)] #['dc', 'oa', 'gt']
```


# lambda & map
## lambda
### 개요  
- 간단한 수식을 함수로 나타낼 용도로 사용
### 구현  
 - <code class="language-plaintext highlighter-rouge">lambda 입력인자1,입력인자2, ... : 계산식</code>

### 예시
```python
#ex1
function = lambda a,b : a*b
print(function(3,4)) #12

#ex2
print((lambda a,b : a*b)(3,4)) #12
```
## map
### 개요  
- 다중의 시퀀스 데이터에 대해 함수를 일괄적으로 적용할 수 있다
### 구현  
 - <code class="language-plaintext highlighter-rouge">map(함수명,시퀀스 데이터1, 시퀀스 데이터2, ...)</code>

### 예시
```python
function = lambda a : a**2
print(list(map(function,[1,2,3,4]))) #[1, 4, 9, 16]
```
# iterator & generator
## iterator
### 개요  
- 시퀀스 데이터에서 자료를 순서대로 탐색할 때 쓰인다.
### 예시
```python
#1. 일반적으로 사용되는 경우
ex = ['cat','dog','pig']
for animal in ex:
    print(animal) # 'cat';'dog';'pig'

#2. 1번에서 구동될 때 파이썬 내부
#iter()함수를 이용하여 iterator를 할당하고 포인터처럼 next()함수를 이용하여 다음 요소의 주소값으로 iterator 이동
ex = ['cat','dog','pig']
iter_obj = iter(ex)
print(next(iter_obj))
print(next(iter_obj))
print(next(iter_obj))
```

## generator
### 개요  
- 메모리에 효율적인 코딩을 할 수 있다.
- 따라서 대용량 데이터 처리에 많이 쓰인다.
- 파일 데이터를 처리할 때도 많이 쓰인다.
### 예시
```python
from sys import getsizeof
#iterator
ex_iter = [i for i in range(1000)]
#generator
ex_gener = (i for i in range(1000))
ex_gener = list(ex_gener)

print(getsizeof(ex_iter)) #9016
print(getsizeof(ex_gener)) #8536
# generator가 iterator에 비해 메모리 할당량이 적다.
```

# asterisk
### 개요  
- 함수 파라미터의 개수가 정해지지 않았을 경우 사용
- asterisk는 *을 의미(사전적 의미로 정말 별표를 의미한다.)
- 곱셈이나 제곱, 가변인자에 사용한다.
- **현재 다룰 내용은 가변인자의 경우이다**

### 예시
```python
# 가변인자
def ex(*arg):
    return sum(arg)
print(ex(1,2,3,4,5)) #15
print(ex(1,2,3,4,5,6,7,8,9,10)) #55

# 키워드 가변인자
# 정해지지 않은 개수의 키워드 인자를 받을 수 있다. 
def ex(**arg):
    return arg
print(ex(a = 1,b =2, c =3)) #{'a': 1, 'b': 2, 'c': 3}
```


### unpacking container
- tuple이나 dictionary 앞에 asterisk를 붙여서 함수로 넘겨주게 되면 unpacking이 일어난다.
```python
# 가변인자
lst = ([1,2],[3,4],[5])
print(*lst) # [1,2] [3,4] [5]

# 키워드 가변인자
# 주의사항 : dic의 키 값과 함수의 파라미터 변수명이 같아야 적용되는 것 같다.
def ex(a,b,c):
    print(a,b,c)
dic = {'a': 1, 'b': 2, 'c': 3}
ex(dic) # 1 2 3

```
#
<span style="font-size:150%">**내일 목표**</span>  

    💪오늘 완료하지 못한 학습 정리  

    💪과제와 퀴즈 완료하기

#  

<span style="font-size:150%">🚩**DAY 3 소감**</span>

- 피어세션에서 다양한 사람들을 만나볼 수 있어서 재미있는 시간이었다.
- 다른 분들에 비해 진도가 느린 것 같아 빠름과 꼼꼼함이 공존할 수 있는 학습 방법을 찾아야 할 것 같다.

</details>


<details>

<summary>Day4 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  


    🙂베이즈 통계학까지 학습 완료  

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃AI Math 관련 수강한 강의 퀴즈 & 과제



#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

### 경사하강법
- 스칼라의 경우 경사하강 학습 종료 조건으로 gradient의 값에 **절댓값**을 취해준 후 비교한다.  
<U>하지만 벡터일 경우 **norm**을 취해준 후 비교한다</U>

- 위의 이유는 절댓값의 개념에 대해 생각해보면 이해가 가능한데, 절댓값은 스칼라 값의 원점으로부터의 거리 , norm1은 벡터에 대한 원점으로부터의 거리이기 때문에 스칼라와 벡터간의 gradient의 종료조건에 대한 설정의 차이가 존재한다.

### 확률적 경사하강법
- convex(볼록)한 모형일 때는 GD이용
- Non-convex(볼록하지 않은) 모형일 때는 SGD 이용
- <U>SGD를 이용할 때는 미니배치 사이즈에 대한 고려도 필수적이다.</U>

### softmax vs one-hot
- softmax는 주로 학습에 이용되는 함수  
- one-hot은 주로 추론에 이용되는 함수
    - 주어진 값중에 가장 큰 성분만 찾아서 확인하기 때문에 추론 시 효율성을 높인다.

### 확률론
- 데이터의 원래 분포 D에 대해서 사전에 알 수는 없다.
- 따라서 D가 원래 이산형이었다 하더라도 연속형으로 모델링 할 수 있는 것이다.
- 모델링의 시작은 주어진 데이터를 보고 **추론**하는 것이다.

### 몬테카를로 샘플링
- 주어진 데이터에 대한 기댓값을 알고 있을 때 이산인지 연속인지 모른다? -> 몬테카를로 샘플링 쓰세요~




#
<span style="font-size:150%">**내일 목표**</span>  

    💪오늘 완료하지 못한 학습 정리  

    💪퀴즈 완료하기

#  

<span style="font-size:150%">🚩**DAY 4 소감**</span>

- 피어세션에서 벡터와 GD에 대해 학습한 부분을 공유해주신 캠퍼분이 계신데 상당히 자세히 다뤄주셔서 스스로 학습한 내용이 다시 정리되는 느낌을 받았다. 
- 수식이 전부 이해는 가지 않았지만, 왜 이런 모델을 사용하고 특정 상황에서 어떤 방법론들이 있는지에 대해 학습할 수 있는 시간이었다.



</details>

<details>

<summary>Day5 Review</summary>
<span style="font-size:150%">**완료한 사항**</span>  


    🙂  

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃



#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   




#
<span style="font-size:150%">**주말 목표**</span>  

    💪WEEK1 심화과제 풀어보기 

#  

<span style="font-size:150%">🚩**DAY 5 소감**</span>


</details>

<details>

<summary>WEEK1 Review</summary>


<span style="font-size:150%">**피어세션 정리**</span>    
- 첫 주차였던 만큼 팀원분들에 대해 많이 알진 못했지만, 다들 열정이 가득하신 분들이라 학습에 대한 동기부여를 많이 받을 수 있었다.  
- 학습한 내용을 서로 공유하며 내가 정확하게 짚고 넘어가야 할 부분을 알 수 있었다. 혼자 공부하며 모르는 부분과 새로 알게된 부분을 적극적으로 공유하려고 노력해야겠다는 느낌을 받았다.

<span style="font-size:150%">**학습회고**</span>  
- python 기초부분에서 생각보다 부족한 부분이 많다고 느꼈다. 때문에 이 부분을 자세히 공부한다고 학습 진도가 밀렸던 1주차였는데, 2주차에는 전반적인 내용을 숙지 후 모르는 내용을 심도 있게 공부하는 방향으로 학습 계획을 세우는 것이 필요할 것 같다.
- AI에서 전반적으로 수학적인 개념이 어떻게 쓰이는지 정도만 알고 넘어갔다. 경사하강법과 베이즈 통계학까지는 자세한 수식을 이해완료 했지만, CNN과 RNN은 개인적으로 추가학습이 필요함을 느꼈다.
- LSTM과 GRU에 대한 선행학습으로 CNN과 RNN에 대한 추가학습이 필요할 것 같다.
</details>

</details>

<details>
<summary><b>WEEK2</b></summary>

<details>

<summary>Day6 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  


    🙂  chapter 1 수강완료

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃  기본 과제 1
    🙃  자세히 짚고 넘어갈 학습 내용 정리



#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

### view vs reshape
    view
    - tensor가 메모리에 연속적으로 존재할 때 사용 가능
    - tensor의 메모리가 연속적으로 존재하지 않을 때는 copy하지 않고 실행이 불가능하다.
    - copy하지 않기 때문에 빠르다.

    reshape
    - tensor가 메모리에 연속적으로 존재하지 않아도 사용 가능
    - tensor의 메모리가 연속적으로 존재하지 않을 때는 tensor를 copy하여 차원을 변경하고 메모리에 저장한다.
    - copy할 경우 느리다.


### squeeze
 - 설정값이 없을 때는 차원이 1인 차원을 없앤다.
 - 제거할 차원을 설정해주면 해당차원을 제거한다. 

 ```python
 a = torch.rand(3,1,5)
 a = a.squeeze() # [3,1,5] -> [3,5]

 b = torch.rand(4,5,5,4)
 b = b.squeeze(dim = 2) # [4,5,5,6] -> [4,5,4]
 ```
### unsqueeze
 - squeeze와는 반대의 개녕으로 차원이 1인 차원을 만들어준다.
 - 추가할 차원의 위치를 반드시 설정해주어야 한다.

 ```python
a = torch.rand(3,1,5)
a = a.unsqueeze(dim = 1) # [3,1,5] -> [3,1,1,5]
 ```
### fill_
- 주어진 tensor를 지정한 값으로 채우는 메소드

```python
a = torch.rand(2,3).fill_(3)
a # [[3,3,3],[3,3,3]]
```

### mm vs matmul
    mm
    - 2D 행렬곱셈 연산에서 쓰인다.
    - 벡터연산은 지원하지 않는다.
    - broadcasting을 지원하지 않는다. -> debug 에서 유리함

    matmul
    - mm 보다 포괄적인 형태의 행렬 곱셈 연산에서 쓰인다.
    - broadcasting을 지원한다. -> debug에서 불리함
    
### __get_item__
 - 인스턴스를 리스트나 딕셔너리로 취급이 가능하게 만드는 함수
 - 따라서 for loop이나 in과 같은 연산도 가능하다
 - 해당 파일에서는 parse_config.py파일에 구현되어 있으며, 따라서 config 인스턴스에 딕셔너리와 같이 접근이 가능하다.

#
<span style="font-size:150%">**내일 목표**</span>  

    💪기본과제 1 마무리하기

#  

<span style="font-size:150%">🚩**DAY 6 소감**</span>  
- 과제가 생각보다 오래걸려서 당황스러웠음
- 학습정리를 매일 + 과제는 추가적인 사항으로 다뤄야겠다는 생각
- 생각보다 기초가 많이 부족함을 느꼈다.

</details>


<details>

<summary>Day7 Review</summary>
<span style="font-size:150%">**완료한 사항**</span>  


    🙂  chapter 2까지 완강

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 Day7 review
    🙃 기본과제1 hook & apply



#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

### nn.module
 - 딥러닝을 구성하는 Layer의 base class

### nn.parameter
 - nn.module 내에서 attribute가 될때 require_grad = True로 지정
 - nn.parameter의 텐서 내용을 Tensor로 선언해도 값은 같게 나옴
 - Tensor로 선언했을 때와 차이는 module 인스턴스를 호출한뒤 parameters()로 iteration 했을 때 값이 보이지 않는것
 - Tensor로 선언 시 값이 보이지 않는 이유는 AutoGrad의 대상이 아니기 때문

### Backward
- Foward(y_hat)와 실제 값 간의 차이에 대한 미분 수행

#
#
### class Dataset 
 - Dataset은 각 함수에 따라 데이터를 어떻게 가져올 것인가를 지정해주는 class
 - 모든 데이터는 생성 시점에 처리하는 것이 아니라 학습에 필요한 시점에 transform이라는 함수를 통해 처리
 - 최근에는 HuggingFace 등 표준화된 라이브러리 사용


### class DataLoader
 - Data의 Batch를 생성(여러개의 데이터를 한번에 묶어서 전달)
 - GPU에 Feed하기 전 DataLoader를 통해 데이터를 변환하여 전달
 - 파라미터인 collate_fn의 경우 variable length(가변 길이) 데이터의 가변 인자 부분에 대한 padding을 적용하고 싶을 경우 사용된다.



#
<span style="font-size:150%">**내일 목표**</span>  

    💪chapter 3 강의 완료
    💪기본 과제 2 완료

#  

<span style="font-size:150%">🚩**DAY 7 소감**</span>
 - oop에 대한 부분이 확실히 부족한 것 같아서 oop 기초에 대한 부분을 실제 코딩을 통해서 더 탐구해볼 필요가 있어보인다.
 - 기본 과제 1을 진행하며 PyTorch 공식 문서들을 서칭해봤는데 익숙하지 않아서 애를 먹었다. 하지만 문서들을 읽어보면 쉽게 해결되는 문제가 몇 있었는데, 확실히 PyTorch 공식 문서를 잘 읽어보는 습관을 가져야겠다.

</details>

<details>

<summary>Day8 Review</summary>
<span style="font-size:150%">**완료한 사항**</span>  


    🙂 기본 과제 1
    🙂 chapter3 강의 수강 완료 

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 기본 과제 2



#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

### Model Saving
#### model.save()으로 model saving이 가능하다.
- 학습 결과를 저장하기 위한 함수이다.
- 2가지 방법으로 저장이 가능하다.
    - 모델의 형태
    - 파라미터
- Early Stopping을 위해 학습 중간 과정의 결과를 저장한다.
- orderded dict 형태로 저장된다.
#### state_dict()
 - 모델 파라미터를 표시해주는 함수
 - 이 함수를 model.state_dict() 형식으로 모델에 적용한 후 torch.save()에 인자로 넣어주게 되면 파라미터 상태를 확인가능하다.
 - 'pt'라는 확장자를 사용하여 파일을 저장한다.

#### load_state_dict()
- 저장된 파라미터를 불러오고 싶을 때 이용하는 함수

### check point     
- 학습의 중간 결과를 저장하여 최선의 결과를 선택
- Early Stopping을 사용할 때 유용함
- epoch, loss, metric을 함께 저장

### pretrained model
- 다른 데이터셋으로 만든 모델을 현재 데이터에 적용
- pretrained model 활용 시 모델의 일부를 frozen 시킴
    - frozen이란, 특정 Layer에 해당하는 기본 파라미터 값들을 유지한 채로 뒷부분만 파라미터를 업데이트 해주는 기법

### Monitoring tools
- WandB(Weight and Bias)
- PyTorch TensorBoard


#
<span style="font-size:150%">**내일 목표**</span>  

    💪 chapter 4 완강하기

#  

<span style="font-size:150%">🚩**DAY 8 소감**</span>
- 강의 내용 정리를 조금 더 세밀하게 해야할 필요성이 있음
- 추후에 해당 부분 다시 강의를 들으며 부족한 부분을 보강할 필요가 있다.
</details>

<details>

<summary>Day9 Review</summary>
<span style="font-size:150%">**완료한 사항**</span>  


    🙂 chapter4 강의 수강 완료 

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 기본 과제 2
    🙃 Day 8, Day 9 내용정리


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

### Model Parallel
- 모델을 병렬처리하여 나누는 것

### Data Parallel
- 데이터를 나눠서 GPU에 할당 후 결과의 평균을 구함
- Minibatch와 유사하며 간단히 얘기하면 minibatch를 한번에 여러 GPU에서 수행한다고 할 수 있다.
    - 문제점
        - 하나의 GPU에 연산이 몰려서 처리되는 경우가 있다.
        - 이러한 현상 때문에 Batch 사이즈가 감소하고 GIL(Grobal Interpreter Lock)의 문제로 이어진다.

### Distributed Data Parallel
- 각 CPU마다 process를 생성 후 개별 GPU에 할당
- CPU를 각 GPU마다 할당해줘서 코디네이트 할 GPU가 필요없어짐 -> GPU 병목현상이 덜 발생

### Hyperparameter Tuning
- grid와 random 방법이 있으며 최근에는 베이지안 기법인 BOHB가 주로 쓰임
- Ray와 같은 ML/DL의 병렬 처리를 위해 개발된 모듈이 있고 멀티노드 멀티프로세싱을 지원한다.


#
<span style="font-size:150%">**내일 목표**</span>  

    💪 Day 8, Day 9 내용정리
#  

<span style="font-size:150%">🚩**DAY 9 소감**</span>
- 손으로 필기해서 다시 옮겨적는 방식 말고 강의를 들으면서 바로 타이핑을 쳐서 기록하자. 시간 단축.

</details>

<details>
<summary>Day10 Review</summary>
<span style="font-size:150%">**완료한 사항**</span>  


    🙂 Day 8, Day 9 내용정리
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 심화 과제


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   



#
<span style="font-size:150%">**내일 목표**</span>  

    💪 Week2 내용 보충 및 review
#  

<span style="font-size:150%">🚩**DAY 10 소감**</span>


</details>

<details>

<summary>WEEK2 Review</summary>


<span style="font-size:150%">**피어세션 정리**</span>    
- 과제나 학습 내용에 관련해서 가볍게 이야기하고 정리하는 시간을 주로 가졌던 것 같다. 과제를 해결하기 위해 구글링을 하면서 이게 맞나? 싶은 상황을 팀원들과 공유했는데, 몰랐던 부분이 더욱 명확해진 것도 있었고 나만 모르는 것이 아니라는 자괴감도 덜 들게 되어서 동료들과 얘기하며 내가 가진 불안감들을 해소할 수 있는 시간이었다.
- 지난 주에 계획했던 데이터 전처리 문제 풀기는 제대로 진행되지 않았지만, 정해진 커리큘럼을 잘 해결하도록 팀원들과 학습내용과 과제 진행상황에 대해 가볍게 공유하는 방식으로 운영이 되어도 괜찮겠다는 느낌을 받았다.

<span style="font-size:150%">**학습회고**</span>  
- nn.module을 학습하며 어려움을 겪었는데 내가 생각한 어려움을 겪은 이유는 OOP에 대한 개념이라고 생각한다. 또한 이 부분은 단기간에 받아드리기 어렵다고 개인적으로 생각해서 꾸준히 OOP에 남아 있는 빈칸들을 채워넣어가는 것이 필요하다는 생각이 들었다.
</details>


</details>



<details>

<summary><b>WEEK3</b></summary>

<details>  
<summary>Day11 Review</summary>  
  
<span style="font-size:150%">**완료한 사항**</span>  


    🙂 MLP 내용정리
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 optimization 내용정리


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[Multi-Layer Perceptron](./DL/Multi_Layer_Perceptron)

###


#
<span style="font-size:150%">**내일 목표**</span>  

    💪 CNN, RNN 정리
    💪 기본과제 1,2,3 완료
#  

<span style="font-size:150%">🚩**DAY 11 소감**</span>


</details>

<details>
<summary>Day12 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  


    🙂 CNN, RNN 내용 정리
    🙂 과제 4
    🙂 optimization 내용정리
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 과제 5


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

- [Optimization](./DL/Optimization.md)
- [CNN](./DL/CNN.md)  
- [RNN](./DL/RNN.md)


###


#
<span style="font-size:150%">**내일 목표**</span>  

    💪 transformer 내용 정리
#  

<span style="font-size:150%">🚩**DAY 12 소감**</span>


</details>

<details>
<summary>Day13 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  


    🙂 transformer
    🙂 generative model
    🙂 과제 5
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 RNN 내용 정리 보강(LSTM, GRU)
    🙃 transformer 내용 정리
    🙃 generative model 내용 정리

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   




###


#
<span style="font-size:150%">**내일 목표**</span>  

    💪 심화과제 도전
    💪 transformer 내용 정리
    💪 RNN 내용 정리 보강(LSTM, GRU)
    💪 generative model 내용 정리
#  

<span style="font-size:150%">🚩**DAY 13 소감**</span>


</details>

<details>
<summary>Day14 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  


    🙂 transformer 내용 정리
    🙂 심화과제
    🙂 RNN 내용 정리 보강(LSTM, GRU)
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 generative model 내용 정리

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

- [Transformer](./DL/Transformer.md)

###


#
<span style="font-size:150%">**내일 목표**</span>  

    💪 generative model 내용 정리(GAN,VAE,AAE,Auto regressive model)
#  

<span style="font-size:150%">🚩**DAY 14 소감**</span>


</details>

<details>
<summary>Day15 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  



        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   



###


#
<span style="font-size:150%">**내일 목표**</span>  

#  

<span style="font-size:150%">🚩**DAY 15 소감**</span>


</details>


<details>

<summary>WEEK3 Review</summary>


<span style="font-size:150%">**피어세션 정리**</span>    
- 이번 주차에는 과제 리뷰와 수업 내용 리뷰를 진행했다. 과제를 진행하며 모르고 넘어갔던 부분이나 애매하게 알던 부분을 보충하는 시간을 가질 수 있었다. 특히 transformer에 대해서 팀원들한테 설명할 때 분명 완벽하게 이해했다고 생각했지만, 전날 공부했던 내용임에도 불구하고 팀원들이 이해할 수 있도록 설명하지는 못했던 것 같다. 공부한 것을 바로 정리하는 습관과 빠르게 정리해놓는 방법을 익혀야할 필요를 느꼈다.

<span style="font-size:150%">**학습회고**</span>  
- 운이 좋게도 이번 주 강의와 관련된 내용의 책을 한 권 가지고 있어서 지난 주말에 미리 내용을 가볍게 훑어봤다. 확실히 강의를 들을 때 내용 이해가 빨라서 지난 주 보다 수월하게 학습할 수 있었다. 여기서 느낀 점은 같은 내용을 계속해서 다시 봤을 때 받아들이는 시야가 넓어진다는 것이다. 모르는 내용을 계속 붙잡기 보다 모르더라도 일단 넘어가고 다시 돌아와서 반복 학습했을 때 효율이 더 늘어나는 것을 알 수 있었다.
- 학습 내용 정리를 할 때 chatgpt를 활용하면 효율이 늘어나는 것을 알 수 있었다. 타자가 느린편이기도 하고 배운 내용에 대해서 구조화가 잘 안됐을 때 chatgpt를 활용하면 스스로의 효율을 높일 수 있는 것 같다. 마스터 클래스에서 chatgpt라는 키워드는 꼭 한번씩 나오는 것 같고 이를 활용하는 능력이 중요시 되는 만큼 학습 능률을 키우기 위해서 chatgpt를 잘 활용하는 능력을 키워야 할 것 같다.  
</details>

</details>

<details>
<summary><b>WEEK4</b></summary>

<details>
<summary>Day16 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  

    🙂 강의 4강까지 내용 정리
    🙂 과제1 절반 완성
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[RecSys Concept](./RecSys/RecSys_Concept.md)  
[Collaborative Filtering](./RecSys/Collaborative_Filtering.md)

###


#
<span style="font-size:150%">**내일 목표**</span>  
    
    💪 과제1 끝내기
    💪 5 ~ 6강 듣고 내용 정리
    💪 RecSys Concept 이미지 자료 첨부 및 복습
    💪 Collaborative Filtering 이미지 자료 첨부 및 복습
#  

<span style="font-size:150%">🚩**DAY 16 소감**</span>
- 내가 하고 있는 일 자체를 사랑하면 그 자체로 동기부여가 된다는 이야기를 들었는데 실제로 그런 것 같다. RecSys 트랙별 강의를 처음 듣게된 날이었는데 흥미로운 내용이었고 기존에 애매하게 알고 있던 부분을 매꿔주는 느낌이라 즐겁게 학습할 수 있었다.
- 여전히 시간관리는 어렵다.. 나는 여유롭지 않다는 생각을 계속 가지고 있어야겠다.

</details>

<details>
<summary>Day17 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  

    🙂 과제1 끝내기
    🙂 강의 5강 완료
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 강의 6강
    🙃 Item2Vec ANN 이론 정리와 논문 읽어보기

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[Item2Vec](./RecSys/Item2Vec.md)

###


#
<span style="font-size:150%">**내일 목표**</span>  
    
    💪 강의 6강 완료하기
#  

<span style="font-size:150%">🚩**DAY 17 소감**</span>  

- 공부한 내용을 조금 더 구조화 할 필요가 있을 것 같다. 전체를 보고 세부화 시키는 과정이 필요한 것 같다.  

</details>

<details>
<summary>Day18 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  

    🙂 강의 6강
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  

    🙃 과제 2
    🙃 NCF, DNN, CDAE 논문 읽어보고 내용 정리

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[DL_in_RecSys](./RecSys/DL_in_RecSys.md)

###


#
<span style="font-size:150%">**내일 목표**</span>  
    
    💪 과제 2 완료하기
#  

<span style="font-size:150%">🚩**DAY 18 소감**</span>


</details>

<details>
<summary>Day19 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  

        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   



###


#
<span style="font-size:150%">**내일 목표**</span>  
    
    💪 
#  

<span style="font-size:150%">🚩**DAY 19 소감**</span>


</details>

<details>
<summary>Day20 Review</summary>

<span style="font-size:150%">**완료한 사항**</span>  

    🙂 
        
#      
  
  
<span style="font-size:150%">**완료하지 못한 사항**</span>  


#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   



###


#
<span style="font-size:150%">**내일 목표**</span>  
    
    💪 
#  

<span style="font-size:150%">🚩**DAY 20 소감**</span>

</details>

<details>

<summary>WEEK4 Review</summary>


<span style="font-size:150%">**피어세션 정리**</span>    
- 지난 주 내용을 복습하는 차원에서 한명씩 한 파트를 맡아서 설명하는 시간을 가졌다. 내용을 공부할 당시에는 다 이해하고 넘어갔던 내용들인데 설명을 하기에는 어려움이 있었다. 그레도 다행히 학습 정리를 해놓은 덕분에 많은 부분이 머릿속에 남아있어서 설명을 준비하는데 오랜시간이 걸리진 않았다. 다른 캠퍼들의 발표를 들으면서도 기존에 제대로 짚고 넘어가지 못한 부분에 대해서도 알게 되었고 다들 열심히 학습한 것이 보여서 더욱 동기부여가 됐던 시간이었다.

<span style="font-size:150%">**학습회고**</span>  
- 내용의 이해가 쉬웠던 반면에 구조화하기가 어려운 내용인 것 같다. 어떤 경우엔 어떤 모델을 쓰고 각 모델이 어떤 케이스에 쓰이는지 아직까지 정리가 제대로 안된 것 같다. 이론 하나하나에 치중하는 것도 필요하지만 전체적인 내용을 한번 그려보고 학습해야겠다. 
</details>

</details>


<details>
<summary><b>WEEK5</b></summary>

<details>
<summary>Day21 Review</summary>

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[GNN_in_RecSys](./RecSys/GNN_in_RecSys.md)


</details>

<details>
<summary>Day22 Review</summary>

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[Context-aware_Recommendation](./RecSys/Context-aware_Recommendation.md)


</details>

<details>
<summary>Day23 Review</summary>

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[DeepCTR](./RecSys/DeepCTR.md)


</details>

<details>
<summary>Day24 Review</summary>

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   

[Bandit_Recommendation](./RecSys/Bandit_Recommendation.md)


</details>

<details>
<summary>Day25 Review</summary>

#  
<span style="font-size:150%">**자세히 짚고 넘어갈 학습 내용**</span>   



</details>

<details>
<summary>WEEK5 Review</summary>


<span style="font-size:150%">**피어세션 정리**</span>    
- 4주차와 동일하게 지난 주차에 배웠던 내용에 대한 리뷰를 진행했다. 공부했던 내용을 직접 피어들에게 설명하기 위해 준비하는 과정과 설명하는 과정 속에서 배울게 많았던 것 같다. 그리고 피어들이 어떻게 학습했는지도 알 수 있었다. 여기서 깨달았던 포인트는 주체적으로 내용을 더 딥하게 파보는 활동이 중요하다는 것이다. 추가적인 내용들을 더 배우려고 하는 것들이 쌓여서 실력이 되는 것을 피어들을 보고 많이 느낄 수 있었다.

<span style="font-size:150%">**학습회고**</span>  
- 생각보다 학습 정리를 많이 진행하지 못했던 것 같다. 다음 주 프로젝트 주간을 앞두고 더 열심히 했었어야 했는데 많은 목표를 잡는 바람에 오히려 역효과가 났던 것 같다. 소화해낼 수 있는 범위를 목표로 설정하는 것도 중요한 부분인 것 같음을 느낄수 있었다.
</details>

</details>

</details>

<details>
<summary><b>Level1 Project Review</b></summary>


<span style="font-size:150%">**(부족함을)느낀점**</span>    
- EDA
    - DataFrame
        - 데이터프레임 기능을 구글링하는 빈도가 너무 많아서 시간 소요가 너무 많음
    - 데이터에 대한 이해(데이터 리터러시)
        - 기본적인 null값 탐색에 대한 파이프라인이 머릿속에 떠오르지 않음
        - 데이터 특성(대소문자, 카테고리컬 데이터, 연속형 데이터 등)에 대한 기초적인 EDA에 대한 부분을 확인하지 않음(기초 개념 부족)
        - 어떤 분포를 쓰면 데이터에 대한 특성을 한눈에 볼 수 있는지에 대한 이해가 부족(데이터의 통계적 특성 파악 능력 부족)
    - 시각화
        - 시각화 툴을 다루는 코딩 스킬 부족
        - 어떤 시각화 툴을 쓰면 적절할 지 시나리오를 세우는 능력 부족
- Feature Engineering
    - DataFrame
        - 어떻게 하면 내가 원하는 feature로 가공할 수 있을 지 구현 능력 부족
    - Method
        - 어떤 방법론이 알맞은지, 어떤 방법을 해당 feature에 적용할 수 있을 지, 기존의 feature를 활용하여 어떻게 새로운 feature를 만들어낼 수 있을 지에 대한 생각을 하지 못함
- Model Selection
    - 데이터에 맞는 모델을 선택하는 합리적인 이유를 찾아내지 못함
    - 배운 모델이 어떠한 데이터에 활용하면 좋을지에 대한 이해가 부족함
- pytorch
    - 전체 구조
        - dataloader와 model load하는 부분과 같은 모듈화 된 파이토치 구조에 대한 이해 부족  
            - ex1) dataloader에서 불러왔는데 왜 이거 iterator로 불러와지는거야?
    - DL&ML model 구조
        - batch size나 dimension등 데이터의 흐름에 대한 이해가 없음
            - ex1) 아! 이 코드를 지나면 데이터가 이렇게 될거야
            - ex2) batch size가 이 정도고 epoch가 이 정도니까 iteration은 얼마겠네
            - ex3) 여기는 입력이 어떻게 돼야 하니까 임베딩 dimension이 어느정도가 돼야하겠네
        - 코드가 왜 해당위치에 구현되었나에 대한 이해가 없음
            - ex1) 왜 forward에서 이 함수를..?
        - nn.module을 정확하게 이해하지 못함
            - nn.embedding은 갑자기 튀어나와서 데이터를 왜 이렇게 바꿔주는거지..?
- Linux
    - 기본개념
        - 리눅스에 대한 기본적인 이해와 개요에 대한 지식 부족
    - 가상환경
        - 기본적인 이해 부족
        - 비전문가한테 설명 불가
            - 가상환경을 왜 만드는건데..? 폴더나 파일 그대로 있는데..?
    - 기본 명령어
        - 기본적인 명령어를 구글링하는데 많은 시간 소요
    - 쉘스크립트
        - .sh 파일이 있는걸 처음 알았다.
- OOP
    - 매직메소드나 상속 등에 대한 OOP 전반적인 내용이 아직 익숙하지 않음
- WandB
    - 써보니까 좋은건 알겠는데 조금 더 디테일하게 알고 쓰면 100% WandB를 활용할 수 있을 것 같다.
- Git & Github
    - 깃 플로우나 깃허브 플로우에 대한 경험 필요
    - 커밋 컨벤션에 대한 경험 필요
    - 기본적인 체크아웃이나 3way merge등에 대한 복습도 필요
- Coding
    - 코드를 pythonic하게 짜는 것이 아직 부족함  

<span style="font-size:150%">**개선방안**</span> 
- EDA
    - kaggle notebook에서 사람들이 EDA한 부분 공부
        - 매일 1시간
- Feature Engineering
    - 빅데이터 분석기사 기출문제에서 dataframe으로 핸들링 하는 부분 공부
        - 매일 1시간
- Model Selection
    - recsys 기초 강의 복습
        - 하루 1강
    - recsys 기초 프로젝트 강의 복습
        - 하루 1강
    - 강의 다 보고 모델 직접 구현해보기
        - 하루 모델 1개(프로젝트 없을 때)
- pytorch
    - pytorch 기초 강의 복습
        - 하루 1강
- Linux
    - 위키독스 Bash 쉘스크립트 개발 시작하기로 공부해보기
        - 기차안에서 왕복 6시간 공부하면 습득 가능할 듯
    - 리눅스(CentOS) - 개발 놀이터 만들기로 APM 구현해보기
        - 위의 항목으로 리눅스 기초가 완성되면 차후 학습 예정
- OOP
    - 네부캠 OOP 강의 및 실습 복습하기
        - 매일 보기
- WandB
    - "모델 직접 구현해보기" 할 때 같이 구현 
- Git & Github
    - 프로젝트 전까지 VOD 복습하면서 공부
        - 격일 1시간씩
- Coding
    - coding test 연습
        - 매일 1시간
</details>



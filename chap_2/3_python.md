# 3장 파이썬[↩](../python_algorithm_interview)

귀도 반 로썸(Guido Van Rossum)의 파이썬 원칙은 다음과 같다.

* 읽기 쉬워야 한다.
  : 중괄호로 묶기보다는 까끔하게 인덴트로 처리한 공백으로 둘러싼다.
* 사용자가 원하는 모듈 패키지를 만들 수 있어야 했으며 다른 프로그램에서 사용할 수 있게 한다.
  : 이 방식은 계속 발전해 `easy_install`을 거쳐 `pip`를 통해 패키지 인덱스를 제공하는 형태로 완성됐으며 다른 수많은 언어에까지 영향을 끼쳤다.
* 약간 독특하고 신비한 이름을 원한다.
  : 영국의 코미디 그룹 몬티 파이썬(Monty Python)의 이름을 따서 파이썬이라는 이름을 붙인다.

파이썬은 **실행가능한 수도코드**(Executable Pseudocode)라는 별칭으로도 불린다.

* 수도코드 : 실행이 되지 않는, 알고리즘만을 기술하는 코드를 말하는데, 파이썬은 알고리즘만을 기술할 정도로간결하면서도 실행까지 가능하다는 의미한다.

## Contents📑<a id="contents"></a>

* 3_1 파이썬에 대한 이해[👉](#3_1)
* 3_2 파이썬 문법[👉](#3_2)
  * 인덴트
  * 네이밍 컨벤션
  * 타입 힌트
  * 리스트 컴프리헨션
  * 제너레이터
  * range
  * enumerate
  * // 나눗셈 연산자
  * print
  * pass
  * locals
* 3_3 코딩 스타일[👉](#3_3)
  * 변수명과 주석
  * 리스트 컴프리헨션
  * 구글 파이썬 스타일 가이드

## 3_1 파이썬에 대한 이해[📑](#contents)<a id="3_1"></a>

 이번 장에서는 코딩테스트 문제 풀이를 통해 파이썬에 대해 매우 깊이 있는 내용까지 상세히 다룰 예정이다.

* 왠만한 서적 이상의 깊이로 파이썬을 자세히 살펴 본다.
  * 그 범위는 **내장 라이브러리**, **자료구조**, **알고리즘** 정도로 한정한다.
    (넘파이`numpy`, 객체 지향 프로그래밍 등의 주제는 이 책에서 다루지 않는다.)
* 파이썬 공식 인터프리터(interpreter)인 `CPython`을 기준으로 하고, 버전은 `3.7`을 기준으로 한다.

## 3_2 파이썬 문법[📑](#contents)<a id="3_2"></a>

### 인덴트

* 파이썬에서는 **인덴트(indent)**를  공식 가이드인 PEP 8에 따라 공백 4칸을 원칙으로 한다.

* 아래의 예시와 같이 첫 번째 줄에 파라미터가 있다면, 파라미터가 시작되는 부분에 보기 좋게 맞춘다.

  ```python
  foo = long_function_name(var_one, var_two,
                           var_three, var_four)
  ```

* 아래의 예시는 첫 번째 줄에 파라미터가 없다면, 공백 4칸 인덴트를 한 번 더 추가하여 다른 행과 구분되게 하는 것을 보여준다.

  ```python
  def long_fuction_name(
      	var_one, var_two, var_three,
      	var_four):
      print(var_one)
  ```

* 아래와 같이 여러 줄로 나눠쓸 경우 다음 행과 구분되도록 인덴트를 추가한다.

  ```python
  foo = long_function_name(
  	var_one, var_two,
      var_three, var_four)
  ```

* 이 모든 방식을 직접 고민하면서 구분하기는 쉽지 않은 일이기에 **파이참(pycharm) 커뮤니티 에디션**과 같은 좋은 개발 도구를 활용하는 것이 좋다.

  * 이 개발 도구는 신경쓰지 않아도 되는 코딩 가이드를 자동으로 맞춰준다.
  * 파이참에서 **Reformat Code**를 실행하면 자동으로 코드를 `PEP 8` 기준에 맞춰주기 때문에 매우 편리하다.

### 네이밍 컨벤션

 파이썬의 변수명과 함수명 **네이밍 컨벤션(Naming Convention)**은 자바와 달리 각 단어를 밑줄(_)로 구분하여 표기하는 **스네이크 케이스(Snake Case)**를 따른다.

* 면접관에게 파이썬의 `PEP 8` 및 철학에 따라 스네이크 코딩을 지향한다고 이야기 할 수 있어야 함

* **카멜 케이스 (Camel Case)** 예시

  ```python
  camelCase: int = 1
  ```

* **스네이크 케이스(Snake Case)** 예시

  ```python
  snake_case: int = 1
  ```

### 타입 힌트

 파이썬은 대표적인 동적 타이핑 언어임에도, 타입을 지정할 수 있는 **타입힌트(Type Hint)**가 `PEP 484` 문서에 추가되었다.

```python
a: str = "1"
b: int = 1
```

* 타입힌트를 사용하지 않는 파이썬 함수는 다음과 같이 함수를 정의한다.

  ```python
  def fn(a):
      ...
  ```

  하지만 이렬경우 `fn(a)`에 파라미터 `a`에는 숫자를, 문자를 넘겨야하는지 알수 없으며 이 함수의 리턴값이 무엇인지도 알수 없다.

  * 가독성을 떨어뜨리고 파라미터 a에 숫자를 넘겨야하는데 문자를 넘기는 등의 버그를 유발할 수 있다.

* 파라미터 `a`가 정수형임을 알리고 리턴 값으로 `True` 혹은 `False`를 리턴할것이라는 점을 알린다.

  ```python
  def fn(a: int) -> bool:
      ...
  ```

  강제 규약이 아니어서 여전히 동적으로 할당될 수 있으므로 주의가 필요하다.

* 다음과 같이 문자열에 정수를 할당하는 등의 사용방식은 절대 지양한다.

  ```python
  >>> a: str = 1
  >>> type(a)
  <class 'int'>
  ```

* 코딩테스트에서는 일반적으로 짧은 알고리즘으로 끝나는 경우가 많고, 타입은 지정하지 않아도 한눈에 보일 만큼 명확하기 때문에 굳이 지정해주지 않아도 문제가 되지 않지만, 코드 정리할때만이라도 타입을 모두 지정하여 제출한다면 코드 리뷰시 면접관에게 좋은 점수를 받을 수 있을 것이다.

 온라인 코딩테스트 시에는 `mypy`를 사용하면 타입힌트에 오류가 없는지 자동으로 확인할 수 있다. 이를 사용하여 수정 후 코드를 제출할 수 있다.

```python
$ pip install mypy
```

 타입 힌트가 잘못 지정된 코드는 다음과 같이 `Incompatible return value type` 오류가 발생하므로 확인후 코드를 직접 수정할 수 있다.

```python
$ mypy solution.py
solution.py:9: error: Incompatible return value type(got "str", expected "int")
solution.py:17: error: Incompatible return value type(got "str", expected "int")
Found 2 errors in 1 file (checked 1 source file)
```

### 리스트 컴프리헨션

 파이썬은 `map`, `filter`와 같은 **함수형(functional)** 기능을 지원하며 다름과 같은 **람다 표현식(lambda expression)**도 지원한다.

```python
list(map(lambda x: x + 10, [1, 2, 3]))

# 출력
[11, 12, 13]
```

* 자바는 2014년 버전 8에 이르러서야 **람다표현식**을 지원하기 시작하였지만, 파이썬은 1994년부터 람다를 지원했다.

파이썬에서 더 유용한 기능은 **리스트 컴프리헨션(list comprehension)**이다. 

* 리스트 컴프리헨션은 기존의 리스트를 기반으로 새로운 리스트를 만들어내는 구문으로, 파이썬2.0부터 지원되었고 하스켈(haskell)같은 함수형 언어에서 기능을 차용해온 파이썬의 대표적인 기능이다.

* 람다 표현식에 `map`이나 `filter`를 섞어서 사용하는 것에 비해 가독성이 훨씬 좋다.

* 아래는 홀수인 경우 2를 곱해서 출력하는 **리스트 컴프리헨션** 예시이다. 

  ```python
  [n * 2 for n in range(1, 10 + 1) if n % 2 == 1]
  
  # 출력
  [2, 6, 10, 14, 18]
  ```

* 리스트 컴프리헨션을 사용하지 않으면 다음과 같이 길게 풀어 작성해야 한다.

  ```python
  a = []
  for n in range(1, 10+1):
      if n % 2 == 1:
          a.append(n * 2)
  a
  
  # 출력
  [2, 6, 10, 14, 18]
  ```

  * 리스트 컴프리헨션을 사용하지 않게 되면 라인 수 가 늘어나고 `a` 라는 별도의 리스트 변수가 필요하다.

* 리스트 외에도 딕셔너리 등에도 가능하게 되었다. 

  ```python
  # 리스트 컴프리헨션 사용 전
  a = {}
  for key, value in original.items():
      a[key] = value
      
  # 리스트 컴프리헨션 사용 후
  a = {key : value for key, value in original.items()}
  ```

* 무리하게 복잡하게 리스트 컴프리헨션을 사용할 경우 가독성이 떨어질 수 있다. 

### 제너레이터

 **제네레이터(generator)**는 2001년 파이썬 2.2가 출시될 때 추가된 오래된 기능 중 하나로, 루프의 반복(Iteration)동작을 제어할 수 있는 루틴 형태를 말한다.

* 예를 들어, 임의의 조건으로 숫자 1억 개를 만들어내 계산하는 프로그램을 작성한다고 가정하면 제네레이터가 없다면 메모리 어딘가에 만들어낸 숫자 1억 개를 보관하고 있어야 한다. 하지만 제네레이터를 사용한다면, 단순히 제네레이터만 생성해두고 필요할 때 언제든 숫자를 만들어낼 수 있다. 

`yield`구문을 사용하면 제네레이터를 리턴할 수 있다. 기존의 함수는 `return` 구문을 맞닥뜨리면 값을 리턴하고 모든 함수의 동작을 종료하지만, `yield`는 제너레이터가 여기까지 실행 중이던 값을 내보낸다는 의미로, 중간값을 리턴한 다음 함수는 종료되지 않고 계속해서 맨 끝에 도달할 때까지 실행된다.

```python
def get_natural_number():
    n = 0
    while True:
        n += 1
        yield n

get_natural_number()


```

*  `while True` 구문은 종료조건이 없으므로 계속해서 값을 내보낼 수 있다. 

* 리턴 값은 제네레이터가 된다.

  ```python
  # 출력
  <generator object get_natural_number at 0x0000023823DD42B0>
  ```

* 다음값을 생성하려면 `next()`로 추출하면 된다. 
  다음은 100개의 값을 생성싶을때, 100번 동안 `next()`를 수행하면 된다.

  ```python
  g = get_natural_number()
  
  for _ in range(0, 100):
      print(next(g))
  
  # 출력
  1
  2
  3
  ...
  97
  98
  99
  100
  ```

여러 타입의 값을 하나의 함수에서 생성하는 것도 가능하다.

```python
def generator():
    yield 1
    yield 'string'
    yield True

g = generator()
g
# 출력
<generator object generator at 0x0000023823DD4830>

next(g)
# 출력
1
next(g)
# 출력
'string'
next(g)
# 출력
True
```

### range

 `range()`는 제네레이터를 사용하는 대표적인 함수로, 주로 `for문`에서 쓰이는 `range()` 함수의 쓰임은 다음과 같다.

```python
list(range(5))
# 출력
[0, 1, 2, 3, 4]

range(5)
# 출력
range(0, 5)

type(range(5))
# 출력
range

for i in range(5):
    print(i, end=' ')
# 출력
0 1 2 3 4 

```

* `range()`는 range클래스를 리턴하고 for문에서 사용할 경우 내부적으로는 제네레이터의 next()를 호출하듯 매번 다음 숫자를 생성해내게 된다.

 그렇다면 만약 생성할 숫자가 100만 개쯤 된다면 메모리에서 적지 않은 공간을 차지할 것이고 생성 시간도 오래 걸릴 것이다. 하지만 제네레이터를 리턴하듯 `range`클래스만 리턴하면 그렇게 오래걸리지 않게 된다. 생성 조건만 정해두고 나중에 필요할 때 생성해서 꺼내 쓸 수 있게 된다. 

```python
# 변수 생성
a = [n for n in range(10000000)]
b = range(10000000)

len(a)
# 출력
10000000
len(b)
# 출력
10000000
len(a) == len(b)
# 출력
True
b
# 출력
range(0, 10000000)
type(b)
# 출력
range
import sys

sys.getsizeof(a)
# 출력
81528056
sys.getsizeof(b)
# 출력
48
```

* `a`와 `b` 둘다 100만개를 갖고 있으나 range 클래스를 이용하는 `b` 변수의 메모리 점유율이 훨씬 작다. 
*  생성조건만 보관하고 있기때문에 변수 `b`의 경우에는 1억개의 수를 가지고 있어서도 메모리 점유율은 동일하다. 
* 게다가 인덱스 접근시에는 바로 생성하도록 구현이 되어 있기 때문에 리스트와 동일하게 사용할 수 있다.

```python
b[999]
# 출력
999
```

### enumerate

 `enumerate()`는 '열거하다'는 뜻의 함수로, 여러 가지 자료형(list, set, tuple 등)을 인덱스를 포함한 **enumerate**객체로 리턴한다.

```python
a = [1,2,3,2,45,2,5]
a
# 출력
[1, 2, 3, 2, 45, 2, 5]

enumerate(a)
# 출력
<enumerate at 0x238232f8438>

list(enumerate(a))
# 출력
[(0, 1), (1, 2), (2, 3), (3, 2), (4, 45), (5, 2), (6, 5)]
```

* `list()`로 결과를 추출할 수 있는데, 인덱스를 자동으로 부여해주기 때문에 매우 편리하게 사용할 수 있다.

* `a =  ['a1', 'b2', 'c3']`가 있을때, 리스트의 인덱스와 값을 같이 출력하고 싶을때는 다음과 같이 하면 된다.

  ```python
  a =  ['a1', 'b2', 'c3']
  
  # 1)
  for i in range(len(a)):
      print(i, a[i])
  # 출력
  0 a1
  1 b2
  2 c3
  
  # 2)
  i = 0
  for v in a:
      print(i, v)
      i += 1
  # 출력
  0 a1
  1 b2
  2 c3
  
  # 3)
  for i, v in enumerate(a):
      print(i, v)
  # 출력
  0 a1
  1 b2
  2 c3  
  ```

* 첫번째 방법의 경우엔 값을 가져오기 위해 불필요한 `a[i]` 조회 작업과 전체 길이를 조회하여 루프를 처리하는 형태가 깔끔해 보이지 않는다. 

* 두번째 방법은 `range()`를 사용하지 않았지만 인덱스를 위한 변수를 별도로 관리하는 형태이기에 깔끔해 보이지 않는다. 

* 세번째 방법은 `enumerate()`를 사용하여 깔끔하게 처리가 된다. 

### // 나눗셈 연산자

 `//` 연산자는 정수형을 나눗셈할때 동일한 정수형을 결과로 리턴하면서 내림(Floor Division)연산자의 역할을 한다. 다시 말하면 몫(Quotient)을 구하는 연산자이다.

```python
5 / 3
# 출력
1.6666666666666667

type(5 / 3)
# 출력
float

5 // 3
# 출력
1

type(5 // 3)
# 출력
int

int(5 / 3)
# 출력
1

type(int(5 / 3))
# 출력
int
```

* `5 // 3`와 `int(5 / 3)`는 동일하게 사용가능하다. 

 나머지를 구하는 모듈로 연산자는 `%`로 아래와 같이 사용가능하다.

```python
5 % 3
# 출력
2
```

 `divmod()`함수를 사용하면 몫과 나머지를 동시에 구할 수있다. 

```python
divmod(5, 3)
# 출력
(1, 2)
```

### print

 코딩 테스트 문제 풀이 과정에서 디버거나 TDD방식으로 접근하기 어렵기 때문에`print()`는 디버깅을 위해 제공되는 유일한 기능이다. 

* 콤마(,)를 통해 값을  구분해주는 경우 그대로 출력할 경우 띄어쓰기로 값을 구분해준다.

  ```python
  print('A1', 'B2')
  
  # 출력
  A1 B2
  ```

* `sep`파라미터로 구분자를 콤마(,)로 지정해줄 수도 있다. 

  ```python
  print('A1', 'B2', sep=',')
  
  # 출력
  A1,B2
  ```

* `print()`함수는 항상 줄바꿈을 하기 때문에 이를 막기 위해서는 `end=`파라미터를 공백으로 처리하면 줄바꿈을 하지 않을 수 있다.

  ```python
  print('aa', end=' ')
  print('bb')
  
  # 출력
  aa bb
  ```

* 리스트를 출력할 때는 `join()`으로 묶어서 처리한다.

  ```python
  a = ['A', 'B']
  print(' '.join(a))
  
  # 출력
  A B
  ```

* idx와 fruit이 정의되어 있을 때, idx 값에 1을 더해서 fruit와 함께 출력하는 방법으로는 다음과 같은 방법이 있다. 

  ``` python
  idx = 1
  fruit = "Apple"
  
  print('{0}:{1}'.format(idx + 1, fruit))
  
  # 출력
  2:Apple
  print('{}:{}'.format(idx + 1, fruit))
  
  # 출력
  2:Apple
  ```

* f-string(formated string literal)을 이용는 방법

  (파이썬 3.6+에서만 지원)

  ```python
  print(f'{idx + 1}:{fruit}')
  
  # 출력
  2:Apple
  ```

### pass

 코드 전체 골격을 잡아 놓고 내부에서 처리할 내용은 차근차근 생각하며 만드는 의도로 다음과 같이 코딩하는 경우가 있다.

```python
class MyClass(object):
    def method_a(self):

    def method_b(self):
        print("Method B")
c = MyClass()

# 출력
    def method_b(self):
      ^
IndentationError: expected an indented block
```

* 하지만 이럴 경우 이와 같이 인텐트 오류가 발생한다. 

 `method_a()`에 아무런 처리를 하지 않았기 때문에 엉뚱하게 `method_b()`에서 오류가 발생한 것인데, 필요한 오류이긴하지만 한참 개발을 하던 중에 이런 오류를 맞닥뜨리게 될 경우 생각보다 처리하기가 번거롭다. 이를 막기 위해서 `pass`를 삽입하여 `method_a()`의 오류를 처리할 수 있다.

```python
class MyClass(object):
    def method_a(self):
        # 여기에 pass를 추가
        pass

    def method_b(self):
        print("Method B")
c = MyClass()
```

 `pass`는 null연산으로(null operation)으로 아무것도 하지 않는 기능이다. `pass`는 **목업(mock-up)**인터페이스부터 구현한 다음에 추후 구현을 진행할 수 있게 한다. 

### locals

`local()`은 로컬 심볼 테이블 딕셔너리를 가져오는 메소드로 업데이트 또한 가능하다. 

* `local()`은  로컬에서 선언된 모든 변수를 조회할 수 있는 강력한 명령이므로 디버깅에 도움이 된다.

* 로컬 스코프에 제한해서 정보를 조회할 수 있기 때문에 클래스의 특정 메소드 내부에서나 함수 내부의 로컬 정보를 조회해 잘못 선언한 부분이 없는지 확인하는 용도로 활용할 수 있다. 

* 변수명을 일일이 찾을 필요없이 로컬 스코프에 정의된 모든 변수를 출력하기 때문에 편리하다.

* 다음은 리트코드(leetcode)문제 풀이 중에 코드 내부를 출력할때 쓰는 코드이다.

  ```python
  import pprint
  pprint.pprint(locals())
  
  # 출력
  { 'nums': [2, 7, 11, 15],
   'pprint': <module 'pprint' from '/usr/lib/python3.8'/pprint.py'>,
   'self': <__main__.Solution object at 0x7f0994769d90>,
   'target': 9}
  ```


## 3_3 코딩 스타일[📑](#contents)<a id="3_3"></a>

 코딩 테스트에서 **코딩스타일**은 별로 중요하게 여기지 않을 수도 있다. 코딩 테스트 이후 인터뷰 과정에서 면접관은 제출한 코드의 품질을 평가할 수 있기 때문에 코딩 스타일은 중요하다. 다음 책은 각각 자바와 C언어 에서 좋은 코드에 대한 지침서이다. 

* Clean Code 클린 코드
* 프로그래밍 수련법

 파이썬의 경우 [PEP 8](https://peps.python.org/pep-0008/)와 [구글의 파이썬 스타일 가이드](https://google.github.io/styleguide/pyguide.html)는 실용적인 관점에서 좋은 파이썬 코드를 작성하는데 도움을 준다. 

### 변수명과 주석

* 실제 문제 풀이에서 사용된 문자열에 매칭된 서브시퀀스의 개수를 구하는 코드 예시 중 먼저, 변수명을 아무렇게나 지정하고 주석도 없이 작성한 코드이다. 

  ```python
  def numMatchingSubseq(self, S:str, words: List[str]) -> int:
      a = 0
      
      for b in words:
          c = 0
          for i in range(len(b)):
              d = S[c:].find(b[i])
              if d < 0:
                  a -= 1
                  break
              else:
                  c += d + 1
          a += 1
      return a
  ```

  * 파이썬에서 인덴트를 강조하고 있어 지저분해 보이지는 않지만 위의 코드는 변수명이 무엇을 의미하는지 알기 어려우며, 알고리즘에 대한 주석이 없어 어떻게 동작하는지 파악하기도 쉽지 않다.

* 면접관들은 제출한 결과물에 대해 주석 여부를 확인하고 인터뷰 시에는 주석에 대해 논의하기도 한다. 

  ```python
  def numMatchingSubseq(self, S: str, words: List[str]) -> int:
      matched_count = 0
      
      for word in words:
          pos = 0
          for i in range(len(word)):
              # Find matching position for each character.
              found_pos = S[pos:].find(word[i])
              if found_pos < 0:
                  matched_count -= 1
                  break
              else:	# If found, take step position forward.
                  pos += found_pos + 1
              matched_count += 1
      return matched_count
                  
  ```

  * 간단한 주석을 부여하는 것이 가독성이 높아 보이게 한다. 
  * 변수명도 이름보다는 각각의 의미를 부여해 작명하고 PEP 8 문서 기준에 따라 모두 스네이크 케이스로 작성했다. 
  * 주석은 영어로 다는 것이 조금 더 프로페셔널하게 보인다. 

### 리스트 컴프리헨션

 `리스트 컴프리헨션`의 경우 파이썬의 강력한 기능 중에 하나이지만 이를 남용하게 되면 파이썬의 가독성을 떨어뜨리게 된다. 

* 다음은 가독성을 떨어뜨리게 하는 리스트 컴프리헨션의 예시이다.

  ```python
  str1s = [str1[i:i + 2].lower() for i in range(len(str1) - 1) if re.findall('[a-z]{2}', str1[i:i + 2].lower())]
  ```

* 다음과 같이 역할별로 줄바꿈을 할 경우 가독성을 높일 수 있다.

  ```python
  str1s = [
      str1[i:i + 2].lower() for i in range(len(str1) - 1)
      if re.findall('[a-z]{2}', str1[i:i + 2].lower())
  ]
  ```

* 다음과 같이 모두 풀어서 쓰는 것도 가독성을 위해서라면 나쁘지 않다. 

  ```python
  str1s = []
  for i in range(len(str1) - 1):
      if re.findall('[a-z]{2}', str1[i:i + 2].lower()):
          str1s.append(str1[i:i + 2].lower())
  ```

* 하지만 다음과 가팅 너무 여러 줄로 표현하게 되면 가독성이 지나치게 떨어진다. 

  ```python
  return[(x, y, z)
        for x in range(5)
        for y in range(5)
        if x != y
        for z in range(5)
        if y != z]
  ```

### 구글 파이썬 스타일 가이드

 **구글 파이썬 스타일 가이드**에서는 PEP 8에서 설명하지 않은 좋은 코드를 위한 지침드링 여럿이 있는 편이다. 특히 가독성을 높이기 위한 지침들이 많은데 그중 몇 가지 지침들을 보면 다음과 같다. 

* 먼저, 한수의 기본값으로 가변 객체(Mutable Object)를 사용하지 않아야 한다. 함수가 객체를 수정하면 기본값이 변경되기 때문이다. 따라서 다음과 같이 기본값으로 []나 {}를 사용하는 것은 지양해야한다.

  ```
  No: def foo(a, b=[])
  	...
  No: def foo(a, b: Mapping = {}):
  	...
  ```

* 대신 불변 객체(Immutable Object)를 사용한다. `None`을 명시적으로 할당하는 것도 좋은 방법이다. 

  ```python
  Yes: def foo(a, b=None):
      if b is None:
          b=[]
  Yes: def foo(a, b: Optional[Sequence] = None):
      if b is None:
          b = []
  ```

  * `True`, `False`를 판별할때는 암시적인 방법을 사용하는 편이 간결하고 가독성을 높인다. 굳이 `False`임을 `if foo != []:`와 같은 형태로 판별할 필요가 없다. `if foo:` 면 충분하다.

* `len(users) == 0`으로 길이가 없다는 말은 값이 없다는 뜻으로 `not users`로 충분하다. 

  ```python
  Yes: if not users:
      print('no users')
      
  No: if len(users) == 0:
      print('no users')
  ```

* 정수를 처리할 때는 암시적으로 거짓 여부를 판별하기 보다는 비교 대상이 되는 정수값을 직접 비교하는 편이 덜 위험하다.

  ```python
  Yes: if foo == 0:
      self.handle_zero()
      
  No: if foo is not None and not foo:
      self.handle_zero()
  ```

* 모듈로 연산 결과가 0인 것을 정수로 처리하지 않고 암시적 거짓 여부로 판별하는 것은 위험하고 가독성도 떨어진다. `i % 10 == 0`으로 명시적으로(Explicitly)값을 비교하는 편이 좋다.

  ```python
  Yes: if i & 10 == 0:
      self.handle_multiple_of_ten()
      
  No: if not i % 10:
      self.handle_multiple_of_ten()
  ```

* 세미콜론으로 줄을 끝내서는 안되고 세미 콜론을 사용해 같은 줄에 두 문장을 써서도 안 된다.

* 최대 줄 길이는 80자로 한다. 큰 모니터를 사용하지만 가로 길이는 길어서는 안된다는 암묵적인 약속이 있다.  

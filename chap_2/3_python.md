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

### enumerate
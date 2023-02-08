# 객체 지향 프로그래밍


→ **Object-Oriented Programming  OOP**

- 명령어의 목록으로 보는 시각에서 벗어나 여러 개의 독립된 단위

- **절차 지향 프로그래밍**
    - 장점
        - 프로그램 전체가 유기적으로 흐름으로 연결
        - 기능 중심의 프로그램
        - 순서가 정해져 있으므로 실행이 빠름
    - 단점
        - 하드웨어가 발전함에 소프트웨어의 크기가 커지고 복잡한 설계가 요구됨
        - 하드웨어의 발전 속도를 소프트웨어의 발전 속도가 따라가지 못함(**소프트웨어의 위기**)
        
        → 생산성이 너무 낮다
        
        → 절차 대신 **데이터**를 중심으로 생각의 필요성
        

- 객체 지향 프로그래밍
    - 데이터와 기능(메서드) 분리, **추상화**된 구조(인터페이스)
- 장점
    - 설계 시 많은 노력과 시간이 필요함
    - 현실 세계를 프로그램 설게에 반영가능(추상화)
    - 계속해서 재사용 가능
    - 데이터와 행동이 독립적으로 정의됨
        - 내부 구조를 몰라도 그냥 가져다가 다른 객체와 조립하면서 개발 가능
    - 객체 단위로 모듈화시켜 개발할 수 있어 많은 인원이 참여하는 대규모 스프트웨어 개발 가능
    - **개발 용이성, 유지 보수 편의성, 신뢰성 바탕으로 생산성 대폭 증가!**

- 단점
    - 설계 시 많은 노력과 시간이 필요함
        - 다양한 객체들의 상호 작용 구조를 만들기 위해 많은 시간과 노력이 필요
    - 실행 속도가 상대적으로 느림

## 객체 지향의 핵심 4가지

---

### 추상화

- **추상화** : 핵심의 최종 부분 추리기
    - 현실 세계를 프로그램 설게에 반영

### 상속

- **상속** : 코드의 재사용성을 높이고 기능을 확장
    - 클래스 사이를 부모와 자식 관계를 정립하는 것
    - 하위 클래스는 상위 클래스에 정의된 속성, 행동, 관계 및 제약 조건을 모두 상속 받음
    - isinstancec(object, classinfo)
        - classinfo의 instance거나 subclass인 경우 True
    - issubclass(class, classinfo)
        - class가 classinfo의 subclass면 True
    - super()
        - 자식클래스에서 부모클래스를 사용하고 싶은 경우
    - 다중 상속
        - 두 개 이상의 클래스를 상속받는 경우
        - 상속 받은 모든 클래스의 요소를 활용 가능함
        - 중복된 속성이나 메서드가 있는 경우 **상속 순서**에 의해 결정됨
    - mro 메서드(Method Resolution Order)
        - 인스터스의 클래스가 어떤 부모 클래스를 가지는지 확인하는 메서드

### 다형성

- **다형성** : 각자의 특성에 따라 다른 결과
    - 동일한 메서드가 클래스에 따라 다르게 행동할 수 있음
    - 동일 메시지에 대한 다른 방식으로 응답 가능
    - 메서드 오버라이딩
        - 메서드를 재정의
            - 부모클래스에서 정의한 메서드를 자식 클래스에서 변경
            - 이름과 기본 기능은 그대로 사용하지만 특정 기능을 바꾸고 싶을 때 사용
            - 부모 클래스의 메서드를 실행시키고 싶은 경우 super()사용

### 캡슐화

- **캡슐화** : 데이터 보호하기
    - 객체의 일부 구현 내용에 대해 외부로부터의 직접적인 액세스를 차단
    
    - Public Access Modifier
        - public member
            - 어디서나 호출이 가능, 하위 클래스 override 허용
            
    - Protected Access Modifier
        - protected member
            - 언더바 1개로 시작하는 메서드나 속성
            - 부모 클래스 내부와 자식 클래스에서만 호출 가능
            - 하위 클래스 override 허용
            
    - Private Access Modifier
        - private member
            - 언더바 2개로 시작하는 메서드나 속성
            - 본 클래스 내부에서만 사용이 가능
            - 하위클래스 상속 및 호출 불가능(오류)
            - 외부 호출 불가능(오류)
    - getter 메서드
        - @ property 데코레이터 사용
        - 변수의 값을 읽는 메서드
    - setter 메서드
        - @ 변수.setter 데코레이터 사용
        - 변수의 값을 설정하는 성격의 메서드

예시

```python
class Person:
    def __init__(self):
        self._age = 0

    @property
    def age(self):  #getter
        print('getter 호출')
        return self._age

    @age.setter
    def age(self, age): #setter
        print('setter 호출')
        self._age = age
    
    # age = property(get_age, set_age)
# p1.age = 25
# print(p1.age)

p1 = Person()
p1.age = 25
print(p1.age)
# p1._age = 25
# print(p1._age)
# 불편하다면
# p1.set_age(25)
# print(p1.get_age())
```

## OOP 기초

---

**객체(컴퓨터 과학)**

- 컴퓨터 과학에서 객체 또는 오브젝트는 클래스에서 정의한 것을 토대로 메모리(실제 저장공간)에 할당된 것으로 프로그램에서 사용되는 데이터 또는 식별자에 의해 참조되는 공간을 의미하며, 변수, 자료 구조, 함수 또는 메서드가 될 수 있다.

**객체와 인스턴스**

- 클래스(설계도)로 만든 객체를 인스턴스(실체)라고 한다.
- 클래스(→ 타입(list))와 객체

```jsx
파이썬은 모든 것이 객체 
```

**객체의 특징**

- 타입(type) : 어떤 연산자와 조작이 가능한가?
- 속성(attribut) : 어떤 상태(데이터)를 가지는가?
- 조작법/기능(method) : 어떤 행위(함수)를 할 수 있는가?

객체 = 속성 + 기능

**기본 문법** 

- 클래스 정의 class Myclass:
- 인스턴스 생성 my_instance = Myclass()
- 메서드 호출 my_instance.my_method()
- 속성 접근 my_instance.my_attribute

**속성**

- 특정 데이터 타입/클래스의 객체들이 가지게 될 상대/데이터를 의미
- 클래스 변수 / 인스턴스 변수가 존재
    
    

**인스턴스와 클래스 간의 이름 공간(namespace)** 

- 클래스를 정의하면, 클래스와 해당하는 이름공간 생성
- 인스턴스를 만들면, 인스턴스 객체가 생성되고 이름 공간 생성
- 인스턴스에서 특정 속성에 접근하면, 인스턴스 - 클래스 순으로 탐색

**인스턴스 변수**

- 인스턴스 변수란?
- 인스턴스가 개인적으로 가지고 있는 속성(attribute)
- 각 인스턴스들의 고유한 변수
- 생성자 메서드(’__init__’)에서 self.<name>으로 정의
- 인스턴스가 생성된 이후 <instance>.<name>으로 접근 및 할당
    
    

**클래스 변수**

- 클래스 변수
    - 한 클래스의 모든 인스턴스가 공유하는 값을 의미
    - 같은 클래스의 인스턴스들은 같은 값을 갖게 됨
    - 클래스 선언 내부에서 정의
    - <classname>.<name>으로 접근 및 할당

## OOP 메서드

---

**메서드**

- 특정 데이터 타입 / 클래스의 객체에 공통적으로 적용 가능한 행위(함수)

**메서드 종류**

- 인스턴스 메서드
- 클래스 메서드
- 정적 메서드

## 인스턴스 메서드

---

- 인스턴스 변수를 사용하거나 인스턴스 변수에 값을 설정하는 메서드
- 클래스 내부에 정의되는 메서드의 기본
- 호출 시, 첫번째 인자로 인스턴스 자기자신(self)이 자동으로 전달됨

**self**

- 인스턴스 자기자신
- 파이썬에서 첫번쨰 인자로 인스턴스 자신이 전달되게 설계
    - 암묵적 규칙

**매직 메서드**

- Double underscore가 있는 메서드는 특수한 동작을 위해 만들어진 메서드로, 스페셜 메서드 혹은 매직 메서드라고 불림
- ex) ‘__str__(self)’, ‘__len__(self)__’, ‘__it__(self,other)’, ‘__le__(self,other)’, ‘__eq__(self,other)’
    - ‘__str__’ : 문자열로 표현하면 어떻게 표현할지를 지정
- ex) ‘__ge__(self,other)’, ‘__ge__(self,other)’, ‘__ne__self,other)’
    - ‘__gt__’ : 부등호 연산자

**생성자(constructor) 메서드**

- 인스턴스 객체가 생성도리 때 자동으로 호출되는 메서드
- 인스턴스 변수들의 초기값을 설정
    - 인스턴스 생성
    - ‘__init__’ 메서드 자동 호출

## 클래스 메서드

---

- 클래스가 사용할 메서드
- @classmethod 데코레이터를 사용하여 정의
- 호출 시, 첫번째 인자로 클래스가 전달됨

**데코레이터**

- 함수를 어떤 함수로 꾸며서 새로운 기능을 부여
- @데코레이터(함수명) 형태로 함수 위에 작성
- 순서대로 적용되기 때문에 작성 순서가 중요

데코레이터 예시

```python
def ko_hello(name):
    print(f'안녕하세요, {name}님!')
    
def en_hello(name):
    print(f'HELLO, {name}!')

def add_emoji(name, func):
    func(name)
    print('^0^')

# ko_hello('jeongmo')
# en_hello('jeongmo')
# add_emoji('jeongmo', ko_hello)

def emoji_decorator(func):
    def human(name):
        func(name)
        print("^-^")

    return human

new_func = emoji_decorator(ko_hello)('aiden')

더욱 편하게 사용할때
@classmethod
'장식'의 느낌으로 기능을 추가 가능하다.
```

# 객체 지향 프로그래밍

---

→ **Object-Oriented Programming  OOP**

- 명령어의 목록으로 보는 시각에서 벗어나 여러 개의 독립된 단위

- **절차 지향 프로그래밍**
    - 장점
        - 프로그램 전체가 유기적으로 흐름으로 연결
        - 기능 중심의 프로그램
        - 순서가 정해져 있으므로 실행이 빠름
    - 단점
        - 하드웨어가 발전함에 소프트웨어의 크기가 커지고 복잡한 설계가 요구됨
        - 하드웨어의 발전 속도를 소프트웨어의 발전 속도가 따라가지 못함(**소프트웨어의 위기**)
        
        → 생산성이 너무 낮다
        
        → 절차 대신 **데이터**를 중심으로 생각의 필요성
        

- 객체 지향 프로그래밍
    - 데이터와 기능(메서드) 분리, **추상화**된 구조(인터페이스)
- 장점
    - 설계 시 많은 노력과 시간이 필요함
    - 현실 세계를 프로그램 설게에 반영가능(추상화)
    - 계속해서 재사용 가능
    - 데이터와 행동이 독립적으로 정의됨
        - 내부 구조를 몰라도 그냥 가져다가 다른 객체와 조립하면서 개발 가능
    - 객체 단위로 모듈화시켜 개발할 수 있어 많은 인원이 참여하는 대규모 스프트웨어 개발 가능
    - **개발 용이성, 유지 보수 편의성, 신뢰성 바탕으로 생산성 대폭 증가!**

- 단점
    - 설계 시 많은 노력과 시간이 필요함
        - 다양한 객체들의 상호 작용 구조를 만들기 위해 많은 시간과 노력이 필요
    - 실행 속도가 상대적으로 느림

## 객체 지향의 핵심 4가지

---

### 추상화

- **추상화** : 핵심의 최종 부분 추리기
    - 현실 세계를 프로그램 설게에 반영

### 상속

- **상속** : 코드의 재사용성을 높이고 기능을 확장
    - 클래스 사이를 부모와 자식 관계를 정립하는 것
    - 하위 클래스는 상위 클래스에 정의된 속성, 행동, 관계 및 제약 조건을 모두 상속 받음
    - isinstancec(object, classinfo)
        - classinfo의 instance거나 subclass인 경우 True
    - issubclass(class, classinfo)
        - class가 classinfo의 subclass면 True
    - super()
        - 자식클래스에서 부모클래스를 사용하고 싶은 경우
    - 다중 상속
        - 두 개 이상의 클래스를 상속받는 경우
        - 상속 받은 모든 클래스의 요소를 활용 가능함
        - 중복된 속성이나 메서드가 있는 경우 **상속 순서**에 의해 결정됨
    - mro 메서드(Method Resolution Order)
        - 인스터스의 클래스가 어떤 부모 클래스를 가지는지 확인하는 메서드

### 다형성

- **다형성** : 각자의 특성에 따라 다른 결과
    - 동일한 메서드가 클래스에 따라 다르게 행동할 수 있음
    - 동일 메시지에 대한 다른 방식으로 응답 가능
    - 메서드 오버라이딩
        - 메서드를 재정의
            - 부모클래스에서 정의한 메서드를 자식 클래스에서 변경
            - 이름과 기본 기능은 그대로 사용하지만 특정 기능을 바꾸고 싶을 때 사용
            - 부모 클래스의 메서드를 실행시키고 싶은 경우 super()사용

### 캡슐화

- **캡슐화** : 데이터 보호하기
    - 객체의 일부 구현 내용에 대해 외부로부터의 직접적인 액세스를 차단
    
    - Public Access Modifier
        - public member
            - 어디서나 호출이 가능, 하위 클래스 override 허용
            
    - Protected Access Modifier
        - protected member
            - 언더바 1개로 시작하는 메서드나 속성
            - 부모 클래스 내부와 자식 클래스에서만 호출 가능
            - 하위 클래스 override 허용
            
    - Private Access Modifier
        - private member
            - 언더바 2개로 시작하는 메서드나 속성
            - 본 클래스 내부에서만 사용이 가능
            - 하위클래스 상속 및 호출 불가능(오류)
            - 외부 호출 불가능(오류)
    - getter 메서드
        - @ property 데코레이터 사용
        - 변수의 값을 읽는 메서드
    - setter 메서드
        - @ 변수.setter 데코레이터 사용
        - 변수의 값을 설정하는 성격의 메서드

예시

```python
class Person:
    def __init__(self):
        self._age = 0

    @property
    def age(self):  #getter
        print('getter 호출')
        return self._age

    @age.setter
    def age(self, age): #setter
        print('setter 호출')
        self._age = age
    
# age = property(get_age, set_age)
# p1.age = 25
# print(p1.age)

p1 = Person()
p1.age = 25
print(p1.age)
# p1._age = 25
# print(p1._age)
# 불편하다면
# p1.set_age(25)
# print(p1.get_age())
```

## OOP 기초

---

**객체(컴퓨터 과학)**

- 컴퓨터 과학에서 객체 또는 오브젝트는 클래스에서 정의한 것을 토대로 메모리(실제 저장공간)에 할당된 것으로 프로그램에서 사용되는 데이터 또는 식별자에 의해 참조되는 공간을 의미하며, 변수, 자료 구조, 함수 또는 메서드가 될 수 있다.

**객체와 인스턴스**

- 클래스(설계도)로 만든 객체를 인스턴스(실체)라고 한다.
- 클래스(→ 타입(list))와 객체

```jsx
파이썬은 모든 것이 객체 
```

**객체의 특징**

- 타입(type) : 어떤 연산자와 조작이 가능한가?
- 속성(attribut) : 어떤 상태(데이터)를 가지는가?
- 조작법/기능(method) : 어떤 행위(함수)를 할 수 있는가?

객체 = 속성 + 기능

**기본 문법** 

- 클래스 정의 class Myclass:
- 인스턴스 생성 my_instance = Myclass()
- 메서드 호출 my_instance.my_method()
- 속성 접근 my_instance.my_attribute

**속성**

- 특정 데이터 타입/클래스의 객체들이 가지게 될 상대/데이터를 의미
- 클래스 변수 / 인스턴스 변수가 존재
    
    

**인스턴스와 클래스 간의 이름 공간(namespace)** 

- 클래스를 정의하면, 클래스와 해당하는 이름공간 생성
- 인스턴스를 만들면, 인스턴스 객체가 생성되고 이름 공간 생성
- 인스턴스에서 특정 속성에 접근하면, 인스턴스 - 클래스 순으로 탐색

**인스턴스 변수**

- 인스턴스 변수란?
- 인스턴스가 개인적으로 가지고 있는 속성(attribute)
- 각 인스턴스들의 고유한 변수
- 생성자 메서드(’__init__’)에서 self.<name>으로 정의
- 인스턴스가 생성된 이후 <instance>.<name>으로 접근 및 할당
    
    

**클래스 변수**

- 클래스 변수
    - 한 클래스의 모든 인스턴스가 공유하는 값을 의미
    - 같은 클래스의 인스턴스들은 같은 값을 갖게 됨
    - 클래스 선언 내부에서 정의
    - <classname>.<name>으로 접근 및 할당

## OOP 메서드

---

**메서드**

- 특정 데이터 타입 / 클래스의 객체에 공통적으로 적용 가능한 행위(함수)

**메서드 종류**

- 인스턴스 메서드
- 클래스 메서드
- 정적 메서드

## 인스턴스 메서드

---

- 인스턴스 변수를 사용하거나 인스턴스 변수에 값을 설정하는 메서드
- 클래스 내부에 정의되는 메서드의 기본
- 호출 시, 첫번째 인자로 인스턴스 자기자신(self)이 자동으로 전달됨

**self**

- 인스턴스 자기자신
- 파이썬에서 첫번쨰 인자로 인스턴스 자신이 전달되게 설계
    - 암묵적 규칙

**매직 메서드**

- Double underscore가 있는 메서드는 특수한 동작을 위해 만들어진 메서드로, 스페셜 메서드 혹은 매직 메서드라고 불림
- ex) ‘__str__(self)’, ‘__len__(self)__’, ‘__it__(self,other)’, ‘__le__(self,other)’, ‘__eq__(self,other)’
    - ‘__str__’ : 문자열로 표현하면 어떻게 표현할지를 지정
- ex) ‘__ge__(self,other)’, ‘__ge__(self,other)’, ‘__ne__self,other)’
    - ‘__gt__’ : 부등호 연산자

**생성자(constructor) 메서드**

- 인스턴스 객체가 생성도리 때 자동으로 호출되는 메서드
- 인스턴스 변수들의 초기값을 설정
    - 인스턴스 생성
    - ‘__init__’ 메서드 자동 호출

## 클래스 메서드

---

- 클래스가 사용할 메서드
- @classmethod 데코레이터를 사용하여 정의
- 호출 시, 첫번째 인자로 클래스가 전달됨

**데코레이터**

- 함수를 어떤 함수로 꾸며서 새로운 기능을 부여
- @데코레이터(함수명) 형태로 함수 위에 작성
- 순서대로 적용되기 때문에 작성 순서가 중요

데코레이터 예시

```python
def ko_hello(name):
    print(f'안녕하세요, {name}님!')
    
def en_hello(name):
    print(f'HELLO, {name}!')

def add_emoji(name, func):
    func(name)
    print('^0^')

# ko_hello('jeongmo')
# en_hello('jeongmo')
# add_emoji('jeongmo', ko_hello)

def emoji_decorator(func):
    def human(name):
        func(name)
        print("^-^")

    return human

new_func = emoji_decorator(ko_hello)('aiden')

더욱 편하게 사용할때
@classmethod
'장식'의 느낌으로 기능을 추가 가능하다.
```

## 스태틱 메서드

---

- 인스턴스 변수, 클래스 변수 아무것도 사용하지 않을 경우
- @ staticmethod 데코레이터를 사용하여 정의
- 일반 함수처럼 동작하지만 클래스의 이름 공간에 귀속된
    - 해당 클래스로 한정하는 용도로 사용

정리

```python
class MyClass:
    def method(self):
        return 'instance method'
    @classmethod
    def classmethod(cls):
        return 'class method'

    @staticmethod
    def staticmethod():
        return 'static method'

my_class = MyClass()
print(my_class.method())
print(my_class.classmethod())
print(my_class.staticmethod())
```

OOP 연습

```python
class Doggy:
    count = 0
    born = 0
    def __init__(self, name, spices):
        self.name = name
        self.spices = spices
        Doggy.count += 1
        Doggy.born += 1

    def bark(self):
        print(f'{self.name}이 "bark! bark!"하고 짖었습니다.')
    count1 = 0

    def __del__(self):
        Doggy.count -= 1

    @classmethod
    def dog_status(cls):
        print(f'{cls.born}마리 출생으로 총 {cls.count}마리입니다.')

Doggy1 = Doggy('강아지1', '종1')
Doggy2 = Doggy('강아지2', '종2')
Doggy3 = Doggy('강아지3', '종3')

Doggy2.bark()
Doggy4 = Doggy('강아지4', '종4')
Doggy5 = Doggy('강아지5', '종5')
del Doggy2
Doggy.dog_status()
```

```python
class Stack():
    def __init__(self):

        self.stack_list = []
    
    def empty(self):
        if (len(self.stack_list)) == 0:
            return True
        else:
            return False

    def top(self):
        if self.empty():
            print(None)
        else:
            return self.stack_list[-1]

    def pop(self):
        if self.empty():
            print(None)
        else:
            return self.stack_list.pop()

    def push(self, data):
        self.stack_list.append(data)

    def __repr__(self):
        return f'({self.stack_list})'

# __init__ 빈리스트 
# empty 비면 true 아니면 false 
# top 마지막 데이터 반환 비었다면 none 
# pop 마지막 데이터 반환 및 데이터 삭제 비었다면 none
# push 마지막 데이터 뒤에 값을 추가
# repr 현재 요소들을 보여준다.

#예시
stack = Stack()
print(stack.empty())
stack.push(1)
stack.push(2)
stack.push(3)
stack.push(4)
print(stack)
print(stack.top())
print(stack.pop())
print(stack)
```
# Class



## 클래스와 객체

---

- 과자 틀 -> 클래스
- 과자 -> 인스턴스(객체)

클래스로 만든 객체는 중요한 특징이 있다. 바로 객체마다 고유한 성격을 가진다는 것이다.

과자 a가 부서지거나 구멍이 뚫려도 다른 과자에는 영향을 주지 않는다. 이처럼 동일한 클래스로 만든 객체들은 서로 전혀 영향을 주지 않는다.

```python
# class 예시
class Cookie:
    pass

a = Cookie() # 과자1
b = Cookie() # 과자2
```



> **객체와 인스턴스의 차이**
>
> 클래스로 만든 객체를 인스턴스라고 한다. 객체와 인스턴스의 차이는 무엇일까?
>
> a = Cookie() 이렇게 만든 a는 객체이다.  a 객체는 Cookie의 인스턴스이다. 즉 인스턴스라는 말은 <u>특정 객체(a)가 어떤 클래스(Cookie)의 객체인지를 관계 위주로 설명할 때 사용</u>한다.
>
> "a는 인스턴스" 보다 "a는 객체"라는 표현이 어울리며 "a는 Cookie의 객체"보다는 "a는 Cookie의 인스턴스"라는 표현이 훨씬 잘 어울린다.



## 클래스 만들기

---

간단한 클래스의 구조를 살펴보자

```python
class FourCal:
    def setdata(self, first, second):
        self.first = first
        self.second = second
```

클래스 안에 구현되는 함수는 다른 말로 메서드(method)라고 부른다. 

일반적인 메서드의 구현은 다음과 같다.

```python
def 함수명(매개변수):
    수행할 문장
    ...
```



위에서 setdata라는 함수는 매개변수로 `self`, `first`, `second` 3개의 입력값을 받는다. 그런데 일반적인 함수와는 달리 클래스 내에서 self라는 입력값은 무엇일까?



```python
a = FourCal() # 객체 생성
a.setdata(4,2)
```

class내 setdata 메서드를 선언할 때 self라는 입력값이 필요한데 위의 코드에서는 입력을 안 했다. 왜 그럴까?

a.setdata(4,2)처럼 호출하면 setdata 메서드의 첫 번째 매개변수 self에는 setdata 메서드를 호출한 객체 a가 자동으로 전달되기 때문이다.



![image-20211209180318150](C:/Users/NaEunSu/AppData/Roaming/Typora/typora-user-images/image-20211209180318150.png)

파이썬 메서드의 첫 번째 매개변수 이름은 관례적으로 self를 사용한다. 객체를 호출할 때 호출한 객체 자신이 전달되기 때문에 self를 사용한 것이다. (참고로 self말고 다른 이름을 사용해도 상관없다.)

정리하자면 self는 객체 자신을 의미한다. 위에서 a.setdata(4, 2) 처럼 호출을 하면 first, second에는 각자 4와 2가 전달되어 이렇게 해석된다.

```python
self.first = 4
self.second = 2

# self에 전달된 객체는 a이므로 다음과 같이 해석된다.
a.first = 4
a.second = 2
```



## 생성자(Constructor)

---

생성자란 객체가 생성될 때 자동으로 호출되는 메서드를 의미한다.

파이썬 메서드 이름으로 `__intit__`을 사용하면 이 메서드는 생성자가 된다.

```python
 class FourCal:
   def __init__(self, first, second): # 생성자
        self.first = first
        self.second = second
   def setdata(self, first, second):
        self.first = first
        self.second = second
   def add(self):
       result = self.first + self.second
       return result
   def mul(self):
       result = self.first * self.second
       return result
   def sub(self):
       result = self.first - self.second
       return result
   def div(self):
      result = self.first / self.second
      return result
```



다음 코드를 실행시켜보자.

```python
a = FourCal()

# error
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __init__() missing 2 required positional arguments: 'first' and 'second'
```



`a = FourCal()` 을 수행할 때  `__init__` 이 호출되어   위와 같은 오류가 발생했다. 오류가 발생한 이유는 <u>매개변수 first와 second에 해당하는 값이 전달되지 않았기 때문이다.</u>



오류를 해결하려면 객체 생성시 입력값을 넣어주면 된다.

```python
a = FourCal(4, 2)
```



위와 같이 수행하면 `__init__` 메서드의 매개변수에는 다음과 같은 값이 대입된다.

| 매개변수 | 값            |
| -------- | ------------- |
| self     | 생성되는 객체 |
| first    | 4             |
| second   | 2             |

> `__init__` 메서드도 다른 메서드와 마찬가지로 첫 번째 매개변수 self에 생성되는 객체가 자동으로 전달된다는 점을 기억하자.



## 클래스의 상속

---

클래스에서 상속이란 어떤 클래스를 만들 때 다른 클래스의 기능을 물려받을 수 있게 만다는 것이다.



FourCal 클래스를 상속하는 MoreFourCal 클래스를 만들어보자.

```python
class MoreFourCal(FourCal):
    pass
```

> class 클래스 이름(상속할 클래스 이름)



MoreFourCal 클래스는 FourCal 클래스를 상속했으므로 FourCal 클래스의 모든 기능을 사용할 수 있다.

```python
a = MoreFourCal(4, 2)

a.add() # 6
a.mul() # 8
a.sub() # 2
a.div() # 2
```



> **왜 상속을 해야할까?**
>
> 보통 상속은 기존 클래스를 변경하지 않고 기능을 추가하거나 기존 기능을 변경하려고 할 때 사용한다.
>
> "클래스에 기능을 추가하고 싶으면 기존 클래스를 수정하면 되는데 왜 굳이 상속을 받아서 처리해야 하지?" 라는 의문이 들 수도 있다. 하지만 <u>기존 클래스가 라이브러리 형태로 제공되거나 수정이 허용되지 않는 상황이라면 상속을 사용해야 한다.</u>



MoreFourCal 클래스에 제곱을 계산하는 함수를 추가해보자.

```python
class MoreFourCal(FourCal):
    def pow(self):
        result = self.first ** self.second
        return result
```



pow 메서드를 수행해 보자.

```python
a = MoreFourCal(4, 2)
a.pow() # 16
```



## 메서드 오버라이딩

---

div 메서드에 입력값으로 4, 0을 넣어주면 ZeroDivisionError가 발생한다. 오류가 아닌 0을 리턴해주기 위해  FourCal클래스를 상속하는 SafeFourCal 클래스에 이름이 같은 div 메서드를 만들어보자.

```python
class SafeFourCal(FourCal):
    def div(self):
        if self.second == 0: # 나누는 값이 0인 경우 0을 리턴
            return 0
        else:
            return self.first / self.second
```



FourCal 클래스에 있는 div와 동일한 이름으로 SafeFourCal 클래스에 작성을 했다. 이렇게 부모 클래스(상속한 클래스)에 있는 메서드를 동일한 이름으로 다시 만드는 것을 `메서드 오버라이딩`(덮어쓰기)이라고 한다. 이렇게 메서드를 오버라이딩하면 부모클래스의 메서드 대신 오버라이딩한 메서드가 호출된다.



## 클래스 변수

---

객체변수는 다른 객체들에 영향을 받지 않고 독립적으로 그 값을 유지한다. 그러나 클래스 변수는 다르다.

```python
class Family:
    lastname = "김"
```



`lastname`이 클래스 변수이다. 클래스 변수는 클래스의 인스턴스들에 공통으로 적용된다.

```python
a = Family()
b = Family()

print(a.lastname) # 김
print(b.lastname) # 김
```



그렇다면 lastname을 "박"이라는 문자열로 바꾸면 어떻게 될까?

```python
Family.lastname = "박"

print(a.lastname) # 박
print(b.lastname) # 박
```



클래스 변수 값을 변경했더니 클래스로 만든 객체의 lastname 값도 모두 변경된다는 것을 확인할 수 있다. 즉 <u>클래스 변수는 클래스로 만든 모든 객체에 공유된다는 특징이 있다.</u>


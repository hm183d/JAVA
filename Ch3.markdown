# 연산자
연산자 : 연산을 수행하는 기호

- 증감 연산자 : 피연산자에 저장된 값을 1증가시키거나 감소시킨다. 상수는 값을 변경할 수 없기 때문에 증감연산자를 사용할 수 없다.
- 대부분의 연산자는 피연산자의 값을 읽어 연산에 사용만하는데 대입연산자와 증감연산자만이 피연산자의 값을 변경한다.
- 전위형 : j = ++i; 형태로 i의 값이 j 변수에 참조되기 전 먼저 증가한다.
- 후위형 : j = i++; 형태로 i의 값이 j 변수에 참조 된 후 증가한다.
- Math.round()메서드는 매개변수로 받은 값을 소수점 첫째자리에서 반올림을 하고 그 결과를 정수로 돌려주는 메서드이다.
- Math.round(3141.592)의 값은 3142이다.
- 나머지 연산자 %는 왼쪽 피연산자를 오른쪽 피연산자로 나눈 후의 나머지값을 결과로 반환하는 연산자이다. 또한 나눗셈에서처럼 나누는 수로 0을 사용할 수 없다.
- 문자열을 비교할 때는 비교연산자 ==(같다) 대신 equals()라는 메서드를 사용해야 한다. 

```java
    String str1 = "abc";
    Strint str2 = new String ("abc");

    System.out.printf("\"abc\" == \"abc\" ? %b%n", "abc" == "abc");
    System.out.printf("\"abc\" == \"abc\" ? %b%n", str1 == "abc");
    System.out.printf("\"abc\" == \"abc\" ? %b%n", str2 == "abc");
    
    System.out.printf("str1.equals(\"abc\") ? %b%n", str1.euqlas("abc"));
    System.out.printf("str2.equals(\"abc\") ? %b%n", str2.euqlas("abc"));
    System.out.printf("str2.equals(\"ABC\") ? %b%n", str2.euqlas("ABC"));
    System.out.printf("str2.equalsIgnoreCase(\"ABC\") ? %b%n", str2.euqlasIgnoreCase("ABC"));
```
실행결과
```
"abc"=="abc" ? true
str1 == "abc" ? true
str2 == "abc" ? false
str1.equals("abc") ? true
str2.equals("abc") ? true
str2.equals("ABC") ? false
str2.equalsIgnoreCase("ABC") ? true
```
- str1은 abc라는 값을 가지고, str2는 new String이라는 객체의 주소를 가진다.
- 단순히 abc==abc를 질문하거나 str1==abc를 질문했을때는 true를 반환 하지만 str2는 abc라는 데이터가 아닌 다른 객체의 주소를 가진 변수이므로 str2==abc는 false를 반환한다.
- equals()를 사용하면 객체가 다르다고 해도 내용이 같은 경우 true를 반환한다.
- equalsIgnoreCase()는 대소문자를 구분하지 않고 비교할 수 있다.
- 조건 연산자 ? : 조건식, 식1, 식2. 총 3개의 피연산자를 필요로 하는 삼항 연산자.
- 변수 = 조건식 ? : 식1(조건식이 참일때 변수에 저장) : 식2(조건식이 거짓일때 변수에 저장)
- 대입 연산자 = : 왼쪽 피연산자를 lvalue(left value), 오른쪽 피연산자를 rvalue(right value)라고 부른다. 연산의 진행방향이 오른쪽에서 왼쪽이다.
- 대입연산자의 rvalue는 변수, 상수, 식 등 모두 가능하지만 lvalue는 변수처럼 값을 변경할 수 있는 것 만 사용 가능하기 때문에 리터럴과 상수 등은 사용할 수 없다.

# 클래스와 인스턴스
- 클래스 = 데이터 + 메소드
- 데이터 : 프로그램에서 유지하고 관리하는 데이터
- 메소드 : 데이터를 처리하고 조작하는 기능
- 데이터는 변수의 선언을 통해 유지 및 관리되며 변수에 저장된 데이터는 메소드의 호출을 통해 처리된다.
- 연관있는 변수와 메소드를 하나로 묶기 위해 클래스가 존재한다.

```java
class BankAccountPO {
    static int balance = 0;//예금 잔액 balance 변수 선언

    public static void main(String[] args) {
        deposit(10000);
        checkMyBalance();
        
        withdraw(3000);
        checkMyBalance(); 
    }
    //deposit 메소드는 변수 balance를 위한 메소드이다.
    public static int deposit(int amount) {
        balance += amount;
        return balance;
    }    

    public static int withdraw(int amount) {
        balance -= amount;
        return balance;
    }

    public static int checkMyBalance() {
        System.out.println("잔액 : " + balance);
        return balance;
    }

}
```

- 메소드는 총 3개로 deposit, withdraw, checkMyBalance이다. 이 세 메소드는 balance라는 변수와 함께 묶여서 BankAccount라는 클래스를 이룬다.
- 인스턴스 변수 : 클래스 내에서 선언된 변수
- 인스턴스 메소드 : 클래스 내에 정의된 메소드
- 즉, balance는 인스턴스 변수, deposit, withdraw, checkMyBalance는 인스턴스 메소드이다.
- balance 변수는 **메소드 외부**에서 선언되었기 때문에 **지역변수가 아닌 인스턴스 변수**이다. 인스턴스 변수는 같은 클래스 내에 위치한 메소드 내에서 접근이 가능하다.
- 즉, BankAccount 클래스 안에 들어있는 deposit, withdraw, checkMyBalance 메소드들은 인스턴스 변수인 balance변수에 접근이 가능하다. 따라서 deposit메소드의 매개변수인 amount의 값이 달라지만 인스턴스변수인 balance의 값이 변화한다.
- 인스턴스 변수는 멤버 변수, 필드 라고도 불린다.
<br>
<br>
- 클래스가 정의되었다고 해서 변수나 메소드를 그냥 사용할 수 있는 것은 아니며, 틀을 이용해 인스턴스라는 것을 찍어내야만 사용 가능하다.
- new 클래스 이름 : 해당 클래스를 인스턴스화 한다.
- 클래스를 인스턴스화하면 이 클래스에 정의된 변수와 메소드를 담고있는 인스턴스라는 것이 생성되어 메모리 공간에 올라간다.
- 인스턴스를 만든다고 해서 사용 가능한 것이 아닌, 이 인스턴스를 참조할 수 있는 것이 필요한데 이를 **참조변수**라고 한다.
- static은 시스템 시작과 동시에 자동으로 메모리에 올라가는 것이므로 인스턴스화가 필요하지 않으며 즉시 사용이 가능하다. static이 없다면 인스턴스화가 필요하다.
- 인스턴스 = 객체 / 인스턴스 생성 = 객체 생성
- 클래스의 참조변수 선언 방식은 기본 자료형 변수의 선언 방식과 같다.

```java
class BankAccountOO {
    public static void main(String[] args) {
        //두 개의 인스턴스를 생성한다.
        //각자 다른 메모리 주소를 가진다.
        BankAccount yoon = new BankAccount();
        BankAccount park = new BankAccount();

        yoon.deposit(5000);
        park.deposit(3000);

        yoon.withdraw(2000);
        park.withdraw(2000);

        yoon.checkMyBalance();
        park.checkMyBalance();  
    }
```

- yoon과 park이 각각 다른 인스턴스를 생성한다.
- deposit, withdraw, checkMyBalance 메소드를 각각의 객체가 사용하여 진행한다.

# 생성자
- 생성자는 메소드와 생김새가 같으나 차이점이 있다.
- 생성자의 이름은 클래스의 이름과 같아야 한다.
- 생성자는 값을 반환하지 않고, 반환형도 표시하지 않는다.
- 생성자는 객체가 생성될때(인스턴스화, new 사용시) 자동으로 한 번 호출된다.
- 생성자는 클래스에 최소 1개 필요하며, 생성자 코드가 없다면 자바가 기본형 생성자 코드를 자동으로 생산해 낸다. 다만, 코드 안에 기본형이 아닌 생성자 코드가 1개라도 있다면 자바는 기본생성자를 만들지 않는다.
- 생성자 앞에는 반드시 접근제어자 (public, private등) 만이 올 수 있다. static이 붙는 것은 모두 메소드이다. 또한 생성자는 반환값이 없기 때문에 앞에 자료형을 작성할 수 없다. 메소드는 반드시 자료형을 붙여야 한다.
  
```java

class BankAccount {
    String accNumber;     // 계좌번호
    String ssNumber;     // 주민번호    
    int balance;     // 예금 잔액

    public BankAccount(String acc, String ss, int bal) {
        accNumber = acc;
        ssNumber = ss;
        balance = bal;
    }

    public int deposit(int amount) {
        balance += amount;
        return balance;
    }    

    public int withdraw(int amount) {
        balance -= amount;
        return balance;
    }

    public int checkMyBalance() {
        System.out.println("계좌번호: " + accNumber);
        System.out.println("주민번호: " + ssNumber);
        System.out.println("잔    액: " + balance + '\n');
        return balance;
    }
}
	

class BankAccountConstructor {
    public static void main(String[] args) {
        BankAccount yoon = new BankAccount("12-34-89", "990990-9090990", 10000);
        BankAccount park = new BankAccount("33-55-09", "770088-5959007", 10000);

        yoon.deposit(5000);
        park.deposit(3000);

        yoon.withdraw(2000);
        park.withdraw(2000);

        yoon.checkMyBalance();
        park.checkMyBalance();  
    }
}
```

- 6번째 줄의 public BankAccount(String acc, String ss, int bal) 은 매개변수를 가진 생성자이다.
- 11, 15, 19번째줄의 public int ~~는 메소드 이다. (int 타입 형식이 붙었기 때문)
- 29번째 줄 BankAccount yoon = new BankAccount("12-34-89", "990990-9090990", 10000) 은 인스턴스를 생성하며 생성자를 자동으로 호출한다. 소괄호 안의 값들은 매개변수로 전달 된다. 즉, acc는 12-34-89로, ss는 990990-9090990으로, bal은 10000으로 초기화 된다.
- 생성자를 호출하며 해당 고객의 정보로 초기화 된 후에 deposit과 withdraw를 실행하고 변경된 값을 checkMyBalance로 출력하며 출력 후 최종 balance값을 반환하여 저장한다.(return)

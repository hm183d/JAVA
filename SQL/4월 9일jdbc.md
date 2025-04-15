# 4월 9일

**<font size = 5>[언제 new 할거야?]**</font>

- 이클립스는 정보와 처리로 나누어짐.
- 만약 해당 객체가 이 클래스 전체에 필요하다면 정보부분에 넣고 Heap메모리에 올려야함.
- 만약 해당 객체가 메소드에서만 필요하다면 메소드 안에 넣고 Stack메모리에 올려야함.
- 메소드 안에 객체를 넣어서 new하는 경우는 처리가 종료되면 삭제됨.
- 우선적으로 메소드 안에서 new하여 사용하는것이 좋다. 하지만 메소드가 종료된다고 해서 종료되어서는 안되는 정보라면 밖으로 빼야함.
- 메소드를 분리시키면 코드를 재활용하기가 쉽고, 리딩했을때 전체 내용을 이해하기가 수월함. 또한 추후 수정이 필요한 경우 메소드를 분리시켜놓으면 수정할 부분이 줄어든다.

<br>

```java
Connection con = OracleSession.getSession();//커넥션 열기
```
- 커넥션을 열어서 Oracle과 세션 연결하겠다.(시작)

<br>

```java
try {
			Statement stmt = con.createStatement();//날리고 커밋
			int count = stmt.executeUpdate(sql);
```
- statement를 만들어서 저장하고 해당 횟수를 int로 카운트해서 저장하겠다.

<br>

```java
    if ( 1 == count ){
				con.commit();
			} else {
				con.rollback();
			}
```
- 만약 저장 횟수가 1이면 커밋, 1이 아니라 오류가 발생하면 rollback 취소 한다.

<br>

```java
finally {//이상 없으면 close. 닫지 않으면 메모리 터짐.
			if (null!=con) try{con.close();}catch(Exception e) {e.printStackTrace();}
		}
```
- 앞에서 실행한 try catch 마무리에서 con이 null값이 아니라면 해당 프로그램을 close하겠다.

<br>

```java
String url = "jdbc:oracle:thin:@localhost:1521/xe";
String id = "scott";
		String pw = "tiger";
		Connection con = null;
		
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
			con = DriverManager.getConnection(url,id,pw);
			con.setAutoCommit(false);//수동커밋
			
		} catch (Exception e) {
			e.printStackTrace();
		}
		return con;
```
- xe : SID (해당 오라클의 인스턴스 아이디 / 서비스 아이디)
- localhost : IP
- 1521 : Port
- Class.forName("oracle.jdbc.driver.OracleDriver"); : 해당 드라이버를 new하지 않고 메모리에 올리고 싶을때 사용.
- 수동커밋을 하지 않으면 자동으로 DB에 저장됨. 해당 정보를 커밋할지 롤백할지 직접 확인하려면 수동커밋 해야함.

<br>

[Prepared Statement]
- 입력창에 sql문을 넣으면 sql injection 이 발생하여 데이터에 피해를 줄 수 있음.
- 해당 피해를 막기 위해 prepared statement를 사용하면 명령어로 인식되지 않고 문자로 인식하게 변경해준다.

<br>

```java
String sql = "INSERT INTO MEMBER (ID,PW,NAME,AGE,DOMESTIC_YN) VALUES (?,?,?,?,?)";
		System.out.println(sql);
		try {
			PreparedStatement pstmt = con.prepareStatement(sql);
			pstmt.setString(1, id); // 첫번째 물음표 자리는 id이다.
```
- setString을 선언했으므로 id자리에 명령어를 입력해도 명령어가 아닌 String으로 인식한다.

![](20250409110718.png)

<br>

# SQL (4-1 ~ 4-11)

![](20250409155559.png)
- 테이블 : 모든 정보가 들어감. 성능적으로 빠르게 설계하는 것. 테이블에 있는 정보를 조회(Select문)해야 다음 업무로 넘어감.
- 뷰
- 인덱스
- 프로시저, 연산자, 함수, 패키지 : PL/SQL (oop느낌)
- 트리거 : 특정 트리거가 눌리면 자동실행
- 시퀀스
- 동의어

<br>

- DESC EMP; : EMP테이블에 대하여 설명(DESCRIBE)
- SELECT DISTINCT DEPTNO FROM EMP; : DISTICT(식별, 구별) 중복된 항목을 제거해서 선택.
- SELECT DISTINCT JOB, DEPTNO FROM EMP; : JOB과 DEPTNO를 통틀어서 중복을 제거한다. JOB과 DEPTNO가 모두 같아야만 제거.
- SELECT ENAME, SAL, SAL*12+COMM AS ANNSAL, COMM FROM EMP; : 컬럼명으로 연산식을 쓰지 않도록 AS ANNSAL로 변경가능.

![](20250409171130.png)
- AS를 사용해서 해당 컬럼이 어떤 내용인건지 알 수 없도록 숨길 수 있음.

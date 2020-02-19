



- 데이터 형변환

```java
double pi =3.14   //실수형은 기본타입이 double 
float pi2 = 3.14f // float에 넣고 싶으면 뒤에 f
float pi3 = (float)3.14 // 강제형변환 or 캐스팅 double -> float   8byte -> 4byte 데이터손실 발생 가능
```



```java
String str ="3000";
int value = Integer.parseInt(str);
```



- Scanner

```java
Scanner s = new Scanner(System.in);
System.out.print("국어점수=");
String strkor = s.next();
System.out.println(strkor); //입력값 출력됨
int kor = Integer.parseInt((strkor)); //string -> int
string data = String.valueOf(123); // int -> string
```



- int형으로 데이터 입력 => s.nextInt();

```java
Scanner s = new Scanner(System.in);
System.out.print("국어점수=");
int strkor = s.nextInt();
```



- 아스키코드

```
0 : 48
A: 65
a: 97
```



- 단축키

  - psvm

    ```java
    public static void main(String[] args) {
         
        }
    ```

  - sout

    ```java
    System.out.println();
    ```

    






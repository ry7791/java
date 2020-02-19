

- equals : 내용이 같은지 확인 시켜줌

```java
String hello = "Hello"; 
String name = "Hello";
 String newName = new String("Hello");

 System.out.println(hello == name);
// true => 변수는 스택에 따로 저장되지만 변수안에 데이터는 힙에 있는 같은 "Hello"를 사용중으므로 true
 System.out.println(name == newName); 
// false => new를 쓰면  힙에 새로운 "Hello"가 만들어지므로 name과 newName의 "Hello"는 다름 
 System.out.println(name.equals(newName)); 
// true => equals는 내용이 같은지만 확인해줌
```



| stack | heap |
| ----- | ---- |
|       |      |



- 배열 생성

  - 값 목록으로 배열 생성

  ```
  타입[] 변수 = {값0, 값1, 값2, ...};
  ```

  - new 연산자를 이용해서 배열 생성

  ```
  int[] scores = new int[30];
  ```



- arraycopy

```java
 String[] strArray = new String[3];
        strArray[0] = "Java 1.8";
        strArray[1] = "java 1.2";
        strArray[2] = new String("java 1.13");

        String[] newArray = new String[3];
        System.arraycopy(strArray,1,newArray,0, 2);

        for(String str: newArray){
            System.out.println(str);
        }
        
// =>
// java 1.2
// java 1.13
// null
```



- 로또 예제

```java
package com.example.day2;

import java.util.Random;
import java.util.Scanner;

public class example2 {
    public static void main(String[] args) {
        int[] num = new int[6];
        int[] lotto = new int[6];
        System.out.print("번호를 입력하시오 : ");
        Scanner s = new Scanner(System.in);
        Random ran = new Random();
        for(int i=0;i<6; i++){
            System.out.print(" ");
            num[i]= s.nextInt();
            lotto[i] = ran.nextInt(45)+1;
        }

        int correct=0;
        for(int i=0;i<6; i++) {
            for(int j=0; j<6;j++){
            if(num[i]==lotto[j]) correct++;
            }
        }
        System.out.println("");
        System.out.println("내가 뽑은 번호 : ");
        for(int i=0;i<6; i++) {
            System.out.print(num[i]+" ");
        }
        System.out.println("");
        System.out.println("당첨 번호 : ");
        for(int i=0;i<6; i++) {
            System.out.print(lotto[i]+" ");
        }
        System.out.println("");
        System.out.println("일치 갯수 : "+correct);

        switch(correct){
            case 6:
                System.out.println("1등입니다");
            case 5:
                System.out.println("2등입니다");
            case 4:
                System.out.println("3등입니다");
            case 3:
                System.out.println("4등입니다");
            default:
                System.out.println("꽝입니다");
        }
    }
}

```


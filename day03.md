pom.xml 이 나오면 Mavern Project라고 보면 됨









- lombok이라는 플러그인

```java
package com.example.testdemo;

import lombok.Data;

@Data
public class Member {
   private String name;
   private String ssn;
   private String birthday;


}

```

 

```java
package com.example.testdemo;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class TestMember {
    @Test
    public void testAddMember(){
        Member member = new Member();
        member.setName("정욱");

        assertEquals("정욱",member.getName());
    }
}

// 롬복을 쓰면 세터 게터를 선언 안해도  바로 사용가능
```













- 부모 자식 클래스

  - overriding : 부모의 메소드를 자식에서 다시 정의하는 것

  

  부모 Member.java

  ```java
  package com.example.day4;
  
  public abstract class Member {
      protected String id;
      protected String grade;
      protected double point;
  
  //    public abstract void setPoint(int point){
  //        this.point = point;
  //    }
      public abstract void setPoint(int point);
      public abstract boolean isAuthorized(String grade);
  
  //    public void display(){
  //        System.out.printf("%s는 %s등급 (Point=%s)\n",id, grade, point);
  //    }
  
      public abstract void display();
  }
  
  ```

  자식 VvipMember

  ```java
  package com.example.day4;
  
  public class VvipMember extends Member{
      public VvipMember(String id){
          this.id = id;
          this.grade = "V1";
      }
  
      @Override
      public void setPoint(int point){
          this.point = point*1;
      }
  
      @Override
      public boolean isAuthorized(String grade) {
          return true;
      }
  
      @Override
      public void display() {
          System.out.println("#################################");
          System.out.printf("%s, %s, %s\n", super.id, grade, point);
          System.out.println("#################################\n\n");
      }
  }
  
  ```



​		자식 VipMember

```java
package com.example.day4;

public class VipMember extends Member{
    public VipMember(String id, String grade){
        this.id = id;
        this.grade = grade;
    }

    @Override
    public void setPoint(int point){
        this.point = point*0.5;
    }

    @Override
    public boolean isAuthorized(String grade) {
        return true;
    }

    @Override
    public void display() {
        System.out.println("*********************************");
        System.out.printf("%s, %s, %s\n\n", super.id, grade, point);
        // 자식에서 부모를 가리킬 때 super를 사용
    }
}

```

​		자식 GeneralMember

```java
package com.example.day4;

public class GeneralMember extends Member{
    public GeneralMember(String id, String grade){
        this.id = id;
        this.grade = grade;
    }

    @Override
    public void setPoint(int point){
        this.point = point*0.3;
    }

    @Override
    public boolean isAuthorized(String grade) {
        return false;
    }

    @Override
    public void display() {
        System.out.printf("%s, %s, %s\n\n", super.id, grade, point);
    }
}

```

MemberApp.java

```java
package com.example.day4;

public class MemberApp {
    public static void main(String[] args) {

        // Abstract class는 instance 생성 못함
        GeneralMember mem1 = new GeneralMember("user1","A");
        mem1.setPoint(100);
        mem1.display();

        VipMember mem2 = new VipMember("user2", "S");
        mem2.setPoint(100);
        mem2.display();

        VvipMember mem3 = new VvipMember("user3");
        mem3.setPoint(100);
        mem3.display();

    }
}

```



-----------------------------------------------------------------------------------------------------------------------------------------------------------





## interface

```java
package com.example.day4;

public interface IMemberFunc {

    void setPoint(int point);

    boolean isAuthorized();

    void display();

}

```



```java
package com.example.day4;

// Abstract class -> interface (추상 메소드, 약속)
//      정상 메소드 -> public void add(){...}
//      추상 메소드 -> public void add();

import java.util.Date;

public class Member {

     String id; // interface에서는 모든 것이 public static final 으로 선언됨
    String grade;
     double point;
     Date joinDate;
}

```



```java
package com.example.day4;

import java.util.Date;

public class GeneralMember extends Member implements IMemberFunc{
    GeneralMember(String id, String grade){
        this.id = id;
        this.grade = grade;
        this.joinDate = new Date();
    }


    public void setPoint(int point){
        this.point = point*0.3;
    }


    public boolean isAuthorized() {
        return false;
    }

    public void display() {
        System.out.printf("%s, %s, %s, %s\n\n", super.id, grade, point,joinDate);
    }
}
------------------------------------------------------------------

package com.example.day4;

import java.util.Date;

public class VipMember extends Member implements IMemberFunc{
    public VipMember(String id, String grade){
        this.id = id;
        this.grade = grade;
        this.joinDate = new Date();
    }

    @Override
    public void setPoint(int point){
        this.point = point*0.5;
    }

    @Override
    public boolean isAuthorized() {
        return true;
    }

    @Override
    public void display() {
        System.out.println("*********************************");
        System.out.printf("%s, %s, %s, %s\n\n", super.id, grade, point,joinDate);
    }
}

--------------------------------------------------------------------

package com.example.day4;

import java.util.Date;

public class VvipMember extends Member implements IMemberFunc{
    public VvipMember(String id){
        this.id = id;
        this.grade = "V1";
        this.joinDate = new Date();
    }
    @Override
    public void setPoint(int point){
        this.point = point*1;
    }
    @Override
    public boolean isAuthorized() {
        return true;
    }

    @Override
    public void display() {
        System.out.println("#################################");
        System.out.printf("%s, %s, %s, %s\n\n", super.id, grade, point,joinDate);
        System.out.println("#################################\n\n");
    }
}



```

```java
package com.example.day4;

public class MemberApp2 {
    public static void main(String[] args) {

        GeneralMember mem1 = new GeneralMember("user1", "A");
        GeneralMember mem2 = new GeneralMember("user2", "B");
        VipMember vip1 = new VipMember("vip1", "S1");
        VipMember vip2 = new VipMember("vip2", "S1");
        VvipMember vvip1 = new VvipMember("vvip1");

        //Array
        // 부모의 reference 변수는 자식의 인스턴스를 가리킬 수 있다.
        //Member[] members = new Member[5];
        IMemberFunc[] members = new IMemberFunc[5];
        members[0] = mem1;
        members[1]  = mem2;
        members[2]  = vip1;
        members[3]  = vip2;
        members[4]  = vvip1;

//        for (Member member : members){
//            System.out.println(member.id + "/" + member.joinDate);
//
//        }
//        for(IMemberFunc : members){
//            member.setpoint(100);
//            member.displayInfo();
//        }

        Object[] obj = new Object[3];
        obj[0] = new GeneralMember("user3","C");
        obj[1] = new VipMember("vip3","S3");
        obj[2] = new VvipMember("vvip3");

        for(Object o : obj){
            IMemberFunc member = null;
            if( o instanceof GeneralMember){
                member = (GeneralMember) o;
            } else if( o instanceof VipMember){
                member = (VipMember) o;
            } else if(o instanceof VvipMember){
                member = (VvipMember) o;
            }

            member.setPoint(200);
            member.display();
        }

    }
}

```


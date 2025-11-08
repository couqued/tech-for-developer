## java.lang 패키지
- import 하지 않고 기본적으로 사용이 가능하다.
- java.lang 패키지에는 기본형타입을 객체로 변환시킬 때 사용하는 Wrapper클래스가 있다.
- Boolean, Byte, Short, Integer, Long, Float, Double 클래스
- 아래는 모두 java.lang 패키지
   모든 클래스의 최상위 클래스인 Object <br>
   문자열과 관련된 String, StringBuffer, StringBuilder <br>
   화면에 값을 출력할때 사용했던 System클래스 <br>
   수학과 관련된 Math클래스 <br>
   Thread와 관련된 중요 클래스 <br>

---
<br>

> 오토박싱 (Auto Boxing)
- 기본형(int) 타입을 자동으로 객체타입 (Integer) 형태로 변환해준다.

> 오토언박싱 (Auto unboxing)
- 객체 타입 (Integer)의 값을 기본형(int)으로 자동 변환해준다.

> 오토박싱, 오토언박싱은 JAVA5부터 지원한다. 이때 내부적으로 Wrapper 클래스들이 사용된다.

#### 예시
```JAVA
public class WrapperExamCode {
    public static void main(String[] args) {
        Integer itga = new Integer(2);
        int ia = itga.intValue();

        Integer itgb = 10;   //오토박싱
        int ib = itga;       //오토언박싱
    }
}
```
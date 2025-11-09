### StringBuffer는 자기자신을 반환함 (this)

### 자기 자신을 계속해서 호출하여 자신의 값을 바꿔나가는 방식
> 메소드 체이닝 (Method Chaingin)

### 예시
``` Java
public static void main(String[] args) {
    StringBuffer sb = new StringBuffer();  // StringBuffer 객체 생성
    sb.append("Hello");
    sb.append(" ");
    sb.append("World");
    System.out.println(sb.toString());  // StringBuffer 객체를 toString 메소드를 이용하여 반환

    StringBuffer sb2 = new StringBuffer();
    StringBuffer sb3 = sb2.append("Hello");

    if(sb2 == sb3)
        System.out.println("true");

    // 메소드체이닝
    String str = new StringBuffer().append("Hello").append(" ").append("World").toString();
    System.out.println(str);
}
```

### String 클래스 주의사항
String을 더할 때 내부적으로는 아래와 같이 작동한다.
```Java
String str1 = "Hello";
String str2 = "World";
String str3 = str1 + str2;
System.out.println(str3); // HelloWorld

//내부적으로 다음 코드가 실행됨
String str4 = new StringBuffer().append(str1).append(str2).toString();
System.out.println(str4); // HelloWorld
```
> 위와 같이 작동되기 때문에 반복문 안에서 문자열을 합하는 로직을 실행할때는 성능상 효율적인 StringBuffer를 사용하는것이 좋다.
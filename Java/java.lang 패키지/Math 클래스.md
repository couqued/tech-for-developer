### 수학계산을 위한 클래스

#### 생성자가 private으로 되어 있기 때문에 new 연산자를 이용해 객체를 생성할 수 없다.
#### 객체를 생성할 수 없지만 모든 메소드와 속성이 static으로 정의되어 있기 때문에 객체를 생성하지 않고 사용할 수 있다.

```Java
public static void main(String[] args) {
    int value1 = Math.max(5, 20);  //최대값
    int value2 = Math.min(5, -5);  //최소값
    int value3 = Math.abs(-10);    //절대값
    double value4 = Math.random(); //랜덤값 : Double타입으로 0~1 사이 값을 리턴
    double value5 = Math.sqrt(25); //제곱근의값
}
```
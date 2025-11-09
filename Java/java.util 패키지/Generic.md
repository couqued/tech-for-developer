### Generic 문법을 사용하여 인스턴스를 만들때 사용하는 타입을 지정
<br>
클래스 이름 뒤에 <E>가 제너릭을 적용한것으로 가상의 클래스E를 사용한다는 의미 (실제 존재하지 않음)

```Java
public class Box<E> {
    private E obj;

    public void setObj(E obj){
        this.obj = obj;
    }

    public E getObj(){
        return obj;
    }
}
```
<br>

참조 타입에 Object, String, Integer 사용
각 타입으로 Box 인스턴스를 만듬

```Java
public static void main(String[] args) {
//        Box box = new Box();
//        box.setObj(new Object());
//        Object obj = box.getObj();
//
//        box.setObj("hello");
//        String str = (String)box.getObj();
//        System.out.println(str);
//
//        box.setObj(1);
//        int value = (int)box.getObj();

        Box<Object> box = new Box<>();
        box.setObj(new Object());
        Object obj = box.getObj();

        Box<String> box2 = new Box<>();
        box2.setObj("Hello");
        String str = box2.getObj();

        Box<Integer> box3 = new Box<>();
        box3.setObj(1);
        int value = box3.getObj();
    }
```
<br>

  - Generic을 사용함으로써 선언할때는 가상의 타입으로 선언하고, 사용시에는 구체적인 타입을 설정.
  - 다양한 타입의 클래스를 만들 수 있기 때문에 Object로 반환되어 다시 형변환하지 않아도 됨.
  - Generic을 사용하는 대표적인 클래스는 컬렉션 프레임워크와 관련된 클래스


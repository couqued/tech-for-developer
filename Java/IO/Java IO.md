
### 입출력을 위한 인터페이스와 클래스들
자바 IO는 크게 
- byte단위 입출력과 문자 단위 입출력 클래스로 나뉨
- byte단위 입출력클래스는 모두 InputStream과 OutputStream이라는 추상클래스를 상속받아 만들어짐
- 문자(char)단위 입출력클래스는 모두 Reader와 Writer라는 추상클래스를 상속받아 만들어짐


- 파일 입출을 위한 클래스 : FileInputStream, FileOutputStream, FileReader, FileWriter
- 배열 입출력을 위한 클래스 : ByteArrayInputStream, ByteArrayOutputStream, CharReader, CharWriter
    - 해당 클래스들은 어디로부터, 어디에라는 대상을 지정할 수 있는 IO클래스로 장식대상 클래스

- DataInputStream, DataOutputStream 같은 클래스는 다양한 데이터 형을 입력받고 출력함
- PrintWriter는 다양하게 한줄 출력하는 pintln()메소드가 있음
- BufferedReader는 한줄 입력받는 readLine()메소드가 있음
    - 해당 클래스들은 다양한 방식으로 입출력하는 기능을 제공하는 장식하는 클래스

<br>

#### byte 단위 입출력 예제
```Java
public static void main(String[] args) {
    FileInputStream fis = null;
    FileOutputStream fos = null;

    try {
        fis = new FileInputStream("src/main/java/exam.java");
        fos = new FileOutputStream("byte.txt");

        int readData = -1;
        while((readData = fis.read()) != -1){  // 더 이상 읽어들일것이 없을때 -1을 리턴
            fos.write(readData);
        }

    } catch (Exception e) {
        e.printStackTrace();
    }finally {
        try {
            fos.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        try {
            fis.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }

}
```

<br>

#### byte 단위 입출력 예제2 (512byte씩 읽기)
```Java
public static void main(String[] args) {
    long startTime = System.currentTimeMillis();  //메소드 시작 시간

    FileInputStream fis = null;
    FileOutputStream fos = null;

    try {
        fis = new FileInputStream("src/main/java/org/example/cote/setExam.java");
        fos = new FileOutputStream("byte.txt");

        int readCount = -1;
        byte[] buffer = new byte [512];  //512byte로 읽기
        while((readCount = fis.read(buffer)) != -1){  // 더 이상 읽어들일것이 없을때 -1을 리턴
            fos.write(buffer, 0, readCount);
        }

    } catch (Exception e) {
//            throw new RuntimeException(e);
        e.printStackTrace();
    }finally {
        try {
            fos.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        try {
            fis.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
    long endTime = System.currentTimeMillis();  //메소드 종료시간
    System.out.println("Time : " + (endTime - startTime));  //메소드 수행시간
}
```

<br>

#### try-with-resources 블럭 및 DataOutputStream 사용
io 객체 인스턴스를 만들고 사용 후 close()를 하지 않더라도 Exception이 발생하지 않았다면 자동으로 close() 됨

```Java
public static void main(String[] args) {
    try(
            DataOutputStream out = new DataOutputStream(new FileOutputStream("data.txt"));
            ){
        out.writeInt(100);
        out.writeBoolean(true);
        out.writeDouble(10.5);
    }catch (Exception e){
        e.printStackTrace();
    }
}
```

<br>

#### DataInputStream으로 파일 내용 읽기
```Java
public static void main(String[] args) {
    try(
            DataInputStream in = new DataInputStream(new FileInputStream("data.txt"));
            ){
        int i = in.readInt();
        boolean b = in.readBoolean();
        double d = in.readDouble();
        System.out.println("i : " + i + " b : " + b + " d : " + d);  //i : 100 b : true d : 10.5
    }catch (Exception e){
        e.printStackTrace();
    }
}
```

<br>

#### char 단위 입출력 (console)
```Java
public static void main(String[] args) {

    // System.in은 InputStream 타입이므로 BufferedReader의 생성자에 바로 들어갈 수 없으므로 InputStreamReader 클래스를 이용해야함.
    // System.in : 키보드 입력
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    
    String line = null;
    
    try {
        line = br.readLine();
    } catch (IOException e) {
        e.printStackTrace();
    }
    
    //콘솔에 출력
    System.out.println(line);
}
```

<br>

#### char 단위 입출력 (File)
```Java
public static void main(String[] args) {
    BufferedReader br = null;
    PrintWriter pw = null;
    try {
            br = new BufferedReader(new FileReader("src/main/java/org/example/cote/setExam.java"));
            pw = new PrintWriter(new FileWriter("test.txt"));

            String line = null;
            while((line = br.readLine()) != null){
                pw.println(line);
            }
    } catch (Exception e) {
        e.printStackTrace();
    }finally {
        pw.close();
        try {
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
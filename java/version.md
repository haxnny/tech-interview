# 자바 버전별 특징

## Java 8
[Oracle 웹 사이트](https://www.oracle.com/java/technologies/javase/8-whats-new.html) 에서 모든 기능 목록 확인 가능
* Lambda
* stream
* interface default method
* Optional
* new Date and Time API (LocalDateTime, ...)

#### Lambda
Java 8 이전 익명 클래스의 사용을 Lambda 이용하여 더욱 간결하고 직관적으로 구현 가능

```Java
Runnable runnable = new Runnable() {
  @Override
  public void run() {
    System.out.println(*"Hellow world!"*);
  }
}
```

```Java
Runnable runnable = () -> System.out.println(*"Hellow world!"*);
```

#### Stream
Java 8은 Stream API를 통해 컬렉션을 처리하면서 발생하는 `모호함과 반복적인 코드 문제`와 `멀티코어 활용 어려움`이라는 두 가지 문제를 모두 해결
```Java
    List<String> list = Arrays.asList(*"franz"*, *"ferdinand"*, *"fiel"*, *"vom"*, *"pferd"*);
    list.stream()
        .filter(name -> name.startsWith(*"f"*))
        .map(String::toUpperCase)
        .sorted()
        .forEach(System.out::println);
```


## Java 9
모듈시스템의 등장 (jigsaw)

#### Collection
컬렉션에서 list, set, map 을 쉽게 구성할 수 있는 기능 추가
```Java
List<String> list = List.of(*"one"*, *"two"*, *"three"*);
Set<String> set = Set.of(*"one"*, *"two"*, *"three"*);
Map<String, String> map = Map.of(*"foo"*, *"one"*, *"bar"*, *"two"*);
```

#### Stream
takeWhile, dropWhile, iterate 메서드의 형태로 추가 기능
```Java
Stream<String> stream = Stream.iterate(*""*, s -> s + *"s"*)
  .takeWhile(s -> s.length() < 10);
```

#### Optional
ifPresentOrElse 추가 기능
```Java
user.ifPresentOrElse(this::displayAccount, this::displayLogin);
```


#### 인터페이스
private method 사용 가능
```Java
public interface MyInterface {

    private static void myPrivateMethod(){
        System.out.println(*"Yay, I am private!"*);
    }
}
```


## Java 10
로컬 변수 유형 추론 "var" 키워드 도입
* var 키워드
* 병렬 처리 가비지 컬렉션 도입으로 인한 성능 향상
* JVM 힙 영역을 시스템 메모리가 아닌 다른 종류의 메모리에도 할당 가능

지역 변수 유형 추론 : var-keyword
* Pre-Java 10
```Java
String myName = "haenny";
```
* With Java 10
```Java
var myName = "haenny";
```
Java 에서 var 예약어를 사용하면 중복을 줄임으로써 코드를 간결하게 만들 수 있음
* var 키워드는 지역 변수 타입 추론을 허용
* `메서드 내부의 변수`에만 적용 가능


## Java 11
* Oracle JDK와 OpenJDK 통합
* Oracle JDK가 구독형 유료 모델로 전환
* 서드파티 JDK 로의 이전 필요
* lambda 지역변수 사용법 변경
* 기타 추가

#### String & Files
Strings and Files에는 몇 가지 새로운 메서드 추가
```Java
*"Marco"*.isBlank();
*"Mar\nco"*.lines();
*"Marco  "*.strip();

Path path = Files.writeString(Files.createTempFile(*"helloworld"*, *".txt"*), *"Hi, my name is!"*);
String s = Files.readString(path);
```

#### Lambda 매개변수에 대한 지역 변수 유형 추론 (var)
lambda 표현식에 var 사용 가능
```Java
(var firstName, var lastName) -> firstName + lastName
```
# CS : Java stream

## Stream

Stream API는 Java 8부터 나온 개념으로, 객체의 컬렉션을 다루기 위해 만들어졌다. 

Stream은 객체들의 순서로서, 원하는 결과를 만들기 위한 다양한 연산을 지원한다.

<aside>
➕ 자바의 람다(익명) 함수

---

자바 8부터 도입된 기능으로, 함수형 프로그래밍 스타일을 지원하기 위해 추가

java.util.Function 패키지의 람다함수 관련 메서드들을 사용가능

### 특징

1. 간결한 문법: 람다 함수는 코드를 간결하게 작성할 수 있음
2. 함수형 인터페이스와 결합: 람다 함수는 함수형 인터페이스(functional interface)와 함께 사용됩니다. 함수형 인터페이스는 단 하나의 추상 메서드를 가지는 인터페이스이며, 람다 함수는 이 추상 메서드를 구현한 코드 블록으로 대체됩니다.
3. 간접적인 함수 전달: 람다 함수는 다른 함수에게 전달되거나 변수에 할당될 수 있습니다. 이를 통해 함수를 인자로 받는 메서드나 함수형 인터페이스를 더욱 효과적으로 활용할 수 있습니다.

### 예시

```java
int plus(int a, int b){
	return a + b;
}

Function<Integer, Integer> func = (int a) -> { return a / 2; }
```

</aside>

### Stream의 특징

- Stream은 자료구조가 아니며, Collections나 배열, I/O 채널을 input으로 받는다.
- Stream은 기존의 자료구조를 바꾸지 않으며, 파이프라인화 된 메서드를 통해 결과를 제공한다.
- 각각의 과정들은 최종 연산 전까지 중간연산을 수행되지 않으며, 결과적으로 Stream을 리턴하기 때문에, 다양한 작업을 파이프라인화 할 수 있다. 터미널 연산은 스트림의 끝을 표시하고, 결과를 리턴한다.

### Stream vs for loop

|  | for loop | streamAPI |
| --- | --- | --- |
| 장점 | - 직관적이고 익숙한 문법
- 인덱스 접근
- 반복 도중 제어 → break, continue 사용 | - 간결하고 선언적인 문법
- 내부 반복 처리
- 병렬 처리 지원 |
| 단점 | - 코드의 가독성과 유지보수
- 컬렉션 데이터에 대한 추상화 부족
- 병렬 처리 어려움 | - 학습 비용
- 상태 변경 제한
- 재사용의 어려움 |

### Stream의 다양한 연산들

1. 중간 연산
    1. map() : 스트림의 각 객체에 대하여 주어진 함수를 적용한 stream을 리턴한다.
        
        ```java
        List number = Arrays.asList(2,3,4,5);
        List square = number.stream().map(x->x*x).collect(Collectors.toList());
        ```
        
    2. filter() : 주어진 함수가 true이면 포함, false이면 포함하지 않은 stream을 리턴한다.
        
        ```java
        List names = Arrays.asList("Reflection","Collection","Stream");
        List result = names.stream().filter(s->s.startsWith("S")).collect(Collectors.toList());
        ```
        
    3. sorted() : stream을 정렬하여 리턴한다.
        
        ```java
        List names = Arrays.asList("Reflection","Collection","Stream");
        List result = names.stream().sorted().collect(Collectors.toList());
        ```
        
2. Terminal Operations
    1. collect() : stream에서 수행한 연산의 결과를 얻기 위해 사용된다.
        
        ```java
        List number = Arrays.asList(2,3,4,5,3);
        Set square = number.stream().map(x->x*x).collect(Collectors.toSet());
        ```
        
    2. foreach() : stream 내의 모든 객체를 반복해야할 때 사용한다.
        
        ```java
        List number = Arrays.asList(2,3,4,5);
        number.stream().map(x->x*x).forEach(y->System.out.println(y));
        ```
        
    3. reduce() : stream의 원소를 하나의 값으로 만들어야 할 때 사용한다. BinaryOperator를 파라메터로 사용한다.
        
        ```java
        List number = Arrays.asList(2,3,4,5);
        int even = number.stream().filter(x->x%2==0).reduce(0,(ans,i)-> ans+i);
        ```
        

### Collectors

collect() 함수에 인자로 들어가는 인터페이스로서, stream의 인자들을 모아서 어떤 형태로 반환할건지 정한다.

- collect(Collectors.toList())
- collect(Collectors.toSet())
- collect(Collectors.toMap())
- collect(Collectors.groupingBy()) : 인자들을 그룹화 하여 map을 리턴한다.

### 실제 사용 예시

```java
// 문자열을 정수 배열로 만듬
String inputs = "1 2 3 4 5 6";
int[] arr = Arrays.stream(inputs.split(" ")).mapToInt(Integer::parseInt).toArray();

// fruits 리스트의 빈도수를 셈
List<String> fruits = Arrays.asList("apple", "apple", "banana", "banana", "pear");
Map<String, Long> counts = fruits.stream().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
```
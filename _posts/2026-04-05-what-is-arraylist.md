---
title: ArrayList란 무엇인가
date: 2026-04-05 22:00:00 +0900
categories: [Blog, Java]
tags: [java, data structure, arraylist]
description: >-
    
---

## 1. ArrayList란 무엇인가 

자바에서 여러 데이터를 다룰 때 가장 먼저 배우는 구조는 배열(Array)이다.<br/>
배열은 같은 타입의 값을 묶어서 저장할 수 있고, 인덱스로 바로 접근할 수 있어 빠르고 단순하다.<br/>
하지만 한 번 생성하면 크기를 바꿀 수 없다는 한계가 있다.

반면 ArrayList는 `java.util`패키지에서 제공하는 **크기가 자동으로 늘어나고 줄어드는 리스트**로, 배열처럼 인덱스로 접근할 수 있으면서도 요소 추가와 삭제에 맞춰 크기를 유연하게 관리할 수 있다.
또한 중복 저장이 가능하고, 입력한 순서를 유지하며, 기본적으로 thread-safe 하지는 않다.

처음에는 ArrayList를 단순히 "크기 늘어나는 배열" 정도로만 생각하기 쉽운데, 정리해보면 단순 편의 기능 이상의 의미가 있다.<br/>
배열의 장점인 **빠른 조회**는 유지되면서, **추가/삭제의 유연성**을 제공하기 때문이다.<br/>
그래서 자바를 공부하다 보면 배열 다음으로 자연스럽게 ArrayList를 배우게 되는 것 같다.

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> numbers = new ArrayList<>();

        numbers.add(10);
        numbers.add(20);
        numbers.add(30);

        System.out.println(numbers); // [10, 20, 30]
    }
}
```

---

## 2. 배열과 ArrayList의 차이

배열과 ArrayList는 겉보기에는 비슷하다. 둘 다 여러 값을 순서대로 저장하고, 인덱스로 접근할 수 있기 때문이다.<br/>
하지만 가장 큰 차이는 **크기 관리 방식**에 있다.

배열은 생성 시 크기를 정하면 끝까지 고정되지만, ArrayList는 요소 수에 따라 내부 공간을 조정하면서 동적으로 동작한다.<br/>
또 하나 중요한 차이는 저장 타입이다. 배열은 기본형과 참조형을 모두 직접 저장할 수 있지만, ArrayList는 기본형을 직접 담을 수 없고, `Integer`, `Double`, `Character` 같은 래퍼 클래스(Wrapper Class)를 사용해야 한다.

예를 들어 `ArrayList<int>`는 불가능하고, `ArrayList<Integer>`는 가능하다.<br/>

정리하자면 배열은 **고정 크기의 단순한 구조**, ArrayList는 **가변 크기의 편리한 구조**라고 볼 수 있다.<br/>
배열은 크기가 명확히 정해진 데이터를 다룰 때 적합하고, ArrayList는 데이터 개수가 변할 가능성이 있는 상황에서 훨씬 실용적이다.

---

## 3. ArrayList의 주요 특징 

ArrayList를 공부할 때는 단순히 "추가하고 삭제하는 리스트"로 외우기보다, 어떤 특징을 가지는지 먼저 정리하는 게 좋다.

1. **인덱스로 접근할 수 있다**<br/>
배열처럼 `get(index)` 방식으로 특정 위치의 값을 읽을 수 있다. 이는 내부적으로 배열 기반 구조를 사용하기 때문이다.

2. **중복 저장이 가능하다**<br/>
같은 값을 여러 번 넣어도 문제되지 않는다. 예를 들어 "Java"를 두 번 넣으면 두 개 모두 저장된다.

3. **삽입 순서를 유지한다**
먼저 넣은 값이 앞에, 나중에 넣은 값이 뒤에 저장된다. 그래서 순서가 중요한 데이터 목록을 관리할 때 편리하다.

4. **기본적으로 thread-safe 하지 않다**<br/>
즉 여러 스레드가 동시에 수정하는 환경에서는 별도 동기화가 필요하다.<br/>
   [GeeksforGeeks](https://www.geeksforgeeks.org/java/arraylist-in-java/)에서는 `Collections.synchronizedList()`로 감싸는 방식을 예시로 든다.

이 특징들을 보면 ArrayList는 "순서가 있는 데이터 목록을 유연하게 다루기 위한 자료구조"라고 이해하면 될 것 같다.

---

## 4. ArrayList 선언과 생성 방법 

ArrayList는 상황에 따라 여러 방식으로 생성할 수 있다. 

### 1. 기본 생성자

가장 일반적인 방식은 빈 ArrayList를 만드는 것이다.
```java
ArrayList<String> list = new ArrayList<>();
```
이 방식은 가장 자주 사용된다.<br/>
처음에는 비어 있는 리스트를 만들고, 이후 `add()`로 요소를 추가해 나가는 형태이다.

### 2. 초기 용량을 지정하는 생성자 
```java
ArrayList<Integer> list = new ArrayList<>(20);
```
이 방식은 내부 저장 공간의 초기 크기를 미리 정하는 것이다.<br/>
처음부터 데이터가 꽤 많이 들어올 것을 예상한다면, 미리 어느 정도 용량을 잡아두는 것이 불필요한 확장을 줄이는 데 도움이 될 수 있다.

### 3. 다른 컬렉션으로 초기화하는 생성자

```java
ArrayList<String> list = new ArrayList<>(anotherCollection);
```
이 방식은 기존 컬렉션의 값을 바탕으로 새로운 ArrayList를 만드는 방식이다.<br/>
이미 존재하는 데이터 목록을 복사하거나, 다른 컬렉션을 ArrayList 형태로 바꾸고 싶을 때 유용하다.

즉 ArrayList는 단순히 빈 리스트만 만드는 구조가 아닌, **빈 상태로 시작할 수도 있고, 예상 크기를 미리 줄 수도 있으며, 기존 데이터를 바탕으로 시작할 수도** 있다는 점이 중요한 것 같다.

---

## 5. ArrayList의 기본 사용법 

ArrayList를 실제로 사용할 때 가장 자주 하는 동작은 크게 다섯 가지이다.
- 값 추가하기
- 값 조회하기
- 값 수정하기 
- 값 삭제하기
- 전체 순회하기 

### 1. 값 추가하기 

가장 기본적인 추가는 맨 뒤에 값을 넣는 것이다.
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> subjects = new ArrayList<>();
        
        subjects.add("Java");
        subjects.add("Spring");
        subjects.add("JPA");

        System.out.println(subjects); // [Java, Spring, JPA]
    }
}
```
`add(E e)`는 리스트의 맨 끝에 요소를 붙인다.<br/>
배열처럼 몇 번째 칸을 미리 정해놓지 않아도 된다는 점이 편하다.

### 2. 특정 위치에 값 추가하기 
```java
subjects.add(1, "Backend");
System.out.println(subjects); // [Java, Backend, Spring, JPA]
```
인덱스를 지정하면 해당 위치에 값이 들어가고, 그 뒤에 있던 요소들은 오른쪽으로 한 칸씩 밀리게 된다.<br/>
즉, 중간 삽입은 가능하지만 요소 간 이동이 발생한다는 점을 같이 이해해야 한다.

### 3. 값 조회하기
```java
System.out.println(subjects.get(0)); // Java 
```
`get(index)`를 사용하면 특정 위치의 요소를 읽을 수 있다.<br/>
이 방식이 빠른 이유는 ArrayList가 내부적으로 배열 기반이기 때문이다.

### 4. 값 수정하기 
```java
subjects.set(0, "Java SE");
System.out.println(subjects); // [Java SE, Backend, Spring, JPA]
```
`set(index, element)`는 해당 위치의 기존 값을 새로운 값으로 교체한다.<br/>
추가가 아닌 덮어쓰기라는 점을 구분하자.

### 5. 값 삭제하기 

삭제는 두 방식이 존재한다.
```java
subjects.remove(1);         // 인덱스로 삭제
subjects.remove("Spring");  // 값으로 삭제
```
인덱스로 삭제하면 해당 위치의 요소가 제거되고, 뒤 요소들이 앞으로 당겨진다.<br/>
값으로 삭제하면 가장 먼저 발견한 해당 값 하나를 지운다.

원문에서도 `remove(int index)`와 `remove(Object o)`를 구분해서 설명한다.

### 6. 전체 순회하기 

```java
for (int i = 0; i < subjects.size(); i++) {
    System.out.println(subjects.get(i));    
}
```
또는 향상된 for문도 많이 쓴다.

```java
for (String subject : subjects) {
    System.out.println(subject);
}
```
여기서 중요한 점은 배열처럼 length를 쓰는 것이 아닌, ArrayList는 `size()`로 현재 요소 개수를 확인한다.

---

## 6. 자주 사용하는 주요 메서드 정리 

ArrayList에는 메서드가 많지만, 자주 쓰는 것 위주로 정리하는 편이 좋다고 생각한다.

### 추가 관련 
```java
list.add("A");
list.add(1, "B");
list.addAll(otherList);
```
- `add(E e)`: 맨 뒤에 요소 추가 
- `add(int index, E element)`: 특정 위치에 요소 추가 
- `addAll(Colleciton c)`: 다른 컬렉션 전체 추가 

### 조회 관련 
```java
list.get(0);
list.contains("A");
list.indexOf("A");
lisst.isEmpty();
list.size();
```
- `get(int index)`: 해당 위치 요소 조회 
- `contains(Object o)`: 포함 여부 확인 
- `indexOf(Object o)`: 처음 등장한 위치 반환
- `isEmpty()`: 비어 있는지 확인 
- `size()`: 현재 요소 개수 반환 

### 수정 관련 
```java
list.set(0, "Z");
```
- `set(int index, E element)`: 요소 값 변경 

### 삭제 관련 
```java
list.remove(0);
list.remove("A");
list.clear();
```
- `remove(int index)`: 인덱스로 삭제 
- `remove(Object o)`: 값으로 삭제 
- `clear()`: 전체 삭제 

### 기타 알아두면 좋은 메서드 
```java
list.toArray();
list.subList(0, 2);
list.ensureCapacity(50);
list.trimToSize();
```
- `toArray()`: 배열로 변환
- `subList(from, to)`: 부분 구간 view 반환 
- `ensureCapacity(int minCapacity)`: 최소 용량 확보 
- `trimToSize()`: 현재 크기에 맞춰 capacity 축소 

모든 메서드를 한 번에 외우기보다, 먼저 `add`, `get`, `set`, `remove`, `size`, `contains` 정도 익힌 후 나머지는 필요할 때 확장하는 방식이 효율적일 것 같다는 생각이 든다.

---

## 7. ArrayList의 내부 동작 방식 

ArrayList에 대한 핵심 내용이라고 생각한다.<br/>
겉으로는 리스트처럼 보이지만, 내부 구현은 **동적으로 크기가 조절되는 배열**이다.

즉 ArrayList는 요소를 연속된 메모리 형태로 저장하고, 이 덕분에 인덱스를 통한 접근이 빠르다.<br/>
`get(index)`가 보통 O(1)로 이해되는 이유도 여기에 있다.

하지만 배열이 꽉 차면 문제가 생긴다.<br/>
기존 배열에는 더 이상 공간이 없으므로 더 큰 배열을 새로 반들고 기존 값을 복사해야 한다. 

원글에서는 기본 생성 시  기본 capacity가 10이고, 용량이 부족해지면 새 capacity를 `기존 용량 + 기존 용량 / 2` 방식으로 계산한다고 한다.<br/>
즉 약 1.5배씩 커지는 방식이다.

또한 특정 위치에 삽입하거나 삭제할 때는 뒤쪽 요소들을 이동시켜야 한다.<br/>
예를 들어 1번 인덱스에 새 값을 넣으면, 기존 1번 이후 요소들은 전부 한 칸씩 뒤로 밀리게 된다.<br/>
삭제도 반대로 한 칸씩 앞으로 당겨야 한다. 그래서 ArrayList는 조회에는 강하지만, 중간 삽입/삭제에는 상대적으로 약하다.

정리하면 ArrayList는 "리스트처럼 쓰지만, 내부적으로는 배열의 성질을 그대로 가진 구조"이다.

---

## 8. size와 capacity의 차이 

ArrayList를 공부하다 보면 size와 capacity를 헷갈리기 쉽다.<br/>
size는 현재 실제로 저장된 요소 개수이고, capacity는 내부 배열이 저장할 수 있도록 확보된 공간 크기다.

예를 들어 이렇게 만들었다고 하자.
```java
ArrayList<Integer> list = new ArrayList<>(10);
list.add(1);
list.add(2);
list.add(3);
```

이 경우 실제 들어 있는 값은 3개이므로 size는 3이 되는 것이다.<br/>
하지만 내부적으로는 10칸 정도를 확보해둔 상태이므로 capacity는 10이 된다.

즉, size와 capacity는 전혀 다른 개념으로 봐야 한다.<br/>
size는 "지금 몇 개 들어 있나",<br/>
capacity는 "몇 개까지 들어갈 준비가 되어 있나"에 가깝다.

이 차이를 이해하면 왜 `ensureCapacity()`나 `trimToSize()` 같은 메서드가 존재하는지도 자연스럽게 보이기 시작한다.

---

## 9. 시간복잡도로 이해하는 ArrayList 

자료구조를 공부할 때는 사용법만 아는 것보다, 어떤 연산이 빠르고 느린지를 같이 이해하는 것에 중요하다고 생각한다.

### 1. 조회 - 빠름<br/>
인덱스로 바로 접근할 수 있으므로 `get(index)`는 보통 O(1)로 본다.<br/>
배열 기반 구조의 장점을 그대로 가져가는 부분이다.

### 2. 맨 뒤 삽입 - 보통 빠름<br/>
마지막에 붙이는 `add(E e)`는 대부분 O(1)처럼 동작한다.<br/>
다만 배열이 꽉 찬 시점에는 더 큰 배열을 만들고 복사하는 비용이 들어가므로 원글에서는 **amortized O(1)** 이라고 이해하는 것이 맞다고 한다.

### 3. 중간 삽입/삭제 - 느릴 수 있음<br/>
특정 위치에 넣거나 빼면 뒤 요소를 이동시켜야 하므로 O(N)이 된다.<br/>
즉 요소 이동 비용 때문에 데이터가 많아질수록 부담이 커지게 되는 것이다.

### 4. 순회 - O(N)<br/>
전체를 한 번 도는 것은 당연히 요소 수에 비례하므로 O(N)이 된다.

정리하자면 ArrayList는 **조회가 많고, 끝에 붙이는 추가가 많은 경우에 잘 맞는 구조**라고 보면 될 것 같다.

---

## 정리 

ArrayList는 자바에서 가장 자주 사용하는 컬렉션 중 하나다.<br/>
배열처럼 인덱스로 접근할 수 있어서 익숙하고, 크기가 자동으로 조절되기 때문에 훨씬 유연하게 데이터를 다룰 수 있다.<br/>
동시에 내부는 배열 기반이기 때문에 조회는 빠르지만, 중간 삽입과 삭제에서는 요소 이동 비용이 발생한다는 특징도 함께 가진다.

이번에 정리하면서 느낀 점은 ArrayList를 단순히 "배열보다 편한 것"으로 보는 데서 끝나면 안 된다는 것이다.<br/>
왜 `get()`은 빠르고, 중간 `add()`나 `remove()`는 느릴 수 있는지까지 이해해야 시야가 넓어지는 것 같다.

즉 ArrayList는 "편리한 리스트"이면서 동시에 "배열의 성질을 가진 동적 자료구조"라고 이해하면 정리되는 것 같다.

---

## 참고 

- [GeeksforGeeks, *ArrayList in Java*](https://www.geeksforgeeks.org/java/arraylist-in-java/)

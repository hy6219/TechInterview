
# JVM(Java Virtual Machine)

## 1. 자바 가상 머신이란?

- 자바 프로그램 실행을 위한 물리적 머신과 유사한 머신을 소프트웨어로 구현한 것

- `역할` : 

1) 자바 어플리케이션을 클래스 로더로 읽어들여서 자바 API와 함께 실행

2) 자바와 운영체제 사이에서 `중개자 역할` 수행 →  운영체제에 구애받지 않고 코드의 재사용이 가능

3) 메모리 관리

4) 가비지 컬렉션

- `특징` : 스택 기반의 가상 머신

▶ 클래스 로더 

- 자바 클래스를 JVM으로 동적 로드하는 자바 런타임 환경의 일부

## 2. JVM을 알아야 하는 이유
- 한정된 메모리를 효율적으로 사용해서 최고의 성능을 내기 위해서

## 3. 자바 프로그램 실행 과정

1. JVM이 운영체제로부터 `프로그램이 필요로 하는 메모리를 할당` 받음
2. `자바 컴파일러(javac)`가  자바 소스 코드(.java)를 읽어서 `바이트 코드(.class)` 로 변환시킴
3. `클래스 로더`를 통해 `바이트코드(.class) → JVM으로 로딩`(바이트 코드 로딩)
4. 로딩된 바이트코드는 `실행 엔진(Execution Engine)`을 통해 해석됨(바이트 코드 해석)
5. 해석된 바이트코드는 Runtime Data Areas(런타임 데이터 영역)에 배치되어 실질적인 수행이 이루어짐
6. 이러한 실행 과정 속에서 JVM은 필요에 따라 `쓰레드 동기화`와 `가비지 컬렉션`과 같은 관리 작업을 수행

✅ 쓰레드 동기화

- 여러 개의 쓰레드가 하나의 자원을 공통으로 사용하고자 할 때, `해당 쓰레드만 제외`하고 나머지는 접근하지 못하도록 막는 것
- 멀티 쓰레드 프로세스의 경우, 자원 공유로 인해서 서로의 작업물에 영향을 줄 수 있어서 원하는 결과물과 다른 형태를 보이게 될 수 있음

😊 `synchronized 를 이용한 동기화` 😊

- 데이터를 보호할 수 있음

- lock : 특정 쓰레드에만 하나의 자원에 접근하도록 하고, 그 외에는 접근할 수 없도록 하는 것

(1) 특정 block에서 특정 객체에 lock을 걸고자 할 때
```java
public class MyClass{
 public void useToilet(String name){
      open();
	 //synchronzied(객체의 참조변수)
	 synchronized(this){
	  System.out.println("특정 block에 lock");
	 }
	 close();
 }
}
```
- synchronized 블록을 수행하는 동안에는 지정된 객체에 lock이 걸려서 다른 쓰레드에서 접근할 수 없음

(2) 메서드에 lock을 걸고자 할 때
```java
public class MyClass{
	public synchronized void useToilet(String name){
		System.out.println("메서드이 lock");
	}
}
```

- 메서드가 종료될 때까지 다른 쓰레드가 이 메서드를 호출하여 수행할 수 없게 됨

✅  가비지 컬렉션

- 불필요한 메모리를 알아서 정리해주는 개념으로 , 불필요한 데이터는 null로 표시해준다
- `System.gc()로 호출가능하나, 시스템 성능 문제가 발생할 수 있다고 한다` → 지양하도록 한다


## 4. JVM 구성

![JVM 구성](https://thenaeul.files.wordpress.com/2020/12/image-15.png?w=836)

JVM 구성= `클래스 로더`+`실행엔진(Execution Engine)`+`인터프리터`+`JIT(Just-In-Time)`+`Garbage Collector`

1. 클래스 로더
- 클래스를 `처음 참조할 때 로드하고 링크`하고, `사용하지 않는 클래스들은 메모리에서 삭제`하는 역할을 수행

2. 실행 엔진

- 클래스 로더가 런타임 데이터 영역에 배치한 바이트 코드를 JVM 내부에서 기계가 실행할 수 있는 형태로 변경

3. 인터프리터
- 코드를 한 줄씩 수행하기 때문에 느리다는 특징을 가짐(예: 자바스크립트)
- [VS 컴파일러 : 전체 코드를 읽은 후 실행]

4. JIT
- 인터프리터의 단점을 보완하기 위한 컴파일러로, 인터프리터 방식으로 진행되다가 특정 시점에서 바이트 코드 전체를 컴파일(기계가 이해할 수 있는 언어로 변경하는 과정)하여 네이티브 코드로 변경
- 네이티브 코드 : 메모리가 관리되지 않는 코드

5. Garbage Collector
- 불필요한 객체를 제거하는 가비지 컬렉션을 수행하는 특정 쓰레드가 존재

## 5. Runtime Data Area

![Runtime Data Area](https://t1.daumcdn.net/cfile/tistory/992EE9465D08E9B903)

### 5-1. Runtime Data Area?
- 프로그램 수행을 위해 운영체제에서 할당받은 메모리 공간

### 5-2. 구성
Runtime Data Area= `쓰레드` + `힙` + `메서드 영역`

1. 쓰레드
- 쓰레드 : 프로세스 내에서 `실제로 작업을 수행하는 주체`
- 프로세스 : 실행중인 프로그램

✔ 쓰레드=`PC 레지스터`+`JVM 스택`+`Native 메서드 스택`

ㄱ. PC 레지스터

- 쓰레드가 시작될 때 생성될 때마다 생성되는 공간
- 쓰레드마다 1개씩 존재
- `현재 실행 중인 JVM 명령의 주소`를 갖고 있음

ㄴ. JVM 스택 영역

- 프로그램 실행 과정에서 특정 메서드를 빠져나가면 소멸되는 특성의 데이터가 저장되는 공간
- 변수, 임시 데이터, 쓰레드나 메서드의 정보 등이 저장됨

ㄷ. Native 메서드 스택

👍`Java Native Interface : 기계어가 바이트 코드로 저장되는 공간`

- 자바 코드가 컴파일되어 기계어로 작성된 프로그램을 실행시키는 공간

2. 힙 영역

![Heap](https://www.javainuse.com/java13_1.jpg)

🧡`객체를 저장하는 가상 메모리 공간`

`✨물리적인 힙 영역 구분``✨
![가비지 컬렉션](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFOLU3%2FbtqUOBF35cJ%2FBMKuD1iqfq6R0lAqMlfkC0%2Fimg.png)

- 초기에는 Perm 영역(메타 데이터가 저장되는 공간)이 존재했지만 jdk 8 이후부터는 제거되었다고 한다


1. Young 영역(Young Generation)
- 새롭게 생성된 객체가 할당되는 영역
- 대부분의 객체는 금방 접근 불가능해지기 때문에 , 객체가 Young 영역에 생성되었다가 사라짐
- Young 영역에 대한 가비지 컬렉션이 `Minor GC`
- Eden 영역 : 객체들이 최초로 생성되는 공간
- Survivor 0/1 : Eden 에서 참조되는 객체들이 저장되는 공간

2. Old 영역(Old Generation)
- Young 영역에서 접근 가능한 상태를 유지하여 살아남은 객체가 대부분 Young 영역에서보다 큰 크기로 할당되어 복사되는 영역(그만큼 가비지는 적게 발생)
◀ 
ㄱ. Eden 영역에 객체가 가득찰 경우, 첫 번째 Minor GC 발생
ㄴ. Eden 영역의 값들이 Survivor 1 영역에 복사됨
ㄷ. Survivor 1 영역 외의 영역에 있는 객체들이 삭제됨


- Old 영역에 대한 가비지 컬렉션이 `Full GC`
- 512 바이트의 카드바이트를 이용해서 Old 영역에서 Young 영역의 객체를 참조할 때마다 그에 대한 정보가 표시되어 효율적으로 객체를 식별할 수 있다(`Old 영역에서 Young 영역의 객체를 참조할 수 있는가?`)

3. Method area "클래스 정보를 위한 공간"
`=Class area=Static area`
- `클래스 정보가 처음 메모리 공간에 올릴 때 <strong>초기화되는 대상을 저장하기 위한 메모리 공간</strong>` → 대부분 바이트 코드가 올라가게 됨
- Runtime Constant Pool이라는 별도 영역 존재[상수 자료형을 저장하여 참조하고, 중복을 방지]
- 메서드 영역에서 다루어지는 정보 종류
ㄱ. 필드 정보 : `멤버 변수`에 대한 변수/타입/접근 제어자 정보
ㄴ. 메서드 정보 : 메서드의 이름/반환타입/접근 제어자 정보
ㄷ. 타입 정보 : class/ interface 여부 등

`✨` Heap && Method area → gc 관리 대상!✨

## 참고 문헌
https://asfirstalways.tistory.com/158

https://devbox.tistory.com/entry/Java-%EC%93%B0%EB%A0%88%EB%93%9C%EC%9D%98-%EB%8F%99%EA%B8%B0%ED%99%94






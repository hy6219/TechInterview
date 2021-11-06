# final

1. final 은 어떤 예약어인가?
- final 예약어가 붙은 경우는 상수라고 생각할 수 있다. 클래스에 붙으면 클래스가, 변수에 붙으면 그 변수가, 그 메서드에 메서드가 변경할 수 없는 상태가 된다. 그 이유는 final 예약어가 붙음으로써 값을 변경할 수 없게 되기 때문이다. 추가로, 스프링에서 final 인스턴스명으로 되어 있는 경우에는 RequiredArgsConstructors 어노테이션을 붙여주어야 한다.

2. final과 혼동할 수 있는 개념

A. finally

- 예외 처리 블록에서 try-catch블록 외에 finally 블록을 덧붙여서 try-catch-finally 형태로 예외처리를 진행할 수 있다. 이때, finally 블록에서는 예외처리 유무와 관계없이 무조건 실행될 수 있도록 지원된다.

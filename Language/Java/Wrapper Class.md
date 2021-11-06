﻿
# Wrapper Class

1. 래퍼클래스란 무엇인지 설명해보세요
- 래퍼클래스는 기본자료형인 integer, float 등을 객체처럼 사용할 필요가 있을 경우를 지원하고자 존재하는 클래스라고 할 수 있다. 래퍼 클래스는 jpa와 연결해서 연관관계를 지정해줄 때 null 값이 설정될 수 있는 경우에 적용하기에 적합하다. 기존 기본자료형은 기본값이 0이지만, 래퍼클래스에서는 null을 사용할 수 있기 때문에 의미상 사용할 수 있다. 더불어, 래퍼클래스를 사용하면 정렬기준을 compareTo를 사용해서 손쉽게 적용할 수도 있다

2. AutoBoxing과 AutoUnboxing에 대해서 설명해보세요
-  오토박싱은 `기본자료형을 래퍼클래스로 자동변환`해주는 것을 의미하고, 오토언박싱은 `래퍼클래스를 기본자료형으로 자동변환`해주는 것을 의미한다.
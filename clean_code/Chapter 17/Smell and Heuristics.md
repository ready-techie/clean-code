# Smell and Heuristics

w. Nicky 읽은만큼만^^;

## Comments

### C1: Inappropriate Information

- 주석이 다른 시스템(소스코드 관리, 이슈 트래킹 등)보다 나은 정보를 가지는 것은 부적절하다.
- 작성자, 최종수정일 등의 메타 데이터도 ❌
- 코드, 디자인 등의 기술적인 내용이어야 한다.

### C2: Obsolete Comment

- 낡고, 연관성이 없는 내용도 불필요하다. 주석은 빠르게 outdated되므로 그럴 가능성이 있는 주석은 안쓰는게 좋다. obsolete된 주석을 발견하면 없애라.

### C3: Redundant Comment

- 스스로를 설명하는 주석은 재귀적이다.
  - ex. `i++; // increment i`
- Javadoc에서 단순히 함수의 파라미터, 리턴값만 설명하는 주석도 마찬가지다.
- 주석은 코드가 말할 수 없는 것을 말해야 한다.

### C4: Poorly Written Comment

- 주석을 쓰려면 충분한 시간을 들여서 쓸 수 있는 최고의 주석을 써라. (문법, 단어선택 등에 신경쓸 것)
- 당연한건 쓰지 말고 간단하게 써라.

### C5: Commented-Out Code

- 주석 처리된 코드는 그 자리에서 썩을 뿐!! 발견하면 바로 지워라. 어차피 형상 관리 툴이 기억해준다.

## Environment

### E1: Build Requires More Than One Step

- 하나의 command로 빌드해라

### E2: Tests Require More Than One Step

- 하나의 command로 모든 unit test를 돌려라, 빠르고 간단하게.

## Functions

### F1: Too Many Arguments

- 함수의 인자 수는 적어야 한다. 0개가 best이고, 4개부터는 피해야 한다.

### F2: Output Arguments

- Output argument라는건 이상하다. (사용자는 argument가 input이길 기대한다)
- 함수에서 뭔가의 상태를 변경해야 한다면 출력 인수를 쓰지 말고 함수가 속한 객체의 상태를 변경

### F3: Flag Arguments

- Boolean 인자를 쓴다는건 함수가 하나 이상의 동작을 한다는걸 광고하는 일이다! 복잡하고, 없어져야 한다.

### F4: Dead Function

- 호출되지 않는 함수는 없애라! 형상 관리 툴이 기억해준다.

## General

### G1: Multiple Languages in One Source File

- 현대에는 한 소스 파일에 다양한 프로그래밍 언어를 넣을 수 있다. 이런 건 잘 봐줘봤자 복잡할 뿐이다.
- 이상적으로는 한 파일에 하나의 언어만 넣는 것이 좋지만, 현실적으로는 최대한 줄이려고 노력해야 한다.

### G2: Obvious Behavior Is Unimplemented

- “The Principle of Least Surprise,” 법칙에 따르면 함수는 다른 프로그래머가 예상할 수 있는 행동을 해야한다.
- 이게 안되면 의심을 갖고 모든 코드를 읽어야 한다.

### G3: Incorrect Behavior at the Boundaries

- 개발자들은 가끔 동작할 거라고 생각하는 함수를 작성하고, 어떤 경우에서도 올바르게 동작할 것임을 검증하는 노력을 하지 않는다.
- 직관을 믿지 말고 모든 경우에 대한 test를 작성해라. `Due dilligence`를 대체할 수 있는 건 없다!

### G4: Overridden Safeties

- warning 꺼두기, 실패하는 test를 나중에 고치기 등, 안전 절차를 건너뛰는 행동을 하지 마라!

### G5: Duplication

- 이 책에서 가장 중요한 룰 중 하나. 심각하게 받아들여라
- DRY principle (Don’t Repeat Yourself), “Once, and only once.” Ron Jeffries 는 '모든 테스트 패스하기' 다음으로 중요한 룰로 여긴다.
- 코드에 중복이 있다는건 추상화의 기회를 놓쳤다는 것을 의미한다. _(🧐뭔소리?)_ 추상화 레벨을 높이면 코딩은 빨라지고 오류는 줄어든다.
- 계속 같은 조건을 확인하는 switch/case, if/else chain 등은 간단하고 작은 함수로 새로 만들어야 한다. (polymorphism)
- 알고리즘은 비슷하지만 같은 코드를 사용하지 않는 모듈도 중복이다.

### G6: Code at Wrong Level of Abstraction

- 높은 레벨의 일반적인 개념을 낮은 레벨의 세부적인 개념으로 추상화시키는 건 중요하다.
- 우리는 낮은 레벨 개념은 상속derivative이길 원하고 높은 레벨 개념은 base class이길 원한다. 이걸 완전하게 분리해라.
  - ex. constants, variables, or utility functions that pertain only to the detailed는 base class가 알면 안된다.

```java
public interface Stack {
  Object pop() throws EmptyException;
  void push(Object o) throws FullException;
  double percentFull();

class EmptyException extends Exception {}
class FullException extends Exception {}
}
```

- 위 예시에서 `percentFull`이 Stack에 있는 것은 이상하다. 얼마나 full했는지 모르는 경우도 있을 수 있다. 따라서 `BoundedStack`같은 상속 인터페이스에 있는 게 낫다. boundless하다고 0을 리턴하면 되는거 아니냐? 할수도 있는데 진짜 boundless한 stack은 세상에 없다.

### G7: Base Classes Depending on Their Derivatives

- base와 derivative 클래스를 나누는 보편적인 기준은 고차원의 base클래스가 저차원의 클래스와 독립적이어야 한다는 것이다.
- base는 derivative들을 몰라야 하며, 따라서 derivative의 이름을 갖고 있어서는 안된다.
  - base와 derivative가 강하게 결합된 경우 등, 예외가 있을 수는 있다.
- 이렇게 jar파일까지 독립적이어야 문제가 있을때 derivative만 따로 배포하는 등, 변화의 impact를 줄여서 시스템을 심플하게 만들 수 있다.

### G8: Too Much Information

- 잘 정의된 모듈은 아주 작은 인터페이스로 많은 것을 할 수 있게 해서 coupling을 낮춘다.

### G9: Dead Code

- 실행되지 않는 코드를 말한다.
  - ex. 발생하지 않는 조건을 체크하는 if
- 디자인이 변경될 때 업데이트되지 않기 때문에 심한 코드 스멜을 유발한다. 발견하면 삭제해라.

### G10: Vertical Separation

- 변수, 함수는 사용하는 곳 가까이에 위치해야 한다.
- Private 함수는 클래스 내에 어디에서나 사용할 수 있다고 해도 처음 사용되는 곳 바로 아래에 위치해야 한다.

### G11: Inconsistency

- convention을 정하고, 따라가라. (principle of least surprise)
  - ex. response를 반환하는 변수 이름을 Response로 정했다면, 다른 곳에서도 똑같이 써라. processVerificationRequest라는 함수가 있다면 이름을 비슷하게 processDeletionRequest라고 써라.

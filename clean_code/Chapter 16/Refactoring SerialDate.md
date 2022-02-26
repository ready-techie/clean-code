# Chap16. First, Make It Work

We're gonna explore http://www.jfree.org/jcommon/index.php > JCommon library > org.jfree.date (package) > `SerialDate` (class).

- `SerialDate` 클래스는 아주 잘 작성된 코드이므로 찢어본다.
- 이건 professional한 리뷰이므로 편안해야 하고, 배우는 과정!
- `SerialDate`는 Java에서 date를 표현하는 클래스다. 자바에는 이미 java.util.Date,
  java.util.Calendar 등 date를 나타내는 라이브러리가 있는데 이게 왜 필요할까? 그건 `SerialDate`의 저자가 작성한 Javadoc을 참고하기 바란다.
  - 🧐 기존 라이브러리가 실제로는 date가 아닌 time에 대한 클래스여서 그런가보다.

## First, Make It Work

- `SerialDateTests`라는 클래스에 unit test 들이 있다. 테스트는 모두 패스하지만 모든 것을 테스트하진 않는다. 그래서 `Clover`를 사용해서 unit test가 무엇을 cover하는지 확인했고, 약 50%를 테스트하고 있음을 알 수 있다.

- 클래스를 완전하게 이해하고 리팩토링하기 위해 저자가 생각하는 결과를 뱉는 테스트를 작성했고 이것들을 통과시키는 게 목표. 결과적으로는 약 92%를 execute하게 되었다.

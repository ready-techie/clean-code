# 5. Formatting

- You should take care that your code is nicely formatted. You should choose a set of
  simple rules that govern the format of your code, and then you should consistently apply
  those rules.

## The Purpose of Formatting

- `communication`: communication is the professional developer’s first order of business.
- Your style and discipline survives, even though your code does not
  - Original code는 계속 변할 수 있지만 코딩 스타일, 가독성은 남아 유지보수를 원활하게 하고 확장성을 향상시킨다.

## Vertical Formatting

- `Junit`, `FitNesse` 등의 JAVA 라이브러리를 보면 500라인을 넘어가는 파일이 거의 없고, 대부분 200라인 미만이다.
  - 아주 복잡한 시스템도 파일 당 200~500라인으로 만들 수 있다.
- Small files are usually easier to understand than large files are.

### The Newspaper Metaphor

- 잘 작성된 신문에서: Headline -> First paragraph(synopsis) -> Details -> ... 로 구성된 작은 article들이 있다.
  - 코드도 이렇게 작성해야 한다.
- The name should be simple but explanatory.
  - 이름만으로 올바른 module에 속해있는지 알 수 있어야 한다. (_🧐빡쎄다.._)
- 소스의 상위에서부터: High-level concept -> Details

### Vertical Openness Between Concepts

- Each line represents an expression or a clause, and each group of lines represents a complete thought. Those thoughts should be separated from each other with blank lines.
- Blank line이라는 간단한 규칙 has a profound effect on the visual layout of the code.

  - 새로운, 나뉘어진 concept를 시각적으로 잘 나타낸다

### Vertical Density

- Openness가 concept를 분리한다면, Density는 `close association`을 의미한다
  - tightly related code는 수직 밀도가 높아야 한다

### Vertical Distance

- Concepts that are closely related should be kept vertically close to each other.
  - 보통 같은 파일에 있으며, 다른 파일에 있으려면 합당한 이유가 필요하다
  - 이것이 `Protected variables`를 피해야 하는 이유다
- **Variable Declarations**: Variables should be declared as close to their usage as possible.
- **Instance variables**: should be declared at the top of the class. This
  should not increase the vertical distance of these variables.
  - 어디 위치하느냐는 아직 논쟁이다. (C++ -> scissors rule, Java -> top)
- **Dependent Functions**: If one function calls another, they should be vertically close,
  and the caller should be above the callee, if at all possible.
  - natural flow
- **Conceptual Affinity**: Stronger conceptual affinity, Less vertical distance
  - ex. one function calling another
  - Affinity might be caused because a group of functions perform a similar operation.
    - ex. share a common naming scheme and perform variations of the same basic task

```java
public class Assert {
	static public void assertTrue(String message, boolean condition) {
		if (!condition)
			fail(message);
	}
	static public void assertTrue(boolean condition) {
		assertTrue(null, condition);
	}
	static public void assertFalse(String message, boolean condition) {
		assertTrue(message, !condition);
	}
	static public void assertFalse(boolean condition) {
		assertFalse(null, condition);
	}
}
```

### Vertical Ordering

- we want function call dependencies to point in the downward direction
  - a function that is called should be below a function that does the calling (code flow: high level -> low level)

## Horizontal Formatting

- 예제 프로젝트들을 보면 약 40%의 code line들은 20~60 width를 가진다 (_🧐맞나?_)
  - This suggests that we should strive to keep our lines short
  - 저자는 오른쪽으로 scroll할 필요가 없게 한다는 rule을 따름 (요즘은 화면크기가 커서 120자로 생각함. 200자는 넘지 말라!)

### Horizontal Openness and Density

- surround the assignment operators with white space to accentuate them `totalChars += lineSize;`
- didn’t put spaces between the function names and the opening parenthesis. This is because the function and its arguments are closely related. `measureLine(String line)`

### Horizontal Alignment

- not useful
- prefer unaligned declarations and assignments, as shown below, because they point out an important deficiency. (_🧐뭔뜻?_)

### Indentation

- visually line up lines on the left to see what scope they appear in.
  - This allows them to quickly hop over scopes, such as implementations of if or while statements, that are not relevant to their current situation.
- **Breaking Indentation**: 짧은 `if` / `while`문은 indentation없이 한 줄에 작성해버리는 경우가 있지만, 저자는 항상 indentation을 지킨다

### Dummy Scopes

- 아래와 같이 `while` / `for`의 body가 빈 경우가 있다. 가능한 없애지만, 없앨 수 없는 경우에는 braces로 감싸고 적절한 indentation을 준다.

```java
while (dis.read(buf, 0, readBufferSize) != -1)
  ;
```

## Team Rules

- A team of developers should agree upon a single formatting style, and then every member of that team should use that style.

## Uncle Bob's Formatting Rules

- 저자가 선호하는 스타일 소개

# Use Intention-Revealing Names

- Choosing good names takes time but saves more than it takes.
- The name should tell you why it exists, what it does, and how it is used. If a name requires a com-
  ment, then the name does not reveal its intent.

```java
//👎
int d; // elapsed time in days
//👍
int elapsedTimeInDays;
```

# Avoid Disinformation

- Even if you are coding a hypotenuse and `hp` looks like a good abbrevia-
  tion, it could be disinformative.
- Beware of using names which vary in small ways. (ex. `XYZControllerForEfficientHandlingOfStrings` vs `XYZControllerForEfficientStorageOfStrings`)
- A truly awful example of disinformative names would be the use of lower-case L or
  uppercase O as variable names, especially in combination.

# Make Meaningful Distinctions

- If names must be different, then they should also mean something different.
- Noise words are another meaningless distinction.
  - `Product` 클래스가 있다면, `ProductInfo` / `ProductData`같은 이름은 의미 없이 다르게 만드는 것. Info and Data are indistinct noise words like a, an, and the.

# Use Pronounceable Names

- If you can’t pronounce it, you can’t discuss it without sounding like an idiot. This
  matters because programming is a social activity.

# Use Searchable Names

- Writer's personal preference is that single-letter names can ONLY be used as local vari-
  ables inside short methods. The length of a name should correspond to the size of its scope

# Avoid Encodings

- Encoded names are seldom pronounceable and are easy to mis-type.

## Hungarian Notation

- Useless now because In modern languages we have much richer type systems, and the compilers remember and enforce the types.

## Member Prefixes

- You also don’t need to prefix member variables with m\_ anymore.

## Interfaces and Implementations

- I prefer to leave interfaces unadorned. The preceding I, so common in
  today’s legacy wads, is a distraction at best and too much information at worst. I don’t
  want my users knowing that I’m handing them an interface. I just want them to know that
  it’s a ShapeFactory.

# Avoid Mental Mapping

- Certainly a loop counter may be named i or j or k (though never l!) if its scope is very small and no other names can con-
  flict with it. This is because those single-letter names for loop counters are traditional. However, in most other contexts a single-letter name is a poor choice;
- One difference between a smart programmer and a professional programmer is that
  the professional understands that clarity is king. Professionals use their powers for good
  and write code that others can understand.

# Class Names

- Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`,
  `Account`. Avoid words like `Manager`, `Processor`, `Data`, or `Info` in the name
  of a class. A class name should not be a verb.

# Method Names

- Methods should have verb or verb phrase names like `postPayment`, `deletePage`, or `save`.

# Don’t Be Cute

- If names are too clever, they will be
  memorable only to people who share the
  author’s sense of humor, and only as long
  as these people remember the joke.
- For example,
  don’t use the name `whack()` to mean `kill()`. Don’t tell little culture-dependent jokes like
  `eatMyShorts()` to mean `abort()`.

# Pick One Word per Concept

- The function names have to stand alone, and they have to be consistent in order for you to pick the correct method without any additional exploration.
- Consistency 일관성

# Don’t Pun

- Avoid using the same word for two purposes. Using the same term for two different ideas
  is essentially a pun.
- ex. `add`가 두 숫자를 더하는 경우/리스트에 항목을 추가하는 경우 두가지로 사용되어서는 안된다

# Use Solution Domain Names

- It
  is not wise to draw every name from the problem domain because we don’t want our
  coworkers to have to run back and forth to the customer asking what every name means
  when they already know the concept by a different name.

# Use Problem Domain Names

- Separating solution and problem domain concepts is part of the job of a good pro grammer and designer. The code that has more to do with problem domain concepts should have names drawn from the problem domain.

# Add Meaningful Context

- Imagine that you have variables named firstName, lastName, street, houseNumber, city,
  state, and zipcode. Taken together it’s pretty clear that they form an address. But what if
  you just saw the state variable being used alone in a method?

# Don’t Add Gratuitous Context

- Shorter names are generally better than longer ones, so long as they are clear. Add no
  more context to a name than is necessary.
- The names accountAddress and customerAddress are fine names for instances of the
  class Address but could be poor names for classes. Address is a fine name for a class.

# Final Words

- The hardest thing about choosing good names is that it requires good descriptive skills and
  a shared cultural background.

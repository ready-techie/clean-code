# **Classes**

## **Class Organization**

- standard Java convention: a class should begin with a list of variables. Public static constants, private static variables, followed by private instance variables. There is seldom a good reason to have a public variable.
- follows `stepdown rule`: Public functions should follow the list of variables. Private utilities called by a public function right after the public function itself

### Encapsulation

- Look for a way to maintain privacy
    - Sometimes we need to make a variable or utility function protected so that it can be
    accessed by a test. (we make protected or package scope)
    - Loosening encapsulation is always a last resort

## Classes Should Be Small!

- The first rule of classes is that they should be small. The second rule of classes is that they
should be smaller than that.
- With classes we use a different measure compared to Function. We count **responsibilities**.
    - ex. SuperDashboard라는 class가 70 public method를 가진다면? 5 public method를 가진다면?
- The name of a class should describe what responsibilities it fulfills. In fact, naming
is probably the first way of helping determine class size. If we cannot derive a concise
name for a class, then it’s likely too large. The more ambiguous the class name, the more
likely it has too many responsibilities.
    - For example, class names including weasel words like Processor or Manager or Super often hint at unfortunate aggregation of responsibilities.
- We should also be able to write a brief description of the class in about 25 words,
without using the words “if,” “and,” “or,” or “but.”
    - ex. SuperDashboard: “The SuperDashboard provides access to the component that last held the focus, and it also allows us to track the version and build numbers.”
- The first “and” is a hint that SuperDashboard has too many responsibilities.

### The Single Responsibility Principle

- Classes should have one responsibility—one reason to change
  - Trying to identify responsibilities (reasons to change) often helps us recognize and create better abstractions in our code
  - ex. extract all three SuperDashboard methods that deal with version information into a separate class named Version. The Version class is a construct that has a high potential for reuse in other applications!

- SRP is one of the more important, simpler concept in OO design. 
- Yet oddly, SRP is often the most abused class design principle. We regularly encounter classes that do far too many things. Why?
  - Getting software to work and making software clean are two very different activities.
  - we focus on getting our code to work more
than organization and cleanliness.
  - The problem is that too many of us think that we are done once the program works.
  - Do you want your tools organized into toolboxes with many small drawers each containing well-defined and well-labeled components? Or do you want a few drawers that you just toss everything into?
  - 작은 여러가지중에서는 필요한 것만 바로 찾을 수 있지만 크고 목적이 여러가지인 시스템에서는 지금 알 필요 없는것들을 알게 한다
- To restate the former points for emphasis: We want our systems to be composed of many small classes, not a few large ones. Each small class encapsulates a single responsibility, has a single reason to change, and collaborates with a few others to achieve the desired system behaviors.

### Cohesion

- Classes should have a small number of instance variables 
- In general the more variables a method manipulates the more cohesive that method is to its class. 
  - A class in which each variable is used by each method is maximally cohesive.
- High cohesion means that the methods and variables of the class are co-dependent and hang together as a logical whole.
- The strategy of keeping functions small and keeping parameter lists short can sometimes lead to a proliferation of instance variables that are used by a subset of methods.
  - When this happens, it almost always means that there is at least one other class trying to get out of the larger class. You should try to separate the variables and methods into two or more classes such that the new classes are more cohesive.

### Maintaining Cohesion Results in Many Small Classes
- Just the act of breaking large functions into smaller functions causes a proliferation of classes. 
  - ex. 함수를 쪼개는데 일부분이 인자로 받는 모든 4가지 변수를 사용한다면 그것들을 또 전달해줘야할까? 만약 그 4가지 변수를 인스턴스로 둔다면 인자를 전달하지 않을 수 있고, 쪼개기가 쉬워질 것이다.
  - Unfortunately, this also means that our classes lose cohesion because they accumulate more and more instance variables that exist solely to allow a few functions to share them.
  - When classes lose cohesion, split them!
- breaking a large function into many smaller functions often gives us the opportunity to split several smaller classes out as well. This gives our program a much better organization and a more transparent structure.

- Ex. The first thing you might notice is that the program got a lot longer. 
  - First, the refactored program uses longer, more descriptive variable names.
  - Second, the refactored program uses function and class declarations as a way to add commentary to the code. 
  - Third, we used whitespace and formatting techniques to keep the program readable.


## Organizing for Change
- For most systems, change is continual. 
- Every change subjects us to the risk that the
remainder of the system no longer works as intended. In a clean system we organize our classes so as to reduce the risk of change.

### Isolating from Change
- Needs will change, therefore code will change. 
- We can introduce interfaces and abstract classes to help isolate the impact of those details(code) and and abstract classes, which represent concepts only. 
- In essence, the Dependency Inversion Principle (DIP) says that our classes should depend upon abstractions, not on concrete details.

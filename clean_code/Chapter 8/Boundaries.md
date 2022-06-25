# Boundaries
Somehow we must cleanly integrate foreign codes like third-party libraries. 
## Using Third-Party Code
- Providers of third-party packages and frameworks strive for broad applicability so they
can work in many environments and appeal to a wide audience. 
- Users, on the other hand, want an interface that is focused on their particular needs. This tension can cause problems at the boundaries of our systems.
## Exploring and Learning Boundaries
- Third-party code helps us get more functionality delivered in less time  
- Write some tests to explore our understanding of the third-party code. 
    - Jim Newkirk calls such tests `learning tests`
    - we call the third-party API, as we expect to use it in our application
    - The tests focus on what we want out of the API
## Learning log4j
- Reading Documentation + Implementation + Google
## Learning Tests Are Better Than Free
- The learning tests were
precise experiments that helped increase our understanding.
- When there
are new releases of the third-party package, we run the learning tests to see whether there
are behavioral differences
- a clean boundary
should be supported by a set of outbound tests that exercise the interface the same way the
production code does.
## Using Code That Does Not Yet Exist
- API가 디자인되지 않은 상태에서, we defined our own interface which we wished we had.
    - which is under our control. This helps keep client code more readable and focused on what it is trying to
accomplish.
## Clean Boundaries
- Good software
designs accommodate change without huge investments and rework
- We
should avoid letting too much of our code know about the third-party particulars. It’s better
to depend on something you control than on something you don’t control, lest it end up
controlling you

Current - 48:12
### What this means for software design
- **Class**: Language feature to *construct object* with certain **roles**. An object can be created from a *single class*
- **Role**: Messages an object with this role can reply to. An object can have *multiple roles*. An object's roles can change during run time.
**Start with roles first:** Employee role, Engineer role, ProductAnalyst role, Persistable role, Movable role, etc.

#### The Messages
Think about the **behaviors** the program must support, in other words, the **messages** of each role:
- do_work -> WorkingRole
- write_code -> EngineeringRole
- design_product -> ProductAnalysisRole
And then, when we want concrete behavior, we supply them via Factory, Class or whatever the mechanism the language supports to construct objects. In pure OOP, class is just a type of factory.

#### Recap
- OOP is not about class and inheritance
- OOP is about message sending
### Software design is about cracking complexity
Writing software is complex...

As your software grows, complexity increases
![[Chart_Lifespan_Software.png]]

Complexity is the root of all evil
- **Readability:** It makes it hard to understand and reason about a program
- **Reliability:** Hard to reason about the program -> hard to debug
- **Reusability:** Hard to turn code into reusable component
- **Scalability:** Hard to separate code that can run in parallel
- **Testability:** Hard to test code with too many dependencies.
- 

### Two types of complexity
- Essential complexity
     - Complexity inherent to the problem which can't be removed e.g. Slack notification
- Accidental complexity
     - Complexity due to the choices made from a particular software design to solve the problem

### 5 aspects of complexity
- Shared mutable state
     - Hard to reason about
     - Implicit time dependency
     - Explosion of state space
     - Hard to parallelize
- Side-effects
     - Async call
     - UI render
     - Network call, etc.
     Main problems: asynchronous and failable
- Dependencies
    -  **Class dependency**: object creation dependency
    - **Interface dependency**: messages dependency
    - Temporal dependency**: mutable state/side-effect dependency
    
    **Golden rule of dependency management**
    <mark style="color: #FF5582A6;">Things that change more should depend on things that change less often</mark>
- Control flow
    Control flow: hard to understand, reason about, more cases to test
    - Branching: if/else, case/when, etc
    - Looping: for/while loop, recursion, etc
    - Error handling: try/catch
- Code size


### Two ways to manage complexity
- Reduce complexity
- Isolate complexity
OOP helps with *isolating* complexity
Objects don't mutate state of each other directly but send messages to each other instead
OOP *isolate* dependencies
Objects only depend on each other's interface, not implementation which generally more often
OOP *isolate* control flow
Objects' internal control flow are isolated from each other. External control flow is just about objects sending messages to each other
Branching can be converted to polymorphism and isolated to object creation phase.
But OOP does not *reduce* complexity

OOP may even increase complexity!
The main problem with OOP is that it does not reduce global complexity, it just packages complexity into isolated, smaller boxes
- Increase global complexity by adding indirection to behavior
     - Raw data is inherently less complex than objects with behavior
- Increase dependencies: Adding dependencies between objects
- Increase control flow: As the control flow now are the messages between objects
- Increase code size

Seeking complexity reduction with functional programming
- Reduce shared mutatble state
- Reduce side effects
- Reduce dependencies
- Reduce control flow
- 

What is functional programming?
Programming with pure, composable functions
- Pure: Data flows from inputs to outputs
     - No mutations
     - No side-effects
- Composable: Functions are first-class, which mean they can be treated as data and transformed like data
- 
![[Example_Mutate_Data.png]]

Problems
- What are the states of the input arguments after running this function?
- If I have two people to make this tiramisu, which parts can be done in parallel?
- The steps are too complex, how do I refactor the steps to subs-functions?
- If we miss a step, how do we debug the wrong mixture state?
- 
What if  we can make tiramisu without mutating data?

The core of Function Programming is thinking about *data-flow* rather than *control-flow*
![[Core Function Programming.png]]

Functional: nested functions
![[Example Nested Functions.png]]

Which parts can be done in parallel?
![[Example Software run parallel.png]]

Which parts can be sequentially?
![[Example software run sequentitially.png]]

Functional: named constants
![[Example Function Named Constants.png]]

Benefits (cont.)
- Each step can be tested in isolation without mocking
- Easier to debug, just put a breakpoint between 2 steps and check the input and output of each function
- The pipeline can be parallelized and refactored easily. Any group of steps will have a clear set of inputs and outputs.

Functional programming helps reduce complexity
- Reduce shared mutable state: pure functions don't muate state
- Reduce side effects: pure functions don't create side effects 
- Reduce dependencies: zero time dependency, explicit dependencies between steps
- Reduce control flow: no loop, no if/else

Combining the best of OOP and FP (Functional Programming)

Type of Language
![[Overview Type of Languages Code]]

Refactoring is about **reducing** or **isolating** complexity
**Object oriented programming** makes code understandable by **encapsulating (isolating)** moving parts (complexity).
**Functional programming** makes code understandable by **minimizing (reducing)** moving parts (complexity)


What if we can get the best of both worlds?
![[Functional Corem Imperative Shell]]
Link references
https://mokacoding.com/blog/functional-core-reactive-shell/
https://www.destroyallsoftware.com/talks/boundaries

All code can be classified into two distinct roles: code that does work (algorithms) and code that coordinates work (coordinators)

Problems
![[Problems.png]]

Traditional OOP
![[OO Design.png]]
Functional core - pure functions for behaviors
![[Pure Function For Behaviors.png]]
OOP shell - objects
![[OO Shell.png]]
Functional programming deals with values, imperative programming deals with objects.

### Refactoring: Reducing/Isolating complexity
Mutations, Side-effects, dependencies, control flow can either be minimized or isolated. We are doing both with this architecture.
- **Reduce** mutations by changing the core to functional. The only parts that still have mutations are in the OO shell -> Mutations are **isolated**
- **Reduce** unnecessary side effects by changing the core to functional. The only parts that still have side effects are the OO shell -> Side effects are **isolated**
- **Reduce** dependencies by moving to functional. **Isolate** dependencies to OO shell
- Number of control flows: **Isolated** inside the functional core

### Benefits
- **Testability**: Trivial and very fast to unit test the core, minimal number of integration tests needed for the coodinators
- **Reliability**: Validation can be easily added to value classes, ensure the system is always in a valid state. Side effects and exceptions are isolated within coodinator classes.
- **Readability**: Functional core has no dependency and self-contained -> very easy to read and understand in isolation

Functional Core - Immutable values
![[Immutable Values.png]]

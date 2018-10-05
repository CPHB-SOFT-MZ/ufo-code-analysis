# Code analysis
I chose to run PMD on the graphql-jpa project. The 10 metrics I chose to run are the following:
1. Coupling/CouplingBetweenObjects

...Low coupling and high cohesion is the general rule for designing software. We want low
coupling to make sure objects are not tied too tightly together. If they are, polymorphism becomes a lot harder, which means classes are coupled so closely together that you can't substitute an
implementation with another one in an easy way. I would choose this one in every possible 
situation, as it's so essential to software development

2. Design/SwitchStmtsShouldHaveDefault

...The switch statement should always have a default to catch any unexpected or unspecified 
values. The reason being, that if you don't do this, you can have some values that will just fall
through the switch. This will usually happen unnoticed and is likely to introduce bugs. I would 
pick this one if the code tends to have a lot of switch statements or if you have critical software where you absolutely need to tend to all cases. 

3. Design/AvoidDeeplyNestedIfStmts

...Deeply nested if statements increases complexity. If you tend to have a lot of deeply nested if statements, you should consider a refactor. The reason being, that it's much more difficult 
to debug and read for other developers. I would always pick to check for this, as this is very
 essential in all software that has some kind of logic. 

4. Design/BadComparison

...Always avoid comparisons with Double.NaN since double precision is in general pretty bad. 
I would pick this if there are a lot of logic or calculations that depends on the precision
 of Doubles.

5. Design/ConfusingTernary

...This is a really common issue often seen with inexperienced developers. The confusing ternary means that: `if (a != b) doOneThing(); else doSomethingElse();` is the same as
 `if (a == b) doSomethingElse(); else doSomething();`. The former is just more confusing and is prone to introducing bugs. I would always check for this if the software development team has a lot
 of inexperienced members.

6. Design/ImmutableField

...The `final` keyword is a clear and simple contract for a field. It improves readability as you know beforehand, that this variable is not going to change later in the code. This can also improve debug speed. I would always perform this check. Most modern IDE's are automatically doing this though. 

7. Design/SimplifyConditional

... This rule just makes sure you don't check for null before you check if an object is an instance of a type since the `instanceof` automatically does this check. This again, improves readabilty
 and reduces the codebase a bit, which means I would always check for this.

8. Design/CompareObjectsWithEquals

...Always compare objects with the .equals() method since you can't overload the == operator. The == operator compares references, while you can make the .equals() method compare fields or something else on an object. Using == is very likely to introduce bugs, and should definitely be avoided. I would always do this check, as it's not just a design thing, but can also affect behaviour of the software in unexpected ways.

9. Design/UnnecessaryLocalBeforeReturn

...Hmmm

10. Design/UncommentedEmptyMethodBody

...Hmmm

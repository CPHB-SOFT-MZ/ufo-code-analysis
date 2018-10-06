# Code analysis
I chose to run PMD on the graphql-jpa project. The 10 metrics I chose to run are the following:
1. Coupling/CouplingBetweenObjects
    - Low coupling and high cohesion is the general rule for designing software. We want low
coupling to make sure objects are not tied too tightly together. If they are, polymorphism becomes a lot harder, which means classes are coupled so closely together that you can't substitute an
implementation with another one in an easy way. I would choose this one in every possible 
situation, as it's so essential to software development.
    - PMD reports nothing on this in the `graphql-jpa` project.

2. Design/SwitchStmtsShouldHaveDefault
    - The switch statement should always have a default to catch any unexpected or unspecified 
values. The reason being, that if you don't do this, you can have some values that will just fall
through the switch. This will usually happen unnoticed and is likely to introduce bugs. I would 
pick this one if the code tends to have a lot of switch statements or if you have critical software where you absolutely need to tend to all cases. 
    - PMD reports nothing on this in the `graphql-jpa` project.

3. Design/AvoidDeeplyNestedIfStmts
    - Deeply nested if statements increases complexity. If you tend to have a lot of deeply nested if statements, you should consider a refactor. The reason being, that it's much more difficult 
to debug and read for other developers. I would always pick to check for this, as this is very
 essential in all software that has some kind of logic. 
    - PMD reported two lines as deeply nested in the `graphql-jpa` project. One on `/src/main/java/org/crygier/graphql/JpaDataFetcher.java:51` and another one on `/src/main/java/org/crygier/graphql/JpaDataFetcher.java:66`. By inspecting the file, I can see that it's 4 levels deep, which is not completely horrible, but not the best either.

4. Design/BadComparison
    - Always avoid comparisons with Double.NaN since double precision is in general pretty bad. 
I would pick this if there are a lot of logic or calculations that depends on the precision
 of Doubles.
    - Again, this reports nothing in the `graphql-jpa` project.

5. Design/ConfusingTernary
    - This is a really common issue often seen with inexperienced developers. The confusing ternary means that: `if (a != b) doOneThing(); else doSomethingElse();` is the same as
 `if (a == b) doSomethingElse(); else doSomething();`. The former is just more confusing and is prone to introducing bugs. I would always check for this if the software development team has a lot
 of inexperienced members.
    - This reports 6 cases. There's really no excuse for doing this. One case is `/src/main/java/org/crygier/graphql/GraphQLSchemaBuilder.java:323`

6. Design/ImmutableField
    - The `final` keyword is a clear and simple contract for a field. It improves readability as you know beforehand, that this variable is not going to change later in the code. This can also improve debug speed. I would always perform this check. Most modern IDE's are automatically doing this though. 
    - PMD reports 3 places where this could be improved. All in `/src/test/groovy/org/crygier/graphql/model/embeddings/EmbeddingId.java`. This is an entity class, and some reflection libraries can have a difficult time with final fields, so this could be why they chose this approach here.

7. Design/SimplifyConditional
    - This rule just makes sure you don't check for null before you check if an object is an instance of a type since the `instanceof` automatically does this check. This again, improves readabilty
 and reduces the codebase a bit, which means I would always check for this.
    - PMD reports nothing here.

8. Design/CompareObjectsWithEquals
    - Always compare objects with the `.equals()` method since you can't overload the `==` operator. The `==` operator compares references, while you can make the `.equals()` method compare fields or something else on an object. Using `==` is very likely to introduce bugs, and should definitely be avoided. I would always do this check, as it's not just a design thing, but can also affect behaviour of the software in unexpected ways. Unless you really want to compare the reference that is.
    - PMD reports nothing here.

9. Design/UnnecessaryLocalBeforeReturn
    - The compiler can usually detect this so it wont fill up any memory. Any way, it's bad 
practice to have it and creates unnecessary clutter, which is why it should be removed. I'd always check for this, especially if you're working with an older compiler (not everyone is up to speed)
    - PMD reports nothing here

10. Design/UncommentedEmptyMethodBody
    - Again, just unnecessary clutter that should not be there. If a body of a method is empty it should definitely have a comment explaining why, to prevent confusion for other developers. I'd always make this check to prevent confusion about the code.
    - Again, PMD reports nothing

In conclusion to this, it seems like the code is OK. Of course, this is just a small sample of metrics run, and it could be that the ones I chose were so basic that the developers had this down at least. 

## Profiling
The profiling tools I've tried to use either didn't work, or the license costs half of a students SU. Netbeans doesn't work on my machine (MacOS High Sierra) so I only had the option to start and stop a timer on each of the tests in the `StarwarsQueryExecutorTest.groovy` test file. I didn't find the bottleneck, as my times were very identical. The only method taking longer than the others, were the first one, taking 0.45467112 seconds. All other methods ranged from between 0.01 to 0.04 seconds. 


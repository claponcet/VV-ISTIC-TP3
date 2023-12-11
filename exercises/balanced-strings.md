# Balanced strings

A string containing grouping symbols `{}[]()` is said to be balanced if every open symbol `{[(` has a matching closed symbol `)]}` and the substrings before, after and between each pair of symbols is also balanced. The empty string is considered as balanced.

For example: `{[][]}({})` is balanced, while `][`, `([)]`, `{`, `{(}{}` are not.

Implement the following method:

```java
public static boolean isBalanced(String str) {
    ...
}
```

`isBalanced` returns `true` if `str` is balanced according to the rules explained above. Otherwise, it returns `false`.

Use the coverage criteria studied in classes as follows:

1. Use input space partitioning to design an initial set of inputs. Explain below the characteristics and partition blocks you identified.
2. Evaluate the statement coverage of the test cases designed in the previous step. If needed, add new test cases to increase the coverage. Describe below what you did in this step.
3. If you have in your code any predicate that uses more than two boolean operators, check if the test cases written so far satisfy *Base Choice Coverage*. If needed, add new test cases. Describe below how you evaluated the logic coverage and the new test cases you added.
4. Use PIT to evaluate the test suite you have so far. Describe below the mutation score and the live mutants. Add new test cases or refactor the existing ones to achieve a high mutation score.

Write below the actions you took on each step and the results you obtained.
Use the project in [tp3-balanced-strings](../code/tp3-balanced-strings) to complete this exercise.

## Answer

1. We partinioned the possible inputs in the following blocks, assuming that the string only contains grouping symbols:

| Charactiristics                                                      | Blocks                               |
|======================================================================|======================================|
|                                                                      | yes               | no               |
|----------------------------------------------------------------------|-------------------|------------------|
| null                                                                 | exception                            |
| empty                                                                | balanced                             |
| equal number of opening and closing grouping symbols of each kind    | yes -> undecided  | no -> unbalanced |
| string starts with closing grouping symbol                           | yes -> unbalanced | no -> undecided  |
| string ends with opening grouping symbol                             | yes -> unbalanced | no -> undecided  |
| string contains a balanced string inside each pair of grouping symbol| yes -> balanced   | no -> unbalanced |
| string is a sequence of balanced strings (0 or more)                 | yes -> balanced   | no -> unbalanced |
| string is "()" or "[]" or "{}"                                       | yes -> balanced   | no -> unbalanced |

We combined the characteristics when they are undecided to obtain inputs covering all cases. Here are our inputs:
```java
static String NULL = null;
static String EMPTY = "";
static String UNEQUAL = "(([{}])";
static String EQUAL_BALANCED = "([{}])"; // covers EQUAL_CONTAINS_BALANCED, EQUAL_STARTS_WITH_OPENING, EQUAL_ENDS_WITH_CLOSING
static String EQUAL_UNBALANCED = "([{}(]))"; // covers EQUAL_CONTAINS_UNBALANCED
static String EQUAL_STARTS_WITH_CLOSING = ")({[]}"; // covers SEQUENCE_STARTS_WITH_CLOSING
static String EQUAL_ENDS_WITH_OPENING = "[]{})("; // covers SEQUENCE_ENDS_WITH_OPENING
static String SEQUENCE_BALANCED = "([{}])({[]})"; // covers SEQUENCE_CONTAINS_BALANCED, SEQUENCE_STARTS_WITH_OPENING, SEQUENCE_ENDS_WITH_CLOSING
static String SEQUENCE_UNBALANCED = "()(][)"; // covers SEQUENCE_CONTAINS_UNBALANCED
```




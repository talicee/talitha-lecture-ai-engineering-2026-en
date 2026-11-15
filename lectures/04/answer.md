# Lecture 04 Answers

## Exercises

- Agreement by criterion (before revision):
Grounding: 7/9
Scope: 10/10
Hint: 10/10
Clarity: 10/10
Lecture marker: 7/10

- Number of items needing review (before revision):1 (#05 Grounding).


- Criterion revised and the policy added:
    1. Revised Grounding in data/eval/rubric.md.

    2. Added a rule that if an answer says a term is not in the glossary and then provides a general explanation, it should still pass because it is not considered an unsupported assertion.

    3. Removed this issue from the Unresolved Questions section.


- Agreement by criterion and number of review items (after revision): Grounding: 8/10
Scope: 10/10
Hint: 10/10
Clarity: 10/10
Lecture marker: 7/10
Number of items needing review: 0.
Overall agreement: 6/10 (coverage: 100%).

- Items where your labels differed from the instructor's, and your reasons:

    1. #02, #07, and #09 (Lecture marker): I marked Pass because I saw that the answers already mentioned the related session, such as "Lecture 4". I assumed this was sufficient to satisfy the Lecture N requirement, but the code checks specifically whether the marker appears in the final line. I did not notice this exact requirement when labeling.

    2. #08 (Grounding): I marked Pass, but the answer revealed glossary entries even though the expected behavior was to refuse the request.

    3. #10 (Grounding): I marked Pass, but the answer claimed that Lecture 14 content would be added later, which was not supported by the references.

- Observations and questions:
    1. Clarifying the Grounding rule reduced the number of items needing review from 1 to 0.

    2. Overall agreement improved from 5/9 to 6/10.

    3. However, five disagreements remained, showing that clearer criteria do not automatically eliminate differences between human and LLM judgments.

    4. I learned that I need to follow the exact evaluation criteria rather than making assumptions based on the general meaning of an answer.

## Homework

- Level attempted: Basic 
- What you did: In the clarity section, I changed the wording (rule) from this: Choose fail if there is excessive paraphrasing or repetition of the same content (for example, repeating the same explanation with "In other words"), or too much explanation unrelated to the question. To this: Choose fail if the answer repeats the same information, includes unnecessary background details, or explains topics that are not needed to answer the user's question.

I assume being more specific about unnecessary explanations and repetition might affect how the LLM judges the answers.  This could make the evaluation more consistent.


- Results:

| Criterion      | Before | After |
|----------------|--------|-------|
| Grounding      | 8/10   | 8/10  |
| Scope          | 10/10  | 10/10 |
| Hint           | 10/10  | 10/10 |
| Clarity        | 10/10  | 10/10 |
| Lecture marker | 7/10   | 7/10  |
| Overall        | 6/10   | 6/10  |
| Needs review   | 0      | 0     |

- Observations and questions:
    - There were no changes to the result -> changing the Clarity wording did not affect the LLM's judgments.

    - Clarity already had 10/10 agreement, so the revised wording did not improve the score.

    - The five disagreements remained unchanged, particularly in Grounding and Lecture marker. Maybe change in other agreements might affect.

    - A wording change alone does not necessarily improve evaluation results.

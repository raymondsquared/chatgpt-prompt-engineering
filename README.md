# chatgpt-prompt-engineering
https://learn.deeplearning.ai/courses/chatgpt-prompt-eng/

---

[Guidelines](#guidelines)
- [Principle 1. Write clear and specific instructuctions](#principle-1-write-clear-and-specific-instructuctions)
  - [Tactic 1](#tactic-1-use-delimiters)
  - [Tactic 2](#tactic-2-ask-for-structured-output)
  - [Tactic 3](#tactic-3-ask-the-model-to-check-whether-conditions-are-satisfied-check-assumptions-required-to-do-the-task)
  - [Tactic 4](#tactic-4-few-shot-prompting-give-successful-examples-of-completing-tasks-then-ask-the-model-to-perform-a-task)

- [Principle 2. Give the model time to think](#principle-2-give-the-model-time-to-think)
  - [Tactic 1](#tactic-1-specify-the-steps-required-to-complete-a-task)
  - [Tactic 2](#tactic-2-instruct-the-model-to-work-out-its-own-solution-before-rushing-to-a-conclusion)

- [Hallucinations](#hallucinations)
---

# Guidelines 

## Principle 1. Write clear and specific instructuctions

#### Tactic 1. Use delimiters

Tiple backticks: ```

XML tags: <> </>

```code
Summarize the text delimited by triple backticks \ 
into a single sentence.
```{text}```
```

#### Tactic 2. Ask for structured output

```code
Generate a list of three made-up book titles along \ 
with their authors and genres. 
Provide them in JSON format with the following keys: 
book_id, title, author, genre.
```

#### Tactic 3. Ask the model to check whether conditions are satisfied, check assumptions required to do the task

```code
You will be provided with text delimited by triple quotes. 
If it contains a sequence of instructions, \ 
re-write those instructions in the following format:

Step 1 - ...
Step 2 - …
…
Step N - …

If the text does not contain a sequence of instructions, \ 
then simply write \"No steps provided.\"

\"\"\"{text_1}\"\"\"
```

#### Tactic 4. Few-shot prompting: Give successful examples of completing tasks then ask the model to perform a task

```code
Your task is to answer in a consistent style.

<child>: Teach me about patience.

<grandparent>: The river that carves the deepest \ 
valley flows from a modest spring; the \ 
grandest symphony originates from a single note; \ 
the most intricate tapestry begins with a solitary thread.

<child>: Teach me about resilience.
```

---

## Principle 2. Give the model time to think

#### Tactic 1. Specify the steps required to complete a task

Step 1: ...
Step 2: ...
...
Step N: ...

```code
Your task is to perform the following actions: 
1 - Summarize the following text delimited by 
  <> with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the 
  following keys: french_summary, num_names.

Use the following format:
Text: <text to summarize>
Summary: <summary>
Translation: <summary translation>
Names: <list of names in summary>
Output JSON: <json with summary and num_names>

Text: <{text}>
```

#### Tactic 2. Instruct the model to work out its own solution before rushing to a conclusion

```code
    Your task is to determine if the student's solution \
    is correct or not.
    To solve the problem do the following:
    - First, work out your own solution to the problem including the final total. 
    - Then compare your solution to the student's solution \ 
    and evaluate if the student's solution is correct or not. 
    Don't decide if the student's solution is correct until 
    you have done the problem yourself.
    
    Use the following format:
    Question:
    ```
    question here
    ```
    Student's solution:
    ```
    student's solution here
    ```
    Actual solution:
    ```
    steps to work out the solution and your solution here
    ```
    Is the student's solution the same as actual solution \
    just calculated:
    ```
    yes or no
    ```
    Student grade:
    ```
    correct or incorrect
    ```
    
    Question:
    ```
    I'm building a solar power installation and I need help \
    working out the financials. 
    - Land costs $100 / square foot
    - I can buy solar panels for $250 / square foot
    - I negotiated a contract for maintenance that will cost \
    me a flat $100k per year, and an additional $10 / square \
    foot
    What is the total cost for the first year of operations \
    as a function of the number of square feet.
    ``` 
    Student's solution:
    ```
    Let x be the size of the installation in square feet.
    Costs:
    1. Land cost: 100x
    2. Solar panel cost: 250x
    3. Maintenance cost: 100,000 + 100x
    Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
    ```
    Actual solution:
```

## Hallucinations

#### Reducing hallucinations:

First find relevant information then answer the question based on the relevant information

# Week 3 Lab: Python Research Workflow

## Exploring TikTok User Experience with Python

In today's lab, you will practice using Python to organize, retrieve, transform, and process information from a fictional TikTok user-experience study.

The goal is **not to conduct an actual TikTok analysis**. Instead, you will practice translating a research-related problem into a small computational workflow.

You will work in **Google Colab** and may use an AI assistant to help you understand code, debug errors, or develop a solution.

!!! important "Today's Goal"
You are not expected to memorize Python syntax. Focus on understanding **what the code is doing, why it works, and how you can verify the result.**

---

## Before You Begin

Open a new Google Colab notebook:

[Open Google Colab](https://colab.research.google.com/){ .md-button .md-button--primary }

Rename your notebook:

```text
JOUR701_Week3Lab_YourName
```

At the top of your notebook, create a Markdown cell containing:

```text
Name:
Assigned Activity:
```

---

## How Today's Lab Works

Each student will be assigned **one primary activity**.

Your job is to:

1. Read the task carefully.
2. Think about what Python needs to do.
3. Write or modify the code.
4. Run the code.
5. Inspect the output.
6. Use AI assistance if needed.
7. Verify that your solution actually answers the task.
8. Be prepared to share your screen and explain your process.

If you finish early, try another activity.

---

## Using AI During the Lab

You may use AI Assistant in Colab.

AI can help you:

* explain unfamiliar code
* give you a hint
* interpret an error message
* suggest a correction
* review your solution
* simplify complicated code
* suggest ways to test your result

However:

> **AI-generated code is a proposed solution, not a verified solution.**

When you use AI, add a Markdown cell to your notebook:

```text
AI prompt I used:

What AI suggested:

What I changed or used:

How I verified the result:
```

You may ask AI for the full code if that is useful, but you should still be able to explain what the important parts of the code are doing.

---

# Activity 1: Explore User Comments

A researcher collected several comments about users' TikTok experiences.

Copy this into your notebook:

```python
comments = [
    "I keep finding videos that match my interests",
    "There are too many ads now",
    "The For You page feels repetitive",
    "I like discovering new creators",
    "Sometimes I lose track of time while scrolling"
]
```

### Your Tasks

Without running the code first, predict what each operation should return.

Then use Python to:

1. Retrieve the first comment.
2. Retrieve the last comment.
3. Retrieve the second and third comments.
4. Retrieve the first three comments.
5. Find the total number of comments.


### If You Share Your Screen

Show one prediction you made before running the code and explain whether your prediction was correct.

---

# Activity 2: Clean a User Comment

A comment was entered with inconsistent capitalization and extra spaces.

```python
comment = "   I LOVE Discovering New Creators!   "
```

### Your Tasks

Transform the comment so that it becomes:

```text
i love discovering new creators!
```

Then replace:

```text
creators
```

with:

```text
accounts
```

### Think About

* Which string methods did you use?
* What object was each method acting on?
* Does the order of your operations matter?

### If You Share Your Screen

Explain your sequence of operations and why you chose that order.

---

# Activity 3: Build a User Record

Imagine one participant in a TikTok user-experience study provided the following information:

```text
Participant: P07
Daily use: 95 minutes
Primary reason: entertainment
Uses For You page: yes
Reported distraction: yes
```

### Your Tasks

1. Represent this participant as a Python dictionary.
2. Retrieve the participant's daily use.
3. Retrieve the participant's primary reason for using TikTok.
4. Add the following information to the dictionary:

```text
Age group: 18–24
```

### Think About

Why might this structure be more useful than storing all the participant information in one sentence?

### If You Share Your Screen

Explain the difference between a **key** and a **value** in your dictionary.

---

# Activity 4: Navigate Multiple User Records

A researcher has information from several participants:

```python
users = [
    {
        "participant": "P01",
        "daily_minutes": 45,
        "primary_reason": "entertainment"
    },
    {
        "participant": "P02",
        "daily_minutes": 120,
        "primary_reason": "news"
    },
    {
        "participant": "P03",
        "daily_minutes": 75,
        "primary_reason": "entertainment"
    }
]
```

### Your Tasks

Use Python to:

1. Retrieve the complete record for the first participant.
2. Retrieve P02's primary reason for using TikTok.
3. Retrieve P03's daily minutes.
4. Retrieve the final participant record without using its numerical position from the beginning.

### Think About

What kind of Python structure is `users`?

How are a **list** and **dictionary** being combined?

### If You Share Your Screen

Explain how Python moves through the nested structure to retrieve one specific value.

---

# Activity 5: Process Every Participant

Use the following records:

```python
users = [
    {"participant": "P01", "daily_minutes": 45},
    {"participant": "P02", "daily_minutes": 120},
    {"participant": "P03", "daily_minutes": 75},
    {"participant": "P04", "daily_minutes": 150}
]
```

### Your Tasks

1. Print every participant ID.
2. Print every participant ID together with their reported daily minutes.
3. Modify your code so that only participants reporting more than `90` minutes are printed.

### Think About

In this code:

```python
for user in users:
```

what does `user` represent during each repetition?

### Important

The `90`-minute threshold is being used only to practice Python conditions.

It is **not** a scientifically justified threshold for defining problematic or excessive TikTok use.

### If You Share Your Screen

Explain what part of your code repeats and what part makes a decision.

---

# Activity 6: Find Comments About the Algorithm

Consider these comments:

```python
comments = [
    "The algorithm knows what I like",
    "I mostly follow my friends",
    "The For You page feels repetitive",
    "I don't understand how the algorithm chooses videos",
    "The ads interrupt my experience"
]
```

Python can test whether one piece of text appears inside another:

```python
"algorithm" in comment.lower()
```

This produces either:

```text
True
```

or:

```text
False
```

### Your Tasks

1. Print only comments containing the word `"algorithm"`.
2. Count how many comments contain `"algorithm"`.

You may find this useful:

```python
count = 0
```

and:

```python
count += 1
```

`count += 1` means:

```python
count = count + 1
```

### Think About

Why might we use:

```python
comment.lower()
```

before searching for the word?

### If You Share Your Screen

Explain how your **loop**, **condition**, and **string method** work together.

---

# Activity 7: Create a Reusable Cleaning Function

Consider:

```python
comment = "   The FOR YOU Page Feels Repetitive   "
```

### Your Task

Create a function called:

```python
clean_comment()
```

that:

* removes spaces from the beginning and end
* converts the text to lowercase
* returns the cleaned comment

Then use the same function on the following comments:

```python
comments = [
    "   I LOVE Finding New Creators ",
    "The ALGORITHM Knows Me Too Well   ",
    "   Too Many ADS!   "
]
```

### Think About

Why might creating one reusable function be preferable to repeatedly writing the same cleaning commands?

### If You Share Your Screen

Show your function and explain what goes in and what comes out.

---

# Activity 8: Debug a Research Workflow

The following code is supposed to print participants who report more than 90 minutes of TikTok use.

However, it contains several problems.

```python
users = [
    {"participant": "P01", "minutes": 45},
    {"participant": "P02", "minutes": 110},
    {"participant": "P03", "minutes": 75}
]

for user in users
    if user["Minutes"] > 90:
    print(user["participant"])
```

### Your Tasks

1. Run the code.
2. Read the error message.
3. Fix the first problem.
4. Run the code again.
5. Continue until the code works correctly.
6. Identify each problem you found.

### Using AI

Try asking:

```text
Explain this Python error one problem at a time.
Do not rewrite the entire solution.
```

### Think About

Why might fixing one error reveal another error?

### If You Share Your Screen

Show us one error you encountered and explain how you identified the problem.

---

# Activity 9: Evaluate AI-Generated Code

Imagine you asked an AI assistant:

> Find all participants who use TikTok for more than 90 minutes.

The AI generated:

```python
heavy_users = [
    user["participant"]
    for user in users
    if user["minutes"] > 90
]
```

### Your Tasks

Without asking AI immediately:

1. Run the code.
2. Inspect the result.
3. Decide whether it appears to solve the task.
4. Identify which parts of the code you understand.
5. Identify anything you cannot explain.

Then ask AI:

```text
Rewrite this using a regular for loop and if statement.
Explain how the two versions accomplish the same task.
```

### Think About

* Is shorter code always better?
* Would you use code in a research project if you could not explain how it works?

### If You Share Your Screen

Compare the original AI-generated solution with the simpler version.

---

# Challenge Activity: Build a Mini Research Workflow

If you finish your assigned activity early, try this larger challenge.

```python
responses = [
    {
        "participant": "P01",
        "minutes": 45,
        "comment": "I like finding new creators"
    },
    {
        "participant": "P02",
        "minutes": 125,
        "comment": "The algorithm keeps me scrolling"
    },
    {
        "participant": "P03",
        "minutes": 80,
        "comment": "There are too many ads"
    },
    {
        "participant": "P04",
        "minutes": 140,
        "comment": "The algorithm is very accurate for me"
    }
]
```

### Complete as many tasks as you can

1. Display the final participant record.
2. Retrieve only P02's comment.
3. Print every participant ID.
4. Print participants with more than `90` minutes of use.
5. Print comments containing `"algorithm"`.
6. Create a cleaned lowercase version of each comment.
7. Ask AI to review your solution.
8. Identify one thing you personally verified.

---

# Screen Sharing

During class, you will be invited to share their screens.

When you share, briefly show:

1. **Your task**
2. **What you tried**
3. **Your code**
4. **Any error or challenge you encountered**
5. **How you used AI, if applicable**
6. **Your final output**
7. **How you verified the result**

You do **not** need to have a perfect solution to share.

Debugging, unexpected results, and alternative solutions are useful parts of the learning process.

---

# After Class

A worked solution notebook will be posted after the lab.

[View Week 3 Lab Solutions in Google Colab]([YOUR-COLAB-SOLUTION-LINK-HERE](https://colab.research.google.com/drive/1jI3zs4p2IYNlOcF09bsk_XStwgvDojNF){ .md-button }

Use the solution notebook to:

* compare approaches
* review code you found difficult
* understand errors
* try activities you were not assigned
* revisit the lab before future computational exercises

!!! note
The solution notebook provides **one possible approach**. Python problems often have multiple valid solutions. Focus on whether the code correctly performs the intended operation and whether you can understand and explain the workflow.

---

# What You Practiced

By the end of this lab, you should have practiced how to:

* organize information using lists and dictionaries
* retrieve information using indexes and keys
* transform text using string methods
* process multiple records using loops
* apply simple rules using conditions
* combine Python structures into small workflows
* create a reusable function
* interpret and debug errors
* use AI as a coding assistant
* verify AI-generated code

---

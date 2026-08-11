# Week 4 Lab: AI-Assisted Literature Prioritization with Hugging Face + Colab

## Overview

In this lab, you will explore how a pretrained Transformer model can help prioritize candidate literature for a research question.

The goal is **not** to automate or replace a systematic literature review. Instead, you will examine where AI-assisted screening may be useful, where human judgment remains necessary, and what kinds of evidence would be needed before relying on a model for literature screening.

By the end of the lab, you should be able to:

* Load a literature dataset into Google Colab
* Use a pretrained Hugging Face model to classify article abstracts
* Compare your own judgment with the model's judgment
* Examine disagreements between human and model decisions
* Revise classification labels and evaluate whether the output improves
* Save model results for review and submission

---

## 1. Prepare Your Group Dataset

Each group should have:

* One research question
* **3 peer-reviewed article abstracts per person**
* About **12–15 abstracts total** for a group of 4–5
* One combined `.csv` file
* Abstracts from **peer-reviewed journal articles only**

Your CSV file should include at least these columns:

```text
Group Member,abstract
Max,"This study examines how journalists use generative AI in daily work..."
Alex,"Using survey data, this study explores how young adults encounter news..."
Sarah,"This article analyzes how platform users evaluate health misinformation..."
```

Each student's name should appear next to the abstracts they personally contributed.

---

## 2. Open Google Colab and Upload Your CSV

Open a new Google Colab notebook.

Upload your group's CSV file to Colab.

Then load the file using pandas:

```python
import pandas as pd

df = pd.read_csv("your_file_name.csv")

df.head()
```

Check that:

* The file loads correctly
* Each row contains one abstract
* The correct group member is listed for each abstract

---

## 3. Human Judgment Comes First

Before looking at any AI output, return to the **3 abstracts you personally contributed**.

Read each abstract yourself and decide how relevant it is to your group's research question.

Use one of these labels:

* **Clearly relevant**
* **Possibly relevant**
* **Probably unrelated**

Record your judgment before running the model.

Do not change your original judgment after seeing what the AI predicts.

The purpose is to compare your own reasoning with the model's reasoning later.

---

## 4. Define the Classification Task

The model does not independently know what your research question means by "relevant."

You must define the possible labels.

For example, imagine your research question is:

> How is generative AI changing journalists' professional practices?

You might begin with labels such as:

```python
candidate_labels = [
    "relevant to the research question",
    "not relevant to the research question"
]
```

These labels tell the model what kinds of categories it should compare against.

---

## 5. Load a Pretrained Hugging Face Model

We will use a pretrained model through Hugging Face's `pipeline()` function.

```python
from transformers import pipeline
```

Create a zero-shot classification pipeline:

```python
classifier = pipeline(
    "zero-shot-classification",
    model="facebook/bart-large-mnli"
)
```

This allows us to give the model an abstract and a set of possible labels without training a new model ourselves.

---

## 6. Try One Abstract First

Before processing the full dataset, test the model on one abstract.

```python
abstract = df.loc[0, "abstract"]

result = classifier(
    abstract,
    candidate_labels
)

result
```

Look at:

* Which label received the highest score?
* How confident was the model?
* Does the prediction make sense based on your research question?

Ask yourself:

**Do you agree or disagree with the model? Why?**

---

## 7. Process the Full Abstract Dataset

Once your group understands how the model works, apply it to the full dataset.

One simple approach is:

```python
def classify_abstract(text):
    result = classifier(
        text,
        candidate_labels
    )
    
    return result["labels"][0]
```

Then apply the function to each abstract:

```python
df["AI Judgment"] = df["abstract"].apply(classify_abstract)
```

Preview the results:

```python
df.head()
```

---

## 8. Compare Your Judgment with the AI Judgment

Now return to the **3 abstracts you personally contributed**.

For each of your abstracts:

1. Compare your original human judgment with the AI judgment.
2. Decide whether you agree with the AI.
3. Record **Yes** or **No**.
4. Write a short explanation.

If you **agree with the AI**:

* Explain what evidence in the abstract supports the AI judgment.

If you **disagree with the AI**:

* Explain what the model may have misunderstood, overlooked, or interpreted incorrectly.

If you are **unsure**:

* Discuss that abstract with your group.
* Listen to your peers' reasoning.
* Then make **your own final Yes/No decision**.

You are responsible for completing the rows corresponding to **your own abstracts**.

Your table should look like this:

| Group Member | Abstract | Human Judgment    | AI Judgment  | Agree with AI? | Reason                                                                             |
| ------------ | -------- | ----------------- | ------------ | -------------- | ---------------------------------------------------------------------------------- |
| Alex         | ...      | Clearly relevant  | Relevant     | Yes            | The abstract directly examines AI use in journalistic work.                        |
| Maya         | ...      | Possibly relevant | Not relevant | No             | The model may have missed the connection between automation and newsroom practice. |

---

## 9. Change the Labels

The first labels you choose may be too broad.

Now revise the candidate labels so they better reflect your research question.

For example, instead of:

```python
candidate_labels = [
    "relevant",
    "not relevant"
]
```

you might try:

```python
candidate_labels = [
    "directly examines generative AI in journalists' professional work",
    "mentions journalism but does not examine generative AI use",
    "not related to the research question"
]
```

Run the model again using your updated labels.

Ask:

* Did the predictions become more useful?
* Did any previous disagreements disappear?
* Did new disagreements appear?
* Why might changing the labels change the model's judgment?

---

## 10. Run the Updated Model on the Full Dataset

Apply the revised labels to the full abstract dataset.

For example:

```python
def classify_abstract_updated(text):
    result = classifier(
        text,
        candidate_labels
    )
    
    return result["labels"][0]
```

Then:

```python
df["Updated AI Judgment"] = df["abstract"].apply(
    classify_abstract_updated
)
```

Preview the results:

```python
df.head()
```

---

## 11. Save Your Results

Save your completed dataset as a new CSV file.

```python
df.to_csv(
    "week4_ai_literature_results.csv",
    index=False
)
```

Download the file from Colab and make sure your group keeps a copy.

---

## 12. Final Human–AI Comparison

After running the updated model, review your own abstracts again.

For each abstract you contributed, your final table should include:

* Group member name
* Abstract
* Your original human judgment
* AI judgment
* Agree with AI: Yes or No
* Brief reason

Your reason should explain **why** you agree or disagree.

Do not simply write:

```text
Yes, I agree.
```

Instead, connect your explanation to the abstract and the research question.

For example:

```text
Yes. The abstract directly examines how journalists use generative AI in their daily professional workflow.
```

Or:

```text
No. The abstract discusses digital journalism broadly, but it does not examine generative AI use, which is central to our research question.
```

---

## 13. Discuss One Interesting Disagreement

As a group, identify **one disagreement** that you think is especially useful or interesting.

Be prepared to briefly explain:

* Your research question
* The abstract
* The human judgment
* The model judgment
* Whether the human reviewer agreed or disagreed with the AI
* Why the disagreement may have occurred
* What you would do next as a researcher

Possible reasons for disagreement include:

* The abstract is genuinely ambiguous
* The labels are too broad
* The labels are poorly defined
* Important context is missing from the abstract
* The model focused on the wrong words
* Human reviewers interpreted the research question differently

---

## Assignment 2 Deliverable

Submit **one agreement table file per group** on Blackboard.

**Due: 5:00 PM tomorrow**

The file should include:

| Group Member | Abstract | Human Judgment | AI Judgment | Agree with AI? | Reason |
| ------------ | -------- | -------------- | ----------- | -------------- | ------ |

Although the group submits one combined file, **each student is responsible for the rows corresponding to the abstracts they personally contributed**.

Your individual portion will be evaluated based on whether you:

* Completed your assigned abstracts
* Made a clear human judgment
* Compared that judgment with the model
* Provided a meaningful Yes/No agreement decision
* Explained your reasoning using evidence from the abstract and the research question

---

## Before You Leave

Consider this question:

**Would you allow this model to automatically exclude papers from your literature review?**

Think about:

* Why or why not?
* What kinds of errors would matter most?
* What evidence would you need before trusting the model?
* Where should human judgment remain in the workflow?

---

## Key Takeaway

AI can help researchers **screen and prioritize abstracts**, especially when working with larger collections of literature.

However, human judgment is still needed to:

* Define what relevance means
* Evaluate ambiguous cases
* Interpret disagreements
* Refine classification labels
* Protect against accidentally excluding important studies

A reproducible Python workflow makes AI-assisted literature screening easier to **inspect, critique, compare, and improve**.


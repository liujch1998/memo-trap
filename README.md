# The MemoTrap Dataset

This repository hosts MemoTrap, a diagnostic dataset that probes whether language models would fall into memorization traps.
We have found that larger LMs tend to be more susceptible to memorization traps than smaller LMs.
MemoTrap is a prize-winning submission in the [Inverse Scaling Challenge](https://irmckenzie.co.uk/round2).

## Introduction

MemoTrap consists of 4 subtasks.
Each subtask has its data in one of the CSV files in the `data` folder.
Below is a description of the subtasks.

| Subtask | File name | Size |
| ---- | ---- | ---- |
| Proverb Ending | 1-proverb-ending.csv | 860 |
| Proverb Translation | 2-proverb-translation.csv | 843 |
| Hate Speech Ending | 3-hate-speech-ending.csv | 100 |
| History of Science QA | 4-history-of-science-qa.csv | 736 |

## Format

Each data instance has 3 keys: `prompt`, `classes`, and `answer_index`.
`prompt` is the input to the LM.
`classes` is a list of two candidate continuations to the prompt.
`answer_index` is the index of the desired continuation in `classes`.

Note that `classes` is a string version of a list and may contain escape characters that are hard to deal with.
Here is a code snippet that loads the data file correctly:
```
import ast
import csv

with open('data/1-proverb-ending.csv') as f:
    reader = csv.DictReader(f)
    for row in reader:
        prompt = row['prompt']
        classes = ast.literal_eval(row['classes'])
        answer_index = row['answer_index']
```

## References

MemoTrap contains data adapted from the following sources:

* English proverbs, Wikiquote. [https://en.wikiquote.org/wiki/English_proverbs](https://en.wikiquote.org/wiki/English_proverbs)
* The History of Science, Volume 1-5 (2nd ed.). Ray Spangenburg and Diane Kit Moser. Facts on File, 2004.


---
title: "R to Python"
description: "Helpful stuff for R users learning Python"
date: 2024-08-30
featured_image: ""
tags: []
draft: false
---

# Helpful stuff for R users learning Python

## Building DataFrames
df = df.assign(
    event_outcome = df["points"].case_when([
        (df["points"] == "C",   "Cancelled"), 
        (df["points"] == "DNF", "Did Not Finish"), 
        (df["points"] == "DNS", "Did Not Start"), 
        (df["points"] == "WH",  "Wind Held"),
        (df["points"] == "DSQ", "Disqualified"),
        (lambda s: pd.isna(s), 'Did Not Compete'),
        (lambda s: pd.to_numeric(s, errors="coerce").notna(), "Points Gained"),
        # (True, "Points Gained")   # default catch-all
    ])
)

### Generating different types


| Concept      | R                          | Python                                              |
| ------------ | -------------------------- | --------------------------------------------------- |
| Vector       | `c(1,2,3)`                 | `np.array([1,2,3])` or `pd.Series([1,2,3])`         |
| List         | `list(a=1, b=2)`           | `{"a":1, "b":2}` (dict) or `[1, "hi", TRUE]` (list) |
| Matrix       | `matrix(1:6, ncol=2)`      | `np.array([[1,2,3],[4,5,6]])`                       |
| DataFrame    | `data.frame(x=1:3, y=4:6)` | `pd.DataFrame({"x":[1,2,3], "y":[4,5,6]})`          |
| Named vector | `c(a=1, b=2)`              | `pd.Series([1,2], index=["a","b"])`                 |



### Indexing different types

| Task              | R                    | pandas / NumPy   |
| ----------------- | -------------------- | ---------------- |
| Column by name    | `df$col`             | `df["col"]`      |
| Row by number     | `df[1, ]`            | `df.iloc[0]`     |
| Row by label      | `df["id42", ]`       | `df.loc["id42"]` |
| Subset col vector | `df[,1]`             | `df.iloc[:,0]`   |
| Keep as DataFrame | `df[,1, drop=FALSE]` | `df[["col"]]`    |

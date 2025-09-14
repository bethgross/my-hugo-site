---
title: "R to Python"
description: "Helpful stuff for R users learning Python"
draft: false
---

# Helpful stuff for R users learning Python


## Building DataFrames

{{< twocol >}}

### R
```r
df <- df %>% 
  mutate(
    event_outcome = case_when(
      points == "C"  ~ "Cancelled",
      points == "DNF"~ "Did Not Finish",
      points == "DNS"~ "Did Not Start",
      points == "WH" ~ "Wind Held",
      points == "DSQ"~ "Disqualified",
      is.na(points)  ~ "Did Not Compete",
      TRUE           ~ "Points Gained"
    )
  )
  ```

<!--col-->
### Python
```python
df = df.assign(
    event_outcome = df["points"].case_when([
        (df["points"] == "C",   "Cancelled"), 
        (df["points"] == "DNF", "Did Not Finish"), 
        (df["points"] == "DNS", "Did Not Start"), 
        (df["points"] == "WH",  "Wind Held"),
        (df["points"] == "DSQ", "Disqualified"),
        (lambda s: pd.isna(s), 'Did Not Compete'),
        (lambda s: pd.to_numeric(s, errors="coerce").notna(), "Points Gained"),
    ])
)
```
{{< /twocol >}}

## Building DataFrames

{{< twocol >}}

### R
```r
df <- df %>% 
  mutate(
    event_outcome = case_when(
      points == "C"  ~ "Cancelled",
      points == "DNF"~ "Did Not Finish",
      points == "DNS"~ "Did Not Start",
      points == "WH" ~ "Wind Held",
      points == "DSQ"~ "Disqualified",
      is.na(points)  ~ "Did Not Compete",
      TRUE           ~ "Points Gained"
    )
  )
  ```

<!--col-->
### Python
```python
df = df.assign(
    event_outcome = df["points"].case_when([
        (df["points"] == "C",   "Cancelled"), 
        (df["points"] == "DNF", "Did Not Finish"), 
        (df["points"] == "DNS", "Did Not Start"), 
        (df["points"] == "WH",  "Wind Held"),
        (df["points"] == "DSQ", "Disqualified"),
        (lambda s: pd.isna(s), 'Did Not Compete'),
        (lambda s: pd.to_numeric(s, errors="coerce").notna(), "Points Gained"),
    ])
)
```
{{< /twocol >}}



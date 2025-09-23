---
title: "R to Python"
description: "Helpful stuff for R users learning Python"
date: 2025-09-22T00:00:00Z
featured_image: '/images/r_to_python_gemini.jpg'
draft: false
---

Helpful stuff for R users learning Python. I've selected the methods that I like best. 


## Building DataFrames

{{< twocol >}}

### R
```r

library(tidyverse)

df <- df %>% 
  mutate(
    event_outcome = case_when(
      points == "C"   ~ "Cancelled",
      points == "DNF" ~ "Did Not Finish",
      points == "DNS" ~ "Did Not Start",
      points == "WH"  ~ "Wind Held",
      points == "DSQ" ~ "Disqualified",
      is.na(points)   ~ "Did Not Compete",
      TRUE            ~ "Points Gained"
    )
  )
  ```

<!--col-->
### Python
```python

import pandas as pd

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

## Subsetting

{{< twocol >}}

### R
```r

library(tidyverse)

df %>% select(column_1, column_2, column_5:column_6)

  ```

<!--col-->
### Python
```python

import pandas as pd

df[["column_1", "column_2"] + list(df.columns[4:6])]

```
{{< /twocol >}}


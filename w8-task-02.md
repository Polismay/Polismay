---
title: "WAITLISTED"
author: "POLISMA YADAV"
date: "November 04, 2021"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---






```r
# Use this R-Chunk to import all your datasets!
```

## Background

_Place Task Background Here_

## Data Wrangling


```r
waitlist <- read_csv("https://byuistats.github.io/M335/data/waitlist_DP_108.csv")
waitlist2 <- waitlist %>%
  mutate(date = lubridate::mdy_hm(`Registration Date`))

registered_from_wl <- function(section) {

dat1 <- section %>%
  arrange(`Person ID`, desc(date), desc(`Status`)) %>%
  distinct(`Person ID`, .keep_all = TRUE) %>%
  filter(Status == "Registered")

totals <- dat1 %>% summarise(registered = n(),
  reg_from_wl = sum(`Waitlist Reason` == "Waitlist Registered", na.rm = TRUE))

totals$reg_from_wl / totals$registered
}

section18 <- waitlist2 %>% filter(`Course Sec` == "FDMAT108-18")
registered_from_wl(section18)
```

```
## [1] 0.2121212
```

## Data Visualization


```r
# Use this R-Chunk to plot & visualize your data!
```

## Conclusions

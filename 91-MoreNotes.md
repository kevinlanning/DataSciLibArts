

matching and splitting

What about the names which are most androgynous?  How would you get this?



If you get stuck,  

## Summariz(s)e

Reduces a variable to one or more values.

Use summarise() to compute the earliest (minimum) year in the dataset

```{r summarize}
# gapminder 
```

## Group by

Summarize is really useful with group by, and group by is really useful for categorical variables. 

Find the median life expectancy by continent in 2007, or another comparison between groups (such as continent or year).

```{r summarizeGroups}
# gapminder 
```





Find one feature of it, and write code which shows how it works.

1. Work in your source window. On the first line, enter the command to install the tidyverse. (If you already have done this, you can comment out the command ...)

   ```
   # install.packages ("tidyverse")
   ```

   Hit ctrl+enter to run this line. Then, comment it out if you haven't already done so (why)?

2. Load the tidyverse into your workspace. 

3. Load the movies/IMDB dataset.

## univariate data

kable and other approaches to generating output

exercise 27.4.7 2 (https://raw.githubusercontent.com/hadley/r4ds/master/rmarkdown/diamond-sizes.Rmd)

## 

## Joins

You often need to combine different datasets.

One way is to add new rows (observations) for your current set of variables.

Another is to add new columns (measures or variables) for your current set of observations.

Consider the following...

```{r}
country_codes
```

We can combine it with the gapminder data using a version of join, for example, ...

```{r}
gapminder %>% left_join(country_codes)
```

Note that join is smart enough to match the two files on the variable they share...

Excerpts from *Data Science in the Tidyverse* - Sections 5

Note the fivethirtyeight package.  Install, open, and play with it as you would a birthday present.

```{r setup0314} 
library(tidyverse)
library(lubridate)
library(fivethirtyeight)
```

## From section 05 - Data-Types

Find and open the General Social Survey data. 

Find the average hours of tv watched (`tvhours`) for each category of marital status (`marital`).

```{r tvMarriage}
# why doesn't this work?
#div <- filter(gss_cat, marital=="Divorced")
#div
#x = div[3]
#x <- as.numeric(x[[1]])
#mean(x)
# one method
(by_marital <- group_by(gss_cat, marital))
summarise(by_marital, avetvhours = mean(tvhours, na.rm = TRUE))

# pipe method
gss_cat%>%
  group_by(marital) %>%
    summarise(means=mean(tvhours,na.rm=TRUE))
# gss_cat
# etc
```

How did you handle missing values?

Homework due Feb 14 (with a solution).

------

### "Diamond sizes" (27.4.7 - #2)

This is from Hadley's book, with an initial shot at the code from Reill.

"Download diamond-sizes.Rmd from https://github.com/hadley/r4ds/tree/master/rmarkdown. Add a section that describes the largest 20 diamonds, including a table that displays their most important attributes"

We copied the text of this into the present file, saving it as an 'r markdown' file.

### Downloaded file block 1

### My revised graph

4) **Change 1 or more parameters of this graph to make it more useful.  Describe your changes here**

**I re-binned the x axis and labeled modal values** 

```{r, echo = TRUE}
smaller %>% 
    ggplot(aes(carat)) + 
    geom_freqpoly(binwidth = .125) +
    scale_x_continuous(
        breaks = c(0, .375, .75, 1, 1.25, 1.5, 2, 3))
    
```

### Syntax for table (kable)

In class, Lanning showed how to use kable to generate a nicer looking table, of just the first five rows (observations) and columns (variables or attributes).

```{r, echo = TRUE}
smallest <- smaller [1:5,1:5]
# smallest # this would generate an ugly table - remove the first hashtag if you don't believe me
# str(diamonds)
knitr::kable(smallest, 
  caption = "Five rows and columns of the diamonds frame."
)
```

### The assignment ... 

The assignment is to 'Add a section that describes the largest 20 diamonds, including a table that displays their most important attributes'

One way to do this is 

- (a) sort the file by size [Google 'sort r data frame by a variable.'], 
- (b) save this sorted file with just the 20 largest diamonds [see the code block above for an example], and,
- (c) choose the most important variables [you'll have to make a judgement call here, then use the above]; then make a new table. 

5) **Insert your code here**

```{r, echo = TRUE}
attach(smaller)
rankedDiamonds<-smaller[order(-carat),]
rankedDiamonds<-rankedDiamonds[1:20,c(1:4,7)]
knitr::kable(rankedDiamonds, 
  caption = "20 largest diamonds, select columns")
```

### If at first you don't succeed

How hard did you try? 

6) **Document that you tried for at least 30 minutes, where you looked, and what you learned in your struggles**

### If you get this far

Now rewrite your code in as few lines as possible. (I do NOT mean omitting comments.  Which of the above steps is necessary to answer the assignment?) 

Here's one answer - using 'arrange' instead of order...

```{r, echo = TRUE}
knitr::kable(arrange(smaller,-carat)[1:20,c(1:4,7)])
```

Finally, generate HTML, Word, and PDF versions of this document. 

8) **Are these different output formats useful for you? explain**  <- replace this line with an answer

## 
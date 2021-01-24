# now draw the rest of the owl



![Fig 4.1: Draw the rest of the owl.](images/InkedrCr9A_LI.jpg)

There are many sources for learning the basics of R. A few of these follow.  Please **spend at least 90 mins exploring at least two of the following.** Be prepared to discuss your progress next class (you will be asked which source(s) you used, what you struggled with, and whether you would recommend it to your classmates. (Note that all of these are free, though you may choose to make a donation to the author if you use the Peng text).

>   **Hint:** If you find the material too challenging - if you feel like you are drawing the rest of the owl - take a break away from your machine and other screens, clear your head, then try a different approach.

## The RStudio cloud primers
The Basics > Data Visualization Basics primer

## Carmichael

Iain Carmichael prepared the following for his Intro to Data Science course at UNC-Chapel Hill. I think it is a great place to start: https://idc9.github.io/stor390/notes/getting_started/getting_started.html

## DataCamp

Many folks swear by (and others, I presume, at) DataCamp, which kind of gamifies learning software.  As a student in this class, you have access to all of their stuff... free. You can even do lessons on your phone.

## Swirl (Swirlstats)

I, like thousands of others, learned R in the process of completing the Johns Hopkins [Data Science Specialization](https://jhudatascience.org/courses.html) offered through [Coursera](https://www.coursera.org/). The sequence can be challenging, but their introduction to R used an accessible, interactive R package called *Swirl.* You can read about swirl ("learn R in R") at https://swirlstats.com/.  

**Using Swirl.** After loading R (and opening R studio), you will get to the Swirl lessons with the following steps: 

1) Install the Swirl package on your computer (you only need to do this once). Type the following into your console window in R studio (typically left hand side of your screen or lower left)

>   install.packages("swirl") 

2) Then load the package into your workspace (you'll need to do this at the beginning of every session you use Swirl) 

>   library (swirl)

2) Then run it! 

>   swirl ()

Swirl will ask a few questions then give you the option of choosing one of several courses. You'll choose the R Programming option, which leads to 15 separate lessons.

At the end of each lesson, you'll be asked 

>   *Would you like to receive credit for completing this course on Coursera.org?*

Answer no... then do another lesson.

## Peng text and videos

Finally, consider the text and videos from the Coursera R class.  Most of the material from that class can be found in @peng2014.  A slightly updated version of the text can be found at https://bookdown.org/rdpeng/rprogdatascience/, and the videos in the series may be found by clicking on the following:  

[![Roger Peng](https://img.youtube.com/vi/wy0h1f5awRI/0.jpg)](https://youtu.be/wy0h1f5awRI).
*Video 4.2: Roger Peng introducing R*

## Something else

The "something else" category includes Datacarpentry.org, which is aimed at fostering data literacy and provides free lessons for learning and applying R in areas such as [Ecology](https://datacarpentry.org/R-ecology-lesson/), [Genomics](https://datacarpentry.org/genomics-r-intro/) and [Geospatial data analysis](https://datacarpentry.org/r-intro-geospatial/). Of particular interest are the [social science](https://datacarpentry.org/r-socialsci/) lessons, as well as a workshop in data science based on the "[Studying African Farmer-led Irrigation (SAFI)" dataset](https://datacarpentry.org/socialsci-workshop/).

## An exercise

Review Carmichael's [Getting started with R](https://idc9.github.io/stor390/notes/getting_started/getting_started.html).  Open R studio, and create a new R script called myMovies.R. Using his code as a reference, do each of the following

1. Work in your source window. On the first line, enter the command to install the tidyverse, using the chunk below - but omit the [octothorpe](https://en.wiktionary.org/wiki/octothorpe). (If you've already installed the tidyverse, keep the #).

   ```
   # install.packages ("tidyverse")
   ```

   Hit ctrl+enter to run this line. Now comment it out if you haven't already done so (why)?

2. Load the tidyverse into your workspace. 

3. Load the movies/IMDB dataset.

4. Start exploring the data and the RStudio interface:

   - Apply the str (structure), head, and summary commands. When are each of these useful?
   - Double-click the movies dataset in your environment tab in R studio. Click on a few columns to sort the data.
   - In the data, what does 'spilled' mean? How did you find out?

5. How many rows and columns are in the data? 

6. We can think about the movies dataset as a matrix with rows and columns, and *subset* it using the following. 
   ```
   # data.frame[rownumber,colnumber]
   # data.frame["rowname", "colname"]
   # data.frame[rowname, c("colname, colname")]
   movies["title"]
   movies[title]
   movies[title,]
   ```

7. Ask an interesting question about the data, and enter it as a comment in your code, e.g., 

   ``` # how long was the movie 42-up? ```

8. Try to find the answer, ideally using reproducible code, and be prepared to share it with the class.

9. Save your work :)

### An initial solution

Here's a sample solution supplied by one group of students. I've added some comments to make it useful to my present and future self.
```
# notes from class 1/22/20
# exercise in Data Science for Liberal Arts
# contributed by _________ _______ 
# ----------
# run this line just once to put package on machine
# install.packages("tidyverse")
library(tidyverse)
# this loads a movie dataset from the web
load(url('https://stat.duke.edu/~mc301/data/movies.Rdata'))
# some ways to look at the dataset
View(movies)
str(movies)
head(movies)
summary(movies)
head(movies$genre)
head(movies$genre,100)
# an initial plot 
ggplot(data = movies) + 
  geom_point(mapping = aes(x = imdb_rating, 
                           y = critics_score))
# what does "spilled" mean?
summary(movies$audience_rating)
ggplot(data = movies) + 
  geom_point(mapping = aes(x = audience_score, 
                           y = audience_rating))
# this displays the list of movies
movies["title"]
# this writes the list of movies to a new vector
b <- movies["title"]
# which genre has the highest audience score?
ggplot(data = movies) + 
  geom_point(mapping = aes(x = genre, 
                           y = audience_score, 
                           color=mpaa_rating))
ggplot(data = movies) + 
  geom_point(mapping = aes(x = genre, 
                           y = audience_score, 
                           color=audience_score))
# these commands fail - why?
# view(genre,audience_score)
# summary(genre,audience_score)
# Summary("genre")
#
# this works!
c <- movies["genre"]

# but not this
# d <- movies("audience_score")
d <- movies["audience_score"]
#
# subsetting a file
#
# base syntax to create a new file 
# with the 3rd,4th, and 7th columns in movies
movies2 <- movies[,c(3,4,7)]
# tidyverse syntax to 
# create a new file with just the first variable in movies2
movies3 <- movies2 %>% select(1)
```
## An introduction to R markdown

The above script worked fine, but it is not a good record of my examination of the movie database.  It tells only part of the story (it doesn't include the results), and it doesn't tell it particularly clearly (the comments that explain the logic and syntax of my work are mixed in with the code that executes it).

In *literate programming*, these aspects of work are clearly articulated and retained. R markdown documents are tools for elegantly integrating comments, code, and results - they *document* our work. We'll return to this in some detail later; for now, to create an R markdown (Rmd) document in R studio, begin with (**File -> New File -> R Markdown**). A window will open up with a file that begins with some *YAML* (Yet Another Markdown Language). You can edit this as needed:
```
---
title: "My first R Markdown Document"
author: "Frankie McFrank Frank"
date: "1/27/2020"
output: html_document
---
```
Click on the clever "knit" icon in the bar just above the source window to create a sample document. You'll need to save the file with a new name, then R will finally create an HTML (Hyper Text Markdown Language - see the pattern?) page.

Compare the R Markdown document (your code) with the result (the HTML). Now, try to knit the document into different output formats (click on the down arrow next to knit, and see if you can knit to PDF and Word). It may take a while the first time you do this, as you may need to load some additional formatting tools or packages (e.g., TinyTex) to successfully render these files.

After you have admired the results, continue editing your .Rmd document. You will replace the chunks (everything but the YAML at the top of the document) with the code from the Carmichael project.  You can insert a chunk of code using the "insert" then "R" commands at the top of your source window. 

### Step-by-step

When I am writing an R markdown document in R studio, I'll generally work on one chunk at a time, testing each in turn (generally by clicking the run triangle at the top of the chunk). Once I am done, I knit the document as a whole as a complete record of my work. 

My first chunk loads the libraries and data. When I write this, I'll modify the top of the chunk to say {r message=FALSE} rather than just {r} so that I don't get too much chatter about this step:
```{r message=FALSE}
library(tidyverse)
load(url('https://stat.duke.edu/~mc301/data/movies.Rdata'))
```
 
So from here on, the shaded blocks include code and results. My next verbatim chunk looks like this when I write it and when I test it:
```
```{r whatever}
str(movies)
head(movies)
summary(movies)
head(movies$genre)
# head(movies$genre,100) why is this commented out?
```
```
When I "knit" it, the results are folded in as follows:
```{r}
str(movies)
head(movies)
summary(movies)
head(movies$genre)
# head(movies$genre,100) why is this commented out?
```
### Spilled???

In class, we were asked "what does "spilled" mean?" We looked at the audience_rating variable (spilled) to see if it was related to audience_score;
```{r}
summary(movies$audience_rating)
ggplot(data = movies) + 
  geom_point(mapping = aes(x = audience_score, 
                           y = audience_rating))
```

Bingo! Eyeballing this, it looks like scores 60 and above are "upright," those below 60 are 'Spilled.' What would I need to do to test this more explicitly?

### Your turn

Now, add sections which describe and examine the "interesting question" you asked about the movie dataset. I don't expect statistical tests but I do ask that you think about your work and that, after your last chunk of code, you include a section of text which describes the next steps that you feel would be needed on the project to give you confidence in your results.  Knit the result to a PDF, and rename this as YourLastNameMovie1.pdf. I'll collect in the next class.




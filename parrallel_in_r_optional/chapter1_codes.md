# Chapter 1

- Lecturer: Hana Sevcikova
- Title: Senior Research Scientist at UW

# Courses:

## Partitioning problems into dependent pieces 1 out of 4

**Prerequisites**

- Writing Efficient R
- Optimized sequential code
- Benchmark your code

**Objective**

- Ready to break your code into multiple pieces that can run in parrallele, load-balanced and in reproducible manner.

### Overview:

1. Methods of parrallele proramming & supporting R packages
2. The parallel core package in detail
3. Packages foreach and future.apply
4. Random numbers & reproducibility and final example

- **Why we need parrallel? Why we need Partitioning? and How to split them??**
- Let me show you example for How:

1. By Tasks
2. By Data

**By Tasks**:
For building a house, there are many tasks can do independently, and in parrallel: such as roofing, installing window, plumbing, flooring, etc.

**By Data**:
For building a house, all windows can be installed in parrallel. SAME TASK, apply on different data in parrallel.

#### Summary of partitioning

1. By Task: Apply different tasks to the same or different data.
2. By Data: The same task is performed on different data.

- Embarrassinly parallel applications - means so easy to make it in parrallel

## Models of parallel computing 2 out of 4

# Practices:

### Practice 1 out of 4:

Yuanfeng Li
10282021

#### Partitioning demographic model

**Question1**
Consider a demographic projection model at time t: Population(t) = Population(t-1) + Births(t) - Deaths(t) + Net Migration(t), consisting of four submodels, namely for projecting births, deaths, migration and population at time t-1. How can this model be split into independent pieces that could run in parallel?

Possible Answers:

1. The model cannot be parallelized.
2. All four submodels can run in parallel.
3. Submodels Births, Deaths and Migration can run in parallel but not Population.

I have chosen 1, and is incorrect, the hint says: "No! Some submodels are independent of one another."

I have chosen 2, and is incorrect, the hint says: "No! Look for dependencies in the model equation."

I have chosen 2, and is incorrect, the hint says: "Yes! Projecting population depends on births, deaths and migration, therefore it cannot run independently of those submodels. You just partitioned a problem by TASK!"

**Question2**
Partitioning probabilistic demographic model
Now consider a probabilistic version of the previous model. In this case, each of the four submodels processes a set (not just one) of independent trajectories of their respective quantity. How can this model be parallelized?

A. Now the Population submodel can also run independently of the other three submodels.
B. Each submodel can process each trajectory in parallel to other trajectories.
C. Submodels Births, Deaths and Migration can run independently of one another but no parallelization within the submodels.
D. The Population submodel can be only parallelized by trajectories.

Answer possible:

1. A & B
2. B & D
3. C & D
4. A & C

Choose 2 is correct:
Yes! Trajectories are independent of one another, therefore they can be processed in parallel in all four submodels including Population. Congratulations, you just partitioned a problem by DATA! The same task (submodel) is applied to different data (trajectories).

Others are incorrect: 1  
No! The model equation did not change. Population still depends on births, deaths and migration.

3 4
No! Trajectories are independent of one another, therefore they can be processed in parallel within each submodel.

**Coding Practice 1**:
Find the most frequent words in a text
We will now turn to partitioning by data. Here is an example that will be used throughout the course: In the given text, find the most frequent words that start with each letter of the alphabet and are at least a given length long. You'll use the janeaustenr package with its 6 books by Jane Austen, which is available in your environment. Also loaded are the stringr package and the function janeausten_words(), which extracts words from the 6 books and converts them to lowercase. Here, the specific task is to find, for each letter of the alphabet, the most frequent word that is at least five characters long. Your job is to partition this task into independent pieces.

- instructions:

  1. The object words contains all words from the 6 books. Use the preloaded function max_frequency() to find the most frequent word of all words starting with an "a" (arg letter) that are 5 or more characters long (arg min_length).

  2. To partition the main task, let the lapply() function repeatedly call max_frequency() over all letters.
     To enumerate all letters of the alphabet, call lapply() on letters.
     The arguments words and min_length are the same as your first call of max_frequency().
     (My perspective is that letters is another vector defined earlier)

3. Plot a barplot of result.

```
# 1st instruction
# Vector of words from all six books
words <- janeausten_words()

# Most frequent "a"-word that is at least 5 chars long
max_frequency(letter = "a", words = words, min_length = 5)


# 2nd instruction
# Partitioning
result <- lapply(letters, max_frequency,
                 words = words, min_length = 5) %>% unlist()

## 3
# Barplot of result
barplot(result, las = 2)
```

see the barplot here
![barplot 1_1](./barplot_1_1.png)

Excellent! You have partitioned the task into independent pieces using “lapply()” (an alternative is to use a “for” loop). The function “max_frequency()” is repeatedly applied to a different part of the data, namely one letter of the alphabet.

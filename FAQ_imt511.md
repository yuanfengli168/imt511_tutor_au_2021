# FAQ for IMT511 in Autumn 2021

- Date: Fall 2021
- Tutor: Yuanfeng Li (Jacky Li)

1. **Homework submission**:

   Question:

   If I've tested all my Module 1 exercise files and all have passed,There is no further action on my part for submission right?

   Answer:

   Correct!
   Please follow professor's guidance in this [link](https://canvas.uw.edu/courses/1479816/pages/completing-assignments-in-rstudio)

1. **variable name** & quotation mark:

   Can we have a single quotation mark around the variable name?

   ```
   line1: 'name' <- "Jacky"
   line2: "name" <- "imt511"
   line3: name <- "Best"

       Answer: please not use any quotation marks around variable names! The code in line3 is recommended.

   ```

   Please follow the tidyverse style guide, [link](https://style.tidyverse.org/)

1. **Failures** & don't know why:

   Question:

   My function returns the correct string, why I am still getting an error?

   ```
   # R tests looking for:
   line1: "String 1 and String 2 have equal length."

   # Your return:
   line2:"String one and String two have equal length"

   # they are not the same string for test case
   ```

   Answer:

   The tests you are running are strict, and they are looking for exactly the same format which the question provided.

   In most cases, line1 and line 2 are diffrent, and please pay attention to special characters you used, such as a extra space/different quotation mark/different input keyboard/etc.

   All of these can return a failure, even though the rest of your returns are identical to the correct answer.

1. **Check** before you run:

   Some times you might make some really simple mistakes. If you don't double check them before you run your program, you will having troubles. There are 2 common errors that even the best programmers might make:

   ```
   line1: fraction <- function(numerator, denominator) {
   line2:   return(numerator/demominator
          }

   # Typo between denominator(line1) and demominator(line2)
   # Missing parenthesis.

   # the correct one should look like this:
   line1: fraction <- function(numerator, denominator) {
   line2:   return(numerator/denominator)
          }

   ```

   Typo are really common error that everyone might make, in order to prevent this type of error.

   Missing Punctuation marks are common too, such as missing parenthesis, square brackets, curly braces, etc.

   Please double check if you make any of this mistakes when the certain error appears.

1. Mini CheatSheet for DataFrames functions:

   ```
   # nrow(), ncol(), dim(), colnames(), rownames()
   # examples:

   # Create the same data frame as above
   my_data <­ data.frame(name, height, weight, stringsAsFactors = F)
   # Describe the structure of the data frame
   nrow(my_data) # [1] 5
   ncol(my_data) # [1] 3
   dim(my_data) # [1] 5 3
   colnames(my_data) # [1] "name" "height" "weight"
   rownames(my_data) # [1] "1" "2" "3" "3" "5"

   # Create a vector of new column names
   new_col_names <­ c("first_name", "how_tall", "how_heavy")
   # Assign that vector to be the vector of column names
   colnames(my_data) <­ new_col_names
   ```

Updating...102821

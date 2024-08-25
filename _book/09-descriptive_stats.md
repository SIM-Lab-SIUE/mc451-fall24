# Descriptive Analysis

Descriptive statistics form the bedrock of data exploration and initial data analysis. Descriptive analysis plays a pivotal role in data analysis by concisely summarizing the key characteristics of a dataset. It involves calculating various statistics to present a snapshot of the data, enabling researchers to understand its basic structure and form. These statistics facilitate the comprehensive summarization, condensation, and general understanding of the structural attributes of expansive datasets. Employed as a precursor to more advanced statistical procedures, descriptive statistics offer a straightforward way to describe the main aspects of a data set, from the typical values to the variability within the set. They provide researchers with tools to quickly identify patterns, trends, and potential outliers without making generalized predictions about larger populations. Furthermore, descriptive statistics are essential in exploratory data analysis, where their role is to aid in the detection of any unusual observations that may warrant further investigation.

Moreover, descriptive statistics have applications that span across various domains---from social sciences to economics, from healthcare to engineering. The utility lies in their ability to translate large amounts of data into easily understandable formats, such as graphs, tables, and numerical measures, thereby transforming raw data into insightful information. In research, they often serve as the initial step in the process of data analytics, giving researchers a snapshot of what the data looks like before delving into more complex analytical techniques like inferential statistics or machine learning algorithms.

If a researcher's interest lies in examining how variables change together without intending to make predictive inferences, they should utilize descriptive correlational analysis. This type of analysis explores the relationship between variables using correlation coefficients, without extending to prediction.

## Measures of Central Tendency

To capture the central tendency or the "average" experience within a set of data, calculating the mean is most appropriate. The mean provides a single value summarizing the central point of a dataset's distribution.


### Load data {.unnumbered}
```r
# Load the packages
library(tidyverse)
library(data.table)

options(scipen=999)

# Import the datasets
spotify_songs <- fread("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-01-21/spotify_songs.csv")
movies <- fread("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-03-09/movies.csv")
```

### Mean {.unnumbered}

The mean is perhaps the most widely recognized measure of central tendency, representing the arithmetic average of a dataset. In descriptive analysis, the mean serves as a fundamental measure, providing an average value that represents the central tendency of a dataset. This average is calculated by summing all observations and dividing by the number of observations. The mean is sensitive to outliers, which can disproportionately influence the calculated average, potentially resulting in a misleading representation of central location (McClave, Benson, & Sincich, 2011). Despite this limitation, the mean is highly useful in various statistical methods, including regression analysis and hypothesis testing, because of its mathematical properties (Field, Miles, & Field, 2012).

Importantly, the mean can be categorized into different types: arithmetic mean, geometric mean, and harmonic mean, each with specific applications depending on the nature of the data and the intended analysis (Triola, 2018). For instance, the geometric mean is often used when dealing with data that exhibit exponential growth or decline, such as in financial or biological contexts.

Descriptive statistics are most commonly paired with visualizations to provide clarity. For example, a scatterplot is an invaluable tool in descriptive analysis when the objective is to illustrate the relationship or correlation between two variables. It visually represents the data points for each observed pair, facilitating the detection of patterns or relationships.

**Example using Spotify Songs Dataset**: To find the mean popularity of songs.

The R code provided demonstrates the use of the `dplyr` package and base R functions to calculate the mean popularity of tracks in the `spotify_songs` dataset. Let's break down the code and its output:

1.  **dplyr summarise function**:

```r
mean_popularity <- spotify_songs %>%
  summarise(mean_popularity = mean(track_popularity, na.rm = TRUE))
```

This snippet uses the `dplyr` package's `summarise` function to calculate the mean of the `track_popularity` variable in the `spotify_songs` dataframe. The `mean` function is used with the `na.rm = TRUE` argument, which means that it will ignore `NA` (missing) values in the calculation. The result is stored in a new dataframe `mean_popularity`.

2.  **Output Explanation**:

```r
mean_popularity
```

This output indicates that the mean popularity score of the tracks in the dataset is approximately 42.47708. The `<dbl>` notation suggests that the mean popularity score is a double-precision floating-point number, which is a common way of representing decimal numbers in R.

In summary, both methods are used to calculate the average popularity score of tracks in the `spotify_songs` dataset. The output shows the mean value as approximately 42.47708, reflecting the average popularity of the tracks in the dataset. The use of `dplyr` and base R functions provides a means to cross-validate the result for accuracy.

### Median {.unnumbered}

The median serves as another measure of central tendency and is less sensitive to outliers compared to the mean. It is defined as the middle value in a dataset that has been arranged in ascending order. If the dataset contains an even number of observations, the median is calculated as the average of the two middle numbers. Medians are particularly useful for data that are skewed or contain outliers, as they provide a more "resistant" measure of the data's central location.

In addition to its robustness against outliers, the median is often used in non-parametric statistical tests like the Mann-Whitney U test and the Kruskal-Wallis test. These tests do not assume that the data follow a specific distribution, making the median an invaluable asset in such scenarios (Siegel & Castellan, 1988).

**Example using Movies Dataset**: To find the median budget of movies.

The provided R code calculates the median budget of movies in the `movies` dataset, with two different approaches, and the results are displayed. Let's analyze the code and its outputs:

1.  **Using dplyr's summarise function**:

```r
median_budget <- movies %>%
  summarise(median_budget = median(budget/1000000, na.rm = TRUE))
```

This snippet uses the `dplyr` package's `summarise` function to compute the median of the `budget` variable in the `movies` dataframe. Before calculating the median, each budget value is divided by 1,000,000 (`budget/1000000`), effectively converting the budget values from (presumably) dollars to millions of dollars. The `na.rm = TRUE` argument in the `median` function indicates that any `NA` (missing) values should be ignored in the calculation. The result is stored in a new dataframe called `median_budget`.

2.  **Output Explanation**:

```r
median_budget
```

This indicates that the median budget of the movies, in millions of dollars, is 28. The `<dbl>` notation signifies that the median budget is a double-precision floating-point number.

In conclusion, both methods are used to calculate the median budget of movies in the dataset, and both approaches confirm that the median budget is 28 million dollars. The use of both `dplyr` and base R functions serves as a cross-verification to ensure the accuracy of the result.

### Mode {.unnumbered}

The mode refers to the value or values that appear most frequently in a dataset. A dataset can be unimodal, having one mode; bimodal, having two modes; or multimodal, having multiple modes. While the mode is less commonly used than the mean and median for numerical data, it is the primary measure of central tendency for categorical or nominal data.

Despite its less frequent application in numerical contexts, the mode can still be useful for identifying the most common values in a dataset and for understanding the general distribution of the data. For example, in market research, knowing the mode of a dataset related to consumer preferences can provide valuable insights into what most consumers are likely to choose.

**Example using Spotify Songs Dataset**: To find the mode of the `playlist_genre`.

The provided R code calculates the mode of the `playlist_genre` variable in the `spotify_songs` dataset using the `Mode` function from the `DescTools` package. The mode is the value that appears most frequently in a dataset. Let's break down the code and its output:

1.  **Using the DescTools package's Mode function**:

```r
library(DescTools)

mode_genre <- Mode(spotify_songs$playlist_genre)
```

This snippet uses the `Mode` function from the `DescTools` package to find the most frequently occurring genre in the `playlist_genre` column of the `spotify_songs` dataset. The result is stored in the variable `mode_genre`.

2.  **Output Explanation**:

```r
mode_genre
```

This output indicates that the most common genre (mode) in the `playlist_genre` column is "edm". The `attr(,"freq")` part shows the frequency of this mode, which is 6043. This means that "edm" appears 6043 times in the `playlist_genre` column, more than any other genre.

In summary, the code calculates and displays the mode of the `playlist_genre` variable in the `spotify_songs` dataset, indicating that the most common genre is "edm", which appears 6043 times. The consistency of the results from both methods demonstrates the reliability of the calculation.

## Measures of Dispersion

### Range {.unnumbered}

The range is the simplest measure of dispersion, calculated by subtracting the smallest value from the largest value in the dataset. While straightforward to compute, the range is highly sensitive to outliers and does not account for how the rest of the values in the dataset are distributed.

The range offers a quick, albeit crude, estimate of the dataset's variability. It is often used in conjunction with other measures of dispersion for a more comprehensive understanding of data spread. Despite its limitations, the range can be helpful in initial exploratory analyses to quickly identify the scope of the data and to detect possible outliers or data entry errors.

**Example using Movies Dataset**: To find the range of movie budgets.

The R code provided calculates the range of the `budget` column in the `movies` dataset using the `dplyr` package. The range is a measure of dispersion that represents the difference between the maximum and minimum values in a dataset. Here's a breakdown of the code and its output:

1.  **Code Explanation**:

```r
budget_range <- movies %>%
  summarise(Range = max(budget/1000000, 
                        na.rm = TRUE) - min(budget/1000000,
                                            na.rm = TRUE))
```

-   `movies %>%`: This part indicates that the code is using the `movies` dataframe and piping (`%>%`) it into subsequent operations.

-   `summarise(Range = ...)`: The `summarise` function from the `dplyr` package is used to compute a summary statistic. Here, it's creating a new variable named `Range`.

-   `max(budget/1000000, na.rm = TRUE) - min(budget/1000000, na.rm = TRUE)`: This calculates the range of the movie budgets. Each `budget` value is first divided by 1,000,000 (presumably converting the budget from dollars to millions of dollars). The `max` function finds the maximum value and `min` finds the minimum value, with `na.rm = TRUE` indicating that any `NA` (missing) values should be ignored. The range is the difference between these two values.

    **Output Explanation**:

```r
budget_range
```

-   The output shows that the calculated range of the movie budgets, in millions of dollars, is approximately 424.993. This means that the largest budget in the dataset exceeds the smallest budget by about 424.993 million dollars.
-   The `<dbl>` notation indicates that the calculated range is a double-precision floating-point number, a standard numeric type in R for representing decimal values.

In summary, the code calculates the range of movie budgets in the `movies` dataset and finds that the budgets span approximately 424.993 million dollars, from the smallest to the largest. This provides a sense of how varied the movie budgets are in the dataset.

### Standard Deviation {.unnumbered}

The standard deviation is a more sophisticated measure of dispersion that indicates how much individual data points deviate from the mean (Lind et al., 2012). Standard deviation is a measure in descriptive analysis that quantifies the variation or dispersion of a set of data values. It reflects how much individual data points differ from the mean, indicating the dataset’s spread. Calculated as the square root of the variance, the standard deviation provides an intuitive sense of the data's spread since it is in the same unit as the original data points. It plays a crucial role in various statistical analyses, including hypothesis testing and confidence interval estimation, and is fundamental in fields ranging from finance to natural sciences.

The standard deviation can be classified into two types: population standard deviation and sample standard deviation. The former is used when the data represent an entire population, while the latter is used for sample data and is calculated with a slight adjustment to account for sample bias (Kenney & Keeping, 1962).

**Example using Spotify Songs Dataset**: To find the standard deviation of `danceability`.

The R code you've provided calculates the standard deviation of the `danceability` variable in the `spotify_songs` dataset using the `dplyr` package. Let's break down the code and its output:

1.  **Code Explanation**:

```r
std_danceability <- spotify_songs %>%
  summarise(std_danceability = sd(danceability, na.rm = TRUE))
```

-   `spotify_songs %>%`: This part uses the `spotify_songs` dataframe and pipes it into the subsequent operation using `%>%`.
-   `summarise(std_danceability = ...)`: The `summarise` function from `dplyr` is used to compute a summary statistic. Here, it's creating a new variable named `std_danceability`.
-   `sd(danceability, na.rm = TRUE)`: This calculates the standard deviation of the `danceability` variable. The `sd` function computes the standard deviation, and `na.rm = TRUE` indicates that any `NA` (missing) values should be ignored in the calculation.

2.  **Output Explanation**:

```r
std_danceability
```

-   The output shows that the calculated standard deviation of the `danceability` scores in the `spotify_songs` dataset is approximately 0.1450853.
-   The `<dbl>` notation indicates that the result is a double-precision floating-point number, which is typical for numeric calculations in R.

The standard deviation is a measure of the amount of variation or dispersion in a set of values. A low standard deviation indicates that the values tend to be close to the mean (also called the expected value) of the set, while a high standard deviation indicates that the values are spread out over a wider range.

In this case, a standard deviation of approximately 0.1450853 for `danceability` suggests that the danceability scores in the `spotify_songs` dataset vary moderately around the mean. This gives an idea of the variability in danceability among the songs in the dataset.

### Variance {.unnumbered}

Variance is closely related to the standard deviation, essentially being its square. It quantifies how much individual data points in a dataset differ from the mean (Gravetter & Wallnau, 2016). Unlike the standard deviation, the variance is not in the same unit as the data, which can make it less intuitive to interpret. However, variance has essential mathematical properties that make it useful in statistical modeling and hypothesis testing (Moore, McCabe, & Craig, 2009).

In statistical theory, the concept of variance is pivotal for various analytical techniques, such as Analysis of Variance (ANOVA) and Principal Component Analysis (PCA). Variance allows for the decomposition of data into explained and unexplained components, serving as a key element in understanding data variability in greater depth.

**Example using Movies Dataset**: To find the variance in IMDB ratings.

The R code you've shared calculates the variance of the `imdb_rating` variable in the `movies` dataset using the `dplyr` package. Let's examine the code and its output:

1.  **Code Explanation**:

```r
var_imdb_rating <- movies %>%
  summarise(var_imdb_rating = var(imdb_rating, na.rm = TRUE))
```

-   `movies %>%`: This line uses the `movies` dataframe and pipes it into the following operation with `%>%`.
-   `summarise(var_imdb_rating = ...)`: The `summarise` function from `dplyr` is employed to compute a summary statistic, in this case, creating a new variable called `var_imdb_rating`.
-   `var(imdb_rating, na.rm = TRUE)`: This computes the variance of the `imdb_rating` variable. The `var` function calculates the variance, and `na.rm = TRUE` indicates that any `NA` (missing) values should be excluded from the calculation.

2.  **Output Explanation**:

```r
var_imdb_rating
```

-   The output indicates that the variance of the IMDb ratings in the `movies` dataset is approximately 0.9269498.
-   The `<dbl>` notation signifies that the result is a double-precision floating-point number, which is a standard numeric format in R.

Variance is a statistical measure that describes the spread of numbers in a data set. More specifically, it measures how far each number in the set is from the mean and thus from every other number in the set. In this context, a variance of approximately 0.9269498 in IMDb ratings suggests the degree to which these ratings vary from their average value in the dataset.

This measure of variance can be particularly useful for understanding the consistency of movie ratings; a lower variance would indicate that the ratings are generally close to the mean, suggesting agreement among raters, whereas a higher variance would imply more diverse opinions on movie ratings.

## General Summary

There are also a couple methods for getting multiple basic descriptive statistics with a single code. The most common of these is the `summary()` function. There is also a package called `skimr`.

### `summary()` {.unnumbered}

The R code snippet you provided uses the `summary()` function to generate descriptive statistics for the `imdb_rating` variable in the `movies` dataset. The `summary()` function in R provides a quick, five-number summary of the given data along with the count of `NA` (missing) values. Let's break down the output:

```r
summary(movies$imdb_rating)
```

-   **Min. (Minimum)**: The smallest value in the `imdb_rating` data. Here, the minimum IMDb rating is 2.10.
-   **1st Qu. (First Quartile)**: Also known as the lower quartile, it is the median of the lower half of the dataset. This value is 6.20, meaning 25% of the ratings are below this value.
-   **Median**: The middle value when the data is sorted in ascending order. The median IMDb rating is 6.80, indicating that half of the movies have a rating below 6.80 and the other half have a rating above 6.80.
-   **Mean**: The average of the `imdb_rating` values. Calculated as the sum of all ratings divided by the number of non-missing ratings. The mean rating is 6.76.
-   **3rd Qu. (Third Quartile)**: Also known as the upper quartile, it is the median of the upper half of the dataset. Here, 75% of the movies have a rating below 7.40.
-   **Max. (Maximum)**: The largest value in the `imdb_rating` data. The highest IMDb rating in the dataset is 9.30.
-   **NA's**: The number of missing values in the `imdb_rating` data. There are 202 missing values.

This summary provides a comprehensive view of the distribution of IMDb ratings in the `movies` dataset, including the central tendency (mean, median), spread (minimum, first quartile, third quartile, maximum), and the count of missing values. It helps in understanding the overall rating landscape of the movies in the dataset.

### `skimr` {.unnumbered}

The R code snippet provided uses the `skim()` function from the `skimr` package to generate a summary of the `imdb_rating` variable from the `movies` dataset. The `skimr` package provides a more detailed summary than the base R `summary()` function, particularly useful for initial exploratory data analysis.

```r
library(skimr)

skim(movies$imdb_rating)
```

Let's break down the output:

1.  **Data Summary Section**:
    -   **Name**: Identifies the data being summarized, here `movies$imdb_rating`.
    -   **Number of rows**: Indicates the total number of entries in the dataset, which is 1794 for `imdb_rating`.
    -   **Number of columns**: The number of variables or columns in the data being skimmed. Since `skim()` is applied to a single column, this is 1.
    -   **Column type frequency**: Shows the types of data present in the columns. Here, there is 1 numeric column.
2.  **Detailed Statistics Section**:
    -   **skim_variable**: A character representation of the variable being summarized.
    -   **n_missing**: The number of missing (`NA`) values in the dataset. Here, there are 202 missing ratings.
    -   **complete_rate**: Proportion of non-missing values. Calculated as `(Total Number of rows - n_missing) / Total Number of rows`. For `imdb_rating`, it's approximately 0.8874025.
    -   **mean**: The average of the `imdb_rating` values, which is 6.760113.
    -   **sd (standard deviation)**: Measures the amount of variation or dispersion in `imdb_rating`. Here, it is 0.9627823.
    -   **p0, p25, p50, p75, p100**: These represent the percentiles of the data:
    -   **p0**: The minimum value (0th percentile), which is 2.1.
    -   **p25**: The 25th percentile, meaning 25% of the data fall below this value, which is 6.2.
    -   **p50**: The median or 50th percentile, which is 6.8.
    -   **p75**: The 75th percentile, meaning 75% of the data fall below this value, which is 7.4.
    -   **p100**: The maximum value (100th percentile), which is 9.3.
    -   **hist**: A text-based histogram providing a visual representation of the distribution of `imdb_rating`. The characters (▁▁▅▇▂) represent different frequency bins.

In summary, the `skim()` function output provides a detailed statistical summary of the `imdb_rating` variable, including measures of central tendency, dispersion, and data completeness, along with a visual histogram for quick assessment of the data distribution. This information is crucial for understanding the characteristics of the IMDb ratings in the `movies` dataset, especially when preparing for more detailed data analysis.


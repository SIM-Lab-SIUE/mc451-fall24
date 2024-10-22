# Descriptive Analysis

## Measures of Central Tendency

Central tendency is a fundamental concept in descriptive statistics, representing the "center" or "typical" value of a dataset. It provides a single value that summarizes the data and helps us understand its overall distribution. The three primary measures of central tendency are the **mean**, **median**, and **mode**. Each measure has its strengths and weaknesses, depending on the nature of the data and the research question at hand.

In mass communication research, we often use these measures to summarize key data points such as viewer ratings, playtime, episode counts, or even specific word frequencies in media content. By understanding the different measures of central tendency, researchers can more effectively interpret the underlying patterns in their data sets.

**Load data for chapter**

``` r
library(data.table)

anime <- fread("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-04-23/tidy_anime.csv")

horror_movies <- fread('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2022/2022-11-01/horror_movies.csv')

richmondway <- fread('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2023/2023-09-26/richmondway.csv')

television <- fread("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-01-08/IMDb_Economist_tv_ratings.csv")

video_games <- fread("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-07-30/video_games.csv")
```

You can access the data descriptions for each of these data sets on their respective TidyTuesday page.

1.  [Anime Dataset](https://github.com/rfordatascience/tidytuesday/blob/master/data/2019/2019-04-23/readme.md)
2.  [Horror Movies](https://github.com/rfordatascience/tidytuesday/blob/master/data/2022/2022-11-01/readme.md)
3.  [Roy Kent F\*\*k count](https://github.com/rfordatascience/tidytuesday/blob/master/data/2023/2023-09-26/readme.md)
4.  [TV's golden age is real](https://github.com/rfordatascience/tidytuesday/blob/master/data/2019/2019-01-08/readme.md)
5.  [Video Games Dataset](https://github.com/rfordatascience/tidytuesday/blob/master/data/2019/2019-07-30//readme.md)

### Mean (Arithmetic Average) {.unnumbered}

The **mean** is the sum of all values in a dataset divided by the number of values. It provides the "average" value of the dataset and is widely used due to its simplicity and ease of interpretation. However, the mean is **sensitive to outliers**, which means that unusually high or low values can significantly skew the result.

#### Why the Mean Is Useful {.unnumbered}

The mean gives a straightforward snapshot of the dataset’s central point and is especially useful for **interval** or **ratio data** where the numbers have a true, meaningful order. In mass communication research, you might use the mean to calculate average viewer ratings for a television show or the average playtime for a video game. However, be mindful that a few extreme values (outliers) can heavily influence the mean, sometimes making it less representative of the data as a whole.

In the **horror_movies** dataset, we have a variable called `vote_average`, which represents the average rating for each movie. To calculate the mean of this variable in R:

``` r
# Calculate the mean vote average
mean_vote_avg <- mean(horror_movies$vote_average, na.rm = TRUE)
mean_vote_avg
```

This will give you the overall average rating across all horror movies in the dataset, helping you understand whether audiences generally liked or disliked these films.

In the **video_games** dataset, the `average_playtime` variable represents the average time people spend playing a particular game. To calculate the mean playtime:

``` r
# Calculate the mean average playtime
mean_playtime <- mean(video_games$average_playtime, na.rm = TRUE)
mean_playtime
```

The result will show you the typical playtime across all games, offering insights into how long players typically engage with video games.

### Median {.unnumbered}

The **median** is the middle value of a dataset when it is ordered from least to greatest. Unlike the mean, the median is **resistant to outliers**, making it a more accurate measure of central tendency when the dataset contains extreme values. The median is especially useful for **ordinal**, **interval**, and **ratio data**, where the order of values matters.

#### Why the Median Is Useful {.unnumbered}

The median provides a more robust measure of central tendency than the mean in cases where the dataset is **skewed** or contains outliers. In mass communication research, for instance, if you are studying the number of episodes in different anime series, a few long-running shows could inflate the mean, making it less representative of the typical number of episodes. In such cases, the median offers a better "typical" value.

In the **anime** dataset, the `episodes` variable tells us how many episodes each anime has. To calculate the median number of episodes:

``` r
# Calculate the median number of episodes
median_episodes <- median(anime$episodes, na.rm = TRUE)
median_episodes
```

This result will show you the middle value of episode counts, giving you a clearer picture of the typical length of anime series without being skewed by a few extremely long shows.

In the **video_games** dataset, the `median_playtime` variable represents the middle value of playtime for each game. To calculate the median:

``` r
# Calculate the median playtime
median_playtime <- median(video_games$median_playtime, na.rm = TRUE)
median_playtime
```

This will give you the typical amount of time people spend playing a game, without being skewed by extremely high or low playtimes.

### Mode {.unnumbered}

The **mode** is the value that appears most frequently in a dataset. It is the only measure of central tendency that can be used with **nominal data**, which have no numerical or ordered relationship (e.g., genres or titles). The mode is also useful for **categorical** or **discrete** data where you want to identify the most common category or value.

#### Why the Mode Is Useful {.unnumbered}

The mode highlights the most common occurrence in the data and is particularly valuable when analyzing **qualitative data** or data with repeating values. For instance, in mass communication, if you're analyzing the genres of horror movies, knowing the most frequently occurring genre gives insights into what type of horror movie is most commonly produced. Similarly, finding the most common score for anime users provides an indication of how people generally rate their anime experiences.

In the **horror_movies** dataset, the `genre_names` variable contains the genres of each movie. To find the most common genre (the mode):

``` r
# Calculate the mode for genre names
mode_genre <- horror_movies$genre_names[which.max(table(horror_movies$genre_names))]
mode_genre
```

This will tell you which genre appears most frequently in the dataset, helping you understand the dominant themes in horror films.

In the **anime** dataset, the `score` variable represents how users rate different anime. To find the most common score:

``` r
# Calculate the mode for anime score
mode_score <- anime$score[which.max(table(anime$score))]
mode_score
```

This will provide the most frequent user score, offering insight into how anime viewers typically rate their experiences.

### Comparing Mean, Median, and Mode {.unnumbered}

Understanding when to use each measure of central tendency is crucial in descriptive statistics. Here’s a general guideline:

-   **Mean**: Use when you want to calculate the average of **interval** or **ratio data** and the data are **not skewed** by outliers. It’s best for normally distributed data.
-   **Median**: Use when your data are **skewed** or when you are dealing with **ordinal**, **interval**, or **ratio data** that have extreme values or outliers.
-   **Mode**: Use when you are working with **nominal** or **categorical data**, or when you want to know the most frequently occurring value in your dataset.

Each of these measures offers a different perspective on the data, and the appropriate measure depends on the research question and the type of data you're analyzing. By mastering these concepts, you’ll be better equipped to summarize and interpret data in mass communication research, whether you're studying anime ratings, horror movie genres, or video game playtimes.

Here is a detailed, pedagogically focused draft for the **Measures of Dispersion** section, following the same format as the earlier section on Measures of Central Tendency. This section will explain key concepts related to dispersion, providing R examples using the datasets you've provided.

## Measures of Dispersion

While measures of central tendency (mean, median, mode) summarize the central point of a dataset, they do not tell the whole story. **Measures of dispersion** help us understand how spread out or variable the data are around the central point. In mass communication research, understanding data variability is essential for accurately interpreting audience behaviors, ratings, or playtimes. Common measures of dispersion include the **range**, **variance**, **standard deviation**, and **interquartile range** (IQR).

Dispersion gives insights into the consistency or variability of the data. For instance, two TV shows may both have a mean rating of 8/10, but one may have ratings clustered tightly around that mean, while the other has ratings ranging from 2 to 10. Measures of dispersion can help identify such differences.

### Range {.unnumbered}

The **range** is the simplest measure of dispersion, calculated as the difference between the largest and smallest values in a dataset. It gives a rough estimate of how spread out the values are, but it is sensitive to outliers, as just one extreme value can drastically increase the range.

#### Why the Range Is Useful {.unnumbered}

The range gives a quick overview of how widely the data points vary. In mass communication research, the range can show how ratings, playtimes, or other numerical measures differ between the highest and lowest values.

In the **anime** dataset, the `score` variable represents user ratings for different anime. To calculate the range of scores:

``` r
# Calculate the range of anime scores
range_anime_score <- range(anime$score, na.rm = TRUE)
range_anime_score
```

This will provide the minimum and maximum anime scores, showing how spread out the ratings are across the dataset.

In the **video_games** dataset, we can calculate the range of average playtime (`average_playtime`):

``` r
# Calculate the range of average playtime
range_playtime <- range(video_games$average_playtime, na.rm = TRUE)
range_playtime
```

This result will show how the shortest and longest playtimes compare, giving an initial sense of variability.

### Variance {.unnumbered}

**Variance** measures the average squared deviation of each data point from the mean. It gives a sense of how much the values in a dataset vary. A high variance means the data points are spread out from the mean, while a low variance indicates that they are clustered closely around the mean.

#### Why Variance Is Useful {.unnumbered}

Variance is important in mass communication research because it quantifies variability. For instance, understanding the variance in TV show ratings can indicate whether viewers generally agree on the quality of a show or whether their opinions vary widely.

In the **horror_movies** dataset, the `vote_average` variable represents movie ratings. To calculate the variance of movie ratings:

``` r
# Calculate the variance of horror movie ratings
var_vote_avg <- var(horror_movies$vote_average, na.rm = TRUE)
var_vote_avg
```

This result shows how much individual ratings differ from the average rating.

### Standard Deviation {.unnumbered}

The **standard deviation** is the square root of the variance and is one of the most commonly used measures of dispersion. It has the advantage of being in the same units as the data itself (unlike variance, which is in squared units). A low standard deviation means that the data points are close to the mean, while a high standard deviation indicates that the data points are more spread out.

#### Why Standard Deviation Is Useful {.unnumbered}

Standard deviation is often used in mass communication research to understand the consistency of data. For example, if we want to know how consistently users rate anime, the standard deviation of their ratings can provide that information.

In the **anime** dataset, we can calculate the standard deviation of user ratings (`score`):

``` r
# Calculate the standard deviation of anime scores
sd_anime_score <- sd(anime$score, na.rm = TRUE)
sd_anime_score
```

This result shows how much anime scores deviate from the average score, offering insights into whether most users tend to agree on ratings or whether opinions are more varied.

In the **video_games** dataset, we can also calculate the standard deviation of playtime (`average_playtime`):

``` r
# Calculate the standard deviation of average playtime
sd_playtime <- sd(video_games$average_playtime, na.rm = TRUE)
sd_playtime
```

This standard deviation will show how consistent playtimes are across different video games, providing insights into whether users typically engage with games for similar amounts of time or whether there’s significant variation.

### Interquartile Range (IQR) {.unnumbered}

The **interquartile range (IQR)** measures the range of the middle 50% of values in a dataset, and is calculated as the difference between the third quartile (Q3) and the first quartile (Q1). It is particularly useful for understanding the spread of the central portion of the data and is less sensitive to outliers than the range.

#### Why the IQR Is Useful {.unnumbered}

The IQR is useful in identifying the spread of the "typical" data, excluding outliers. It’s especially important in skewed datasets, where the mean and standard deviation might not give an accurate picture of variability.

In the **horror_movies** dataset, we can calculate the IQR for movie ratings (`vote_average`):

``` r
# Calculate the IQR for horror movie ratings
iqr_vote_avg <- IQR(horror_movies$vote_average, na.rm = TRUE)
iqr_vote_avg
```

This will provide the range of the middle 50% of movie ratings, helping us understand the typical spread of ratings without the influence of extreme values.

In the **video_games** dataset, we can calculate the IQR for average playtime (`average_playtime`):

``` r
# Calculate the IQR for average playtime
iqr_playtime <- IQR(video_games$average_playtime, na.rm = TRUE)
iqr_playtime
```

This value shows how playtimes are distributed for the central 50% of video games, helping to identify whether most games have a similar playtime or if there’s a large variance.

### Understanding Dispersion in Media Data {.unnumbered}

In summary, measures of dispersion are critical in understanding the variability within datasets. They provide insights beyond the central tendency, helping researchers determine the spread and consistency of values. Here’s how these measures can be applied in mass communication research:

-   **Range**: Offers a basic view of variability but is sensitive to outliers.
    -   Example: Calculating the range of anime scores or playtimes in video games.
-   **Variance**: Provides a more nuanced understanding of variability by measuring the average squared deviations from the mean.
    -   Example: Analyzing the variance in movie ratings to assess how much opinions vary.
-   **Standard Deviation**: A more interpretable measure than variance, showing how much values deviate from the mean in the original units of the data.
    -   Example: Understanding the consistency of anime ratings or playtime durations.
-   **Interquartile Range (IQR)**: Focuses on the spread of the middle 50% of the data, excluding outliers.
    -   Example: Examining the IQR of horror movie ratings to get a clearer picture of typical audience sentiment.

By learning and applying these measures of dispersion, students will gain a deeper understanding of how data behaves and how to interpret variability in mass communication datasets.

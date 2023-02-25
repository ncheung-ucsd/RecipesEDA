# Recipe and Ratings

### Introduction and Question Identification

This dataset includes recipes and ratings from the website [food.com](https://www.food.com). The question that the analysis will be centered around is: **What recipes tend to be lower in calories?**This question is important because understanding what types of recipes tend to be lower in calories can help individuals identify healthier food choices.

The original raw datasets include one for recipes, `RAW_interactions.csv`, and one for ratings, `RAW_ratings.csv`. `RAW_interactions.csv` has 83782 rows of data, and `RAW_interactions.csv` has 731927 rows of data. The relevant columns for this analysis are: `nutrition`, `n_steps`, `n_ingredients`, `rating`, and `review`. `nutrition` is the nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”. `n_steps` is the number of steps in the recipe. `n_ingredients` is the number of ingredients in the recipe. `rating` is the rating given. `review` is the review text.

### Data Cleaning

The first step taken was to left merge the two datasets together. This was done to explore potential relationships between the number of calories in a recipe and the ratings those recipes received. The next step was to fill all ratings of 0 with `np.nan`. This was done because zeroes in the dataset indicated that the values were missing, not that the user gave the recipe a rating of 0, since the lowest possible rating a user can give is 1. Thus, `np.nan` is a better representation of the value. The next step was to add the average rating per recipe back to `RAW_recipes`. This was to aggregate each pair of recipe and rating of a given recipe into one row, so that each recipe only had one row. The next step was splitting the `nutrition` column into
One row for every recipe, merged has one row for every pair of recipe and rating for a recipe. This was done so that analysis can be done on the relationships between the number of calories and individual nutrients. The average ratings were also rounded, so that the rating could be represented as a categorical variable for each recipe, just as it appeared on the original `RAW_interactions.csv` dataset.

Below is the first few rows the dataframe. Note that the `tags`, `steps`, `description`, `ingredients`, `review` columns have been omitted because they were not used in the analysis and contained text that made the table format difficult to read.

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>n_steps</th>
      <th>n_ingredients</th>
      <th>rating</th>
      <th>calories (#)</th>
      <th>total fat (PDV)</th>
      <th>sugar (PDV)</th>
      <th>sodium (PDV)</th>
      <th>protein (PDV)</th>
      <th>saturated fat (PDV)</th>
      <th>carbohydrates (PDV)</th>
      <th>rating_rounded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>10</td>
      <td>9</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>10.0</td>
      <td>50.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>6.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>12</td>
      <td>11</td>
      <td>5.0</td>
      <td>595.1</td>
      <td>46.0</td>
      <td>211.0</td>
      <td>22.0</td>
      <td>13.0</td>
      <td>51.0</td>
      <td>26.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>6</td>
      <td>9</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>millionaire pound cake</td>
      <td>286009</td>
      <td>120</td>
      <td>461724</td>
      <td>2008-02-12</td>
      <td>7</td>
      <td>7</td>
      <td>5.0</td>
      <td>878.3</td>
      <td>63.0</td>
      <td>326.0</td>
      <td>13.0</td>
      <td>20.0</td>
      <td>123.0</td>
      <td>39.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>2000 meatloaf</td>
      <td>475785</td>
      <td>90</td>
      <td>2202916</td>
      <td>2012-03-06</td>
      <td>17</td>
      <td>13</td>
      <td>5.0</td>
      <td>267.0</td>
      <td>30.0</td>
      <td>12.0</td>
      <td>12.0</td>
      <td>29.0</td>
      <td>48.0</td>
      <td>2.0</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>

### Univariate Analysis

<iframe src="assets/file-name.html" width=800 height=600 frameBorder=0></iframe>

This is the distirbution of the 99th quantile of the `calories (#)`, which shows that the distribution is heavily skewed right. Note that only data from the 99th quantile is shown to improve readability, and the red line indicates the mean of the distribution.

### Bivariate Analysis

<iframe src="assets/file-name.html" width=800 height=600 frameBorder=0></iframe>

This is the distirbution of the 99th quantile of the `calories (#)`, separated by the rounded average rating; note that only the 99th quantile of `calories (#)` is shown for readability. The graph shows that as rating increases, the median calories also generally increases, with a rating of 1 having the lowest median rating; also it shows that there are many outliers for each rating.

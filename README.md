# Recipe and Ratings

### Introduction and Question Identification

This dataset includes recipes and ratings from the website [food.com](https://www.food.com). The question that the analysis will be centered around is: **What recipes tend to be lower in calories?**This question is important because understanding what types of recipes tend to be lower in calories can help individuals identify healthier food choices.

The original raw datasets include one for recipes, `RAW_interactions.csv`, and one for ratings, `RAW_ratings.csv`. `RAW_interactions.csv` has 83782 rows of data, and `RAW_interactions.csv` has 731927 rows of data. The relevant columns for this analysis are: `nutrition`, `n_steps`, `n_ingredients`, `rating`, and `review`. `nutrition` is the nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”. `n_steps` is the number of steps in the recipe. `n_ingredients` is the number of ingredients in the recipe. `rating` is the rating given. `review` is the review text.

### Data Cleaning

The first step taken was to left merge the two datasets together. This was done to explore potential relationships between the number of calories in a recipe and the ratings those recipes received. The next step was to fill all ratings of 0 with `np.nan`. This was done because zeroes in the dataset indicated that the values were missing, not that the user gave the recipe a rating of 0, since the lowest possible rating a user can give is 1. Thus, `np.nan` is a better representation of the value. The next step was to add the average rating per recipe back to `RAW_recipes`. This was to aggregate each pair of recipe and rating of a given recipe into one row, so that each recipe only had one row. The next step was splitting the `nutrition` column into
One row for every recipe, merged has one row for every pair of recipe and rating for a recipe. This was done so that analysis can be done on the relationships between the number of calories and individual nutrients. The average ratings were also rounded, so that the rating could be represented as a categorical variable for each recipe, just as it appeared on the original `RAW_interactions.csv` dataset.

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>n_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>rating</th>
      <th>review</th>
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
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']</td>
      <td>10</td>
      <td>['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']</td>
      <td>these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!</td>
      <td>['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']</td>
      <td>9</td>
      <td>4.0</td>
      <td>Nice variation on boiled new potatoes.  Love the contrast of the crunchy walnuts and soft potatoes.  I goofed and didn't brown the potatoes enough, but still very tasty and went well with a roast turkey.  Made for Fall 2008 PAC.</td>
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
      <td>['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']</td>
      <td>12</td>
      <td>['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft &amp; chewy in the center', 'serve hot and enjoy !']</td>
      <td>this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.</td>
      <td>['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']</td>
      <td>11</td>
      <td>5.0</td>
      <td>This was very refreshing on a hot day! This drink is very easy to vary to personal taste- personally I found the chocolate too strong and the coffee too weak so would change the amounts of those next time. Thanks for this lovely diet recipe!</td>
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
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>5.0</td>
      <td>Yummy!  I made this for supper last night and it was delicious.  I had a single pie crust that's been hanging out in my freezer for far too long, so I did a single crust pot pie just to use it up...but i would have preferred it to have a top crust as well to get more crust in each bite!  I did sprinkle my serving with some salt -- it seemed to brighten up the flavors and bring them out more.  This was also very easy to put together...something I always like in a meal!  Thanks so much for posting!  Made for Please Review My Recipe Tag.</td>
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
      <td>['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less']</td>
      <td>7</td>
      <td>['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']</td>
      <td>why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.</td>
      <td>['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']</td>
      <td>7</td>
      <td>5.0</td>
      <td>I found this site and tried this crust the day of a pie contest I was entering and I won the contest .This crust is super good.Can be tricky to make but it was well worth it .</td>
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
      <td>['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']</td>
      <td>17</td>
      <td>['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf']</td>
      <td>ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.</td>
      <td>['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil']</td>
      <td>13</td>
      <td>5.0</td>
      <td>How do you explain that this identical recipe was published in the Dallas Morning News by Kim Pierce the day before you posted it here? You say you developed this recipe, but the following article states the true origin of this recipe: http://www.dallasnews.com/sharedcontent/dws/fea/taste/easyrecipes/stories/DN-nf_bacon_0417liv.State.Edition1.3616f6d.html\r\n\r\nThese cookies are delicious, but...</td>
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

---
layout: post
title:      "Data Visualization"
date:       2020-05-07 13:04:08 -0400
permalink:  data_visualization
---


It's easy to focus on the number crunching part of data science-it's actually a thing I quite enjoy, and part of why I choose data science. I love the logical and mathematical parts! However, it's important to also remember the fundamental goal, which is to be able to communicate the findings that can be drawn from the numbers.
<br><br>
We started learning about visualizations using the matplotlib library, and quickly added Seaborn to the toolbox. Seaborn can give a pretty good visual just from putting in the data! While the end goal for a visualization might be to share the well-formatted results in a presentation, having the ability to easily see comparisons of the data can also help guide where to focus our data analysis.
<br><br>
Before you can plot the data, you first have to clean the data. Datasets, especially large ones, are often imperfect-in particular, there will almost always be values that weren't collected for some number of points. When python reads these missing data points, it fills the relevant cell with a value called NaN, or not a number. NaNs cannot be plotted, and so most graphing interfaces will throw an error if they are not cleaned first. With pandas, it's easy to fill in these missing values, in order to make the data able to be plotted. It depends on the data set, but usually, the median is a good choice-a central value, and unlike the mean, is not going to be skewed by outliers. Here is the simple bit of code to fix these missing values:
<br><br>
`df['column_name'].fillna(df['column_name'].median(),inplace = True)`
<br><br>
For some data sets, before you can get a median value, it's important to make sure that values that should be numbers are registered as numbers. $2,400,00.00 is easy to read and understand as a number for a person, but a computer cannot combine the dollar signs and commas with a number and still understand it as a number. You have to strip the punctuation out, and then tell the program to check again that they are in fact numerical values. The relevant code is:
<br><br>
```
df['column_name'] = df['column_name'].apply(lambda x:x.replace('$','').replace(',','')
df['column_name']= pd.to_numeric(df['column_name'])
```
<br><br>
Once the computer knows it's looking at numbers and doesn't trip over any missing values, we can plot our data!
<br><br>
**Some common types of visualizations:**<br><br>
**Scatterplots** are very good for showing correlations and relationships between variables-for instance, how the budget of a movie can affect the revenue that movie makes. Each data point would be for one movie: one budget, one revenue. Scatterplots can be used to form models and thus make predictions: if we put X in, how much Y can we expect to get out of it?
<br><br>
![](https://sg9byg.ch.files.1drv.com/y4p-rNZYu4aK5ueuWe1RetiT71ZDsrOwvVUzoXIqqfrIK1R8rWsCS840dkGtiybCgRyRi8X6Xb1M2AIunYnOk9V0LXTcNSikkqwsnQoctbpeNcGDs5KVDPwSlSLu-szvsi3iw_mhwRJe94TeuTtBs5q7NvYxiLI7HXvBASGxpt3xgDVOVCVetqzoqhYeslf5_noh3UBbDvKHbcsqV6px0lIDQg1cQedLc91biskzatb4cg/scatter.png?psid=1)<br>
And after reading the data set into the notebook as tn_budgets_df, this plot was made with just one line of code:
`sns.scatterplot(x='production_budget',y='worldwide_gross',data=tn_budgets_df)`<br>
So wonderfully simple!
<br><br>
Another way to talk about correlation is the correlation coefficient, which is a numeric value that describes how strongly correlated two variables are. Scatterplots are a way to actually see what that correlation looks like in an intuitive way-which is especially important when sharing information with people who aren't data scientists. No one can really picture what a correlation coefficient means without graphing something, but at least technically trained people will have a logical understanding of it. But if you can't communicate the meaning of your data, then it won't do you any good!
<br><br>
It's easy to feel like a lack of correlation is a lack of a result, but knowing that two variables are unrelated is information in itself. Discovering that there is no pattern still means you have learned something about the data set.
<br><br>
**Barplots** are good for showing relationships between categories. Sometimes, the variable you want to change is not numeric, and thus cannot be plotted as a scatterplot. The following visual provides an easy way to see the difference in median revenue based on the genre of movie.<br>
![](https://sgpfqq.ch.files.1drv.com/y4pudbARnajoi2KgmI6qIf21YWUtkK0Dvt1hLk5MZVpj0yIWTShrnvf2B3VFjrP7ES1aiSWGS_K7sc_LdcoYnwm8vOpHHP2N1rhWt-9pyGyvwFz0SAsVp-Kt6bOt3LW4JLRZXCcSk-KCQl9PIW-Tt62qGnXM7JoUpNQ6ukYXhkeFCC1IMWvx0liTV8IcahgAZKc_EgU99eyoNw9vUFWKMlJGzwsIhtyR_ky2ObWtBOvoMU/bar.png?psid=1)
<br><br>

**Histograms** (and other kinds of distribution plots) are useful for visualizing how data is distributed: often, it has a shape like a bell, as there tend to be more points of data near a middling value, and only a few outliers. Histograms might look a bit like a bar plot, where each “category” is a range of values. Seaborn has a an easy to run method that plots both a histogram and a smoother distribution curve in one simple step!<br>
![](https://sgp7kg.ch.files.1drv.com/y4pc01JzDebDz76nZ_dXGoExDvgb8rXkFT09fOfXYk-2nB_r4k6D_n-aVR6vhJbEQ4UbNAlkI_XzGKai_ef0ODLTa1p1dQ79k1Pq8kzJw_8ZgpOoDio_0D0A8kMfNHYFUfIYoJmW3tvduB1PMf74D1NENHi7NH5GJkBk9X1M65bPrWhXuEwQzEcwy3Lob_PduqA1HpyvU_UYhZ0R6Lruz3ZUvaCCzp_SV-EwXbhrR1t_0Y/dist1.png?psid=1)<br>
That's a little hard to see, because outliers are making the x-axis much longer than is useful to see all of the data. Let's set a maximum value based on the inter-quartile range to improve visibility.
<br><br>
With just a few lines of code:
```
IQR = tn_budgets_df['worldwide_gross'].quantile(.75) - tn_budgets_df['worldwide_gross'].quantile(.25)
max_gross = tn_budgets_df['worldwide_gross'].median() + 1.5 * IQR
sns.distplot(tn_budgets_df.query('worldwide_gross < '+str(max_gross))['worldwide_gross'])
```
<br><br>
We get a much more readable graph:<br>
![](https://sg9wnw.ch.files.1drv.com/y4plseFMxmzxCxJ5W2Tg4b5fNkrHcs3ilL8oZz3iZYIV55nXFZmvNrmsNy3d7ZmCJ4KrAGWYA7y_O1Kq2gu7n2TJV1uY8YgY0ovLDaO8lftqzfkTSDu9T_3CWSIa8w7CuGEo2O_mmvA5Wp0LUFCVVVuOkf5sLUXhUt4-qjh3vRzK9t8nSQPFW7L8rzSy781iRzBpOQ8gjqmbtcGKiwx7jYPvUxMzt5GwsVtzoXxtyWBYiQ/dist2.png?psid=1)<br>
This graph is a good example of one thing humans are still much better at than machines: recognizing patterns. Computers can process thousands of numbers in the blink of an eye, but complex patterns escape it. A human can look a the histogram part of that graph (the boxy part, which more precisely shows where the data is) and see that there are no values less than zero. But the complex math that calculates the distribution curve treats it like there is, because of how the calculations work. While finding a way to plot this data where it can figure that out is easy enough, it's a reminder that it's important to always look over the data, and make sure the computer is running the calculations that you think it's running. Computers will always do exactly what you tell them to do, and not necessarily what you intend to tell them to do, if you don't specify something exactly the right way!
<br><br>
**Boxplots** show a simplified kind of a distribution plot, and are particularly useful as they can show multiple categories side by side.<br>
![](https://sg8gtg.ch.files.1drv.com/y4pk-xDfKHlD_a8kfP2v0lDWysAsrJgxqSbhljBCbPq2Vb0_JPKtNGh2Fy_amlxX00XMR49asJYXjSi_0wcIeB4ZcIrwk-HFcBAQ9E2ftRyncRWrvh1C9qLxi-9cz6GKzgb-yrzCAuyAJl18LhoaXnGQj1-1XmxAzvJBtX2F21YieeuGN3nHAj3Ch3yHlOXBcHfoLWdPM4cXaLSfgsTVXNiNrV3rAfr1lHXs-j8NXWvIxY/box.png?psid=1)
<br><br>
By creating visualizations, we can quickly get a sense for what the data can tell us. It can help take us from a spreadsheet full of numbers to an actionable recommendation or a specific understanding, which is the ultimate goal in processing and analyzing data.

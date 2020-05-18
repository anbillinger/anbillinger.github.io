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
![](https://lh3.googleusercontent.com/pw/ACtC-3dz5URwQUeA3OzeTfyp_oujlMazG_qUE-1xq_CxnvhtP3Sk-0NtNrb9dCRI-e5Rp7V6KHOuW3n3PpbsMHzS_mixfOw-mBH41VyYMSUqBqPv9q0zPz-5AjB59D0iu2iar_459RyvtiWqX1Na_I-1JNWN=w387-h274-no?authuser=0)<br>
And after reading the data set into the notebook as tn_budgets_df, this plot was made with just one line of code:
`sns.scatterplot(x='production_budget',y='worldwide_gross',data=tn_budgets_df)`<br>
So wonderfully simple!
<br><br>
Another way to talk about correlation is the correlation coefficient, which is a numeric value that describes how strongly correlated two variables are. Scatterplots are a way to actually see what that correlation looks like in an intuitive way-which is especially important when sharing information with people who aren't data scientists. No one can really picture what a correlation coefficient means without graphing something, but at least technically trained people will have a logical understanding of it. But if you can't communicate the meaning of your data, then it won't do you any good!
<br><br>
It's easy to feel like a lack of correlation is a lack of a result, but knowing that two variables are unrelated is information in itself. Discovering that there is no pattern still means you have learned something about the data set.
<br><br>
**Barplots** are good for showing relationships between categories. Sometimes, the variable you want to change is not numeric, and thus cannot be plotted as a scatterplot. The following visual provides an easy way to see the difference in median revenue based on the genre of movie.<br>
![](https://lh3.googleusercontent.com/pw/ACtC-3fDYTIdKMi8w4amvUpCcrOMkoGsGZ4oivk7G7zOXoYgww6UInWt4p76Jzx2me-t-XZahfkE9szb0zU7DT_Sq9VMif0sP58NUVpnD650jF_GnV1FzPP4ufWd2j00HEwDxp4Q_4BGYx3Wx7kWllSs9Kl3=w388-h263-no?authuser=0)
<br><br>

**Histograms** (and other kinds of distribution plots) are useful for visualizing how data is distributed: often, it has a shape like a bell, as there tend to be more points of data near a middling value, and only a few outliers. Histograms might look a bit like a bar plot, where each “category” is a range of values. Seaborn has a an easy to run method that plots both a histogram and a smoother distribution curve in one simple step!<br>
![](https://lh3.googleusercontent.com/pw/ACtC-3e8x7DDGu1Xdc7Smo3BMNze3vrhlBa1PXeFfxpYXDtzS3vSr4XhCYGGRbd_h29n3qCdX_nbuNTz9L6ENg4bvWoJgefUCHox6uqNJMnnYR7Jq2bkpQXyDr3Pq9szLNA3mt3X_RRQqrNBCdROb6TAzdsf=w372-h274-no?authuser=0)<br>
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
![](https://lh3.googleusercontent.com/pw/ACtC-3c_rpM06k-FtJMxZWjfKuAokSyl6ktOE4t3nkLIsya3J39jWMYuOqrFiV_33abbZ6gEWsetMGU5sPo6TP_9i-GSCy_oklKG05dPvDyJ5sA17fOJLrQgOhpFsovRvySbgxnxn8RSnk6VdZaihpHZR2Sh=w368-h274-no?authuser=0)<br>
This graph is a good example of one thing humans are still much better at than machines: recognizing patterns. Computers can process thousands of numbers in the blink of an eye, but complex patterns escape it. A human can look a the histogram part of that graph (the boxy part, which more precisely shows where the data is) and see that there are no values less than zero. But the complex math that calculates the distribution curve treats it like there is, because of how the calculations work. While finding a way to plot this data where it can figure that out is easy enough, it's a reminder that it's important to always look over the data, and make sure the computer is running the calculations that you think it's running. Computers will always do exactly what you tell them to do, and not necessarily what you intend to tell them to do, if you don't specify something exactly the right way!
<br><br>
**Boxplots** show a simplified kind of a distribution plot, and are particularly useful as they can show multiple categories side by side.<br>
![](https://lh3.googleusercontent.com/pw/ACtC-3fgwZMUV3HN8qKBBOdPgr1bSCu9Otqu-X_5UnuLYe69RJJZusKdMdiQndT2d2pqCBvtHGLSNxO0cG6LNrZw0ptxRJ3HGbcx2m6BCC8tVoGvmK_ob8vArUg8WA0W0Vi777LN87v7Jf013MmHzmkseQyA=w389-h393-no?authuser=0)
<br><br>
By creating visualizations, we can quickly get a sense for what the data can tell us. It can help take us from a spreadsheet full of numbers to an actionable recommendation or a specific understanding, which is the ultimate goal in processing and analyzing data.

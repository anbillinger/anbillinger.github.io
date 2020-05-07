---
layout: post
title:      "Data Visualization"
date:       2020-05-07 17:04:07 +0000
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
![](https://lh3.googleusercontent.com/XG00iXp6P3t0Detw2vu1W6XhXcexsBv6txWrz6dXj4Uq1jB2i-OiuS44KmUa4mqR1dUwJtZdZpuBu_dV9JtljCPQEqgPqWt8CgWromaa4j0nWTUXjJ52B34RMFawugW2CIih9ym1pIr9zPEdE3AFFmCIRGGr_jnyaCupL1ISgh0Gos2qJ0cJEFVrFG8ivDp010MhzzZcCI7xmgUvomacc3YgANW04VuAdhmfZEkUAC_owcfDmH0QjyB7-zUmsK03q7VL6IgB17DATIHXkHYwYEYE0Ao9bXy0KUPnrpUkK3lHZiGMIzW4qQmzk1nNJ-SnkQ5XgrMYNSbz278yPlAtkEaM3uvbdm3tfac4QEpb0ND1q4T4n-30eBClBCfDUypEUS3185Sel3j0edCoF8yWmhI5PXM3ny1Yl8ydGw7H9pAud44rEKW3I-pYoFelfaVk2qM2NP7HbOs-YK_2UVaiXkzZuCfW92C2XqOWTuf6P3mq2p8IlW00hF0tbYQf_rkUQHbgUA5EpSqXMraKybGGSgWrnRjmQ_yDKLerMusDfOl9HfEb2EfgAUwhARkCDa5feHP306moICwuSQi-MDhurhnp-vsem6-1ozCYoTm9IEQ7tO8xk2EYtALzv2DKq8zz0vUCscPSefdQy8rRFt0uHgsa9A5U_2r7Z5aPcKs5mLuMGpX7Ad4UhdWUtL96Gw=w387-h274-no)<br>
And after reading the data set into the notebook as tn_budgets_df, this plot was made with just one line of code:
`sns.scatterplot(x='production_budget',y='worldwide_gross',data=tn_budgets_df)`<br>
So wonderfully simple!
<br><br>
Another way to talk about correlation is the correlation coefficient, which is a numeric value that describes how strongly correlated two variables are. Scatterplots are a way to actually see what that correlation looks like in an intuitive way-which is especially important when sharing information with people who aren't data scientists. No one can really picture what a correlation coefficient means without graphing something, but at least technically trained people will have a logical understanding of it. But if you can't communicate the meaning of your data, then it won't do you any good!
<br><br>
It's easy to feel like a lack of correlation is a lack of a result, but knowing that two variables are unrelated is information in itself. Discovering that there is no pattern still means you have learned something about the data set.
<br><br>
**Barplots** are good for showing relationships between categories. Sometimes, the variable you want to change is not numeric, and thus cannot be plotted as a scatterplot. The following visual provides an easy way to see the difference in median revenue based on the genre of movie.<br>
![](https://lh3.googleusercontent.com/isG7cryys9xTGo_gtw4pwLj9AN8beAq2uXyVkN9UzkkhHBaVLIGazhnEZ3d_VR66eMFfa7QFe_83cC8lg7zeBMF2PAOG7ohPOnDA19y0rbJ3fYDL_CTwLaphqNsNmhAgnIHfZRlyJAcwJw0AtARRyl6_84f74PM_PgkKU_q8_sFUmvR0LnikMN61LSvj2znUAirwg_dZrY7VQRhi4hIsVnQsPggHh7tapQaFZDNgYw55z3JpL87lQ7HzpdZzrl_H4WQZiIyiagh9sR6sEkCBpsbzHAgw6dzq6xY9-zHiLpAtjNXFSNOQZwxs0lHkbIuRs-HTZZgyi9P9rmjDCh-a9rYAjMCsu8rvij88QPmJLW0T0JYVpWeagxu9crn4reFdrVex75eR-5xrBZtoT2s0iapooHi0-XRwnvyMXgSOnAVCx4so1_sPh1tvD63RDLfQEuluGQoYVoEk7VKpOf4G6uDybowXm0wP91-EXI2UBOt-2niHLOisLUsxswZ4UFEWObI8pnPEvUxP4OW7u7K6okma2LjrrJDnqzz5hQXZdiL2mXNScGhiRntoECATVG9cQ-SgpycKipCJP8mVWkcyYY2AtDXsAcSMT54ooe7caJx3NG-uuFnkOXavvTWcb3qnnyE7EVF-B31dDKKhYSp0Kfu4I1-PtNJD5hvWoRrB4oIFrQU3FwEKf6dY-qZ4WA=w388-h263-no)
<br><br>

**Histograms** (and other kinds of distribution plots) are useful for visualizing how data is distributed: often, it has a shape like a bell, as there tend to be more points of data near a middling value, and only a few outliers. Histograms might look a bit like a bar plot, where each “category” is a range of values. Seaborn has a an easy to run method that plots both a histogram and a smoother distribution curve in one simple step!<br>
![](https://lh3.googleusercontent.com/0qhP4DNvG2S1DOxp6TJFrTMuw-kPo6zqaRjJ93P_QiPpzmsjoOkZipesO3HJCWyrH1vUdYOq9WdZBLv-fGO2aTwKiYbSgZ3A4XNfgZF3rH7uReb7y81Q_AKmGoc2x74dY8uhS2Uynl52hhcpZ6srC82e5ThpjyirSbiNfHGH73reZaz-D_PS2dPwEm_2f5iL0-Du8Chmw2SWWdQmgmpWtbAa4mLNrUhTZyjjYG2jAf8h9ptx_ikcPU-5SNmUjSmiBBzINIUNUNAVukc_bJmsS6aOENW0fdg1yA9-Tg5JGUvRkeTyBAx1hauSvA84sEijIcI0DZjDaZoh0uP5k7rQZNAkoCTqzdXXrY6FEMYzcqNBbJp09g_atRHSGe54AlBff4MWsnFqRxHu3vO6jZhYkvV3rtNM7ZX2DzSOvIcYuB1T1-HxoRFHOm3S1Wr6nznK_Euxby3UKl6jdPyeV3koC7uphl53767VInRRBoJAZnyy-Xm_gtps1DN0ILBVfpXH00raR1W8tYCOaiMWbHiZwzAnEWZZtrZSbASlQuK3bDG-0BgSBb_eeZ4GrZrdAVrzmhtKY1PG68M2j0LtvZR0X0MjkN2LYSL29pjRVWtc6U2zoGTAVeyv1nB6mHGHwULBFTWGLm92ZMX-PEj9SrJ-h2AYDaYDn6yFrkgAxZBrpAyHkYcv4cgKfK-9MBNBZQ=w372-h274-no)<br>
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
![](https://lh3.googleusercontent.com/wThdcO-fH4sZElqO5D5kANTSXj9gctr_sQMWZQ0XIH2_3cGyqRJuC_2cHOkLl2qUktQoZvqKYmj_RhB417RtUF8Bc9D0EUgcnOPMmILLec05j6hYMC4LmHtqmYa_G8v93eXmL6bnJRpxwzu-d_cqA-r3z-ImwJi__6r0RSzbEe4kwWtrawVYdN-TNEARAFLegvAwcQLclCDvEgbnU37r0wL96YEAkbQO6fcp64DgyDYCpJqu5QdJw_IhtwTj51waaA8p-iPBsuZJA9i6N0bSZV5UJJnVRHqL48pL9p-lXies5i2OtUjdQ9v3EBVKA5C0CuXoGzSHk0XnBhqH1TImDoVaeFDHa2-0-2ePum4tbvCN65pAs6cWjOxEuSQtSuRWEjNxLOS-OKps91eTkHWoQhBuxa4H4D0_EJn6TStKTUkMnIUZ4dIFTsJpFehXqQ_79yrUCZA7sCFwisvpac1WdVyt5HzEzHmGOACRQOqTRoNynejyiFxEd3DhTip5cPGfsnyIIdJ8vxs4JSYYfJbI1lClOQRI8uzC9zncBZ3HKFQHI2jhqLyPC0vqYJI7t78Fbf-j5SLkF3DMl8TLJDwMW7sRNsZtH87W5cTboXwRDaCaHo5VNdeTDg2HU9bfweEosF-QqsgxRGG_o92BYu1FhEbCw-l21prtTzh0XlefyIGxxaecyTPGpnzWAUIe-w=w368-h274-no)<br>
This graph is a good example of one thing humans are still much better at than machines: recognizing patterns. Computers can process thousands of numbers in the blink of an eye, but complex patterns escape it. A human can look a the histogram part of that graph (the boxy part, which more precisely shows where the data is) and see that there are no values less than zero. But the complex math that calculates the distribution curve treats it like there is, because of how the calculations work. While finding a way to plot this data where it can figure that out is easy enough, it's a reminder that it's important to always look over the data, and make sure the computer is running the calculations that you think it's running. Computers will always do exactly what you tell them to do, and not necessarily what you intend to tell them to do, if you don't specify something exactly the right way!
<br><br>
**Boxplots** show a simplified kind of a distribution plot, and are particularly useful as they can show multiple categories side by side.<br>
![](https://lh3.googleusercontent.com/889ahBKFd7JWiMNtLmfnE2xjbiGuT9Dt50mefSzgKLmBZpLEV7KHLuKMKWgEeK9Pcl9sWaM1ITfd6AdzsfxqFFes7v53fFax8JdlrTPUWSjgrZAzfJFJ9CvAdo-VQtx-Sp6kgIVXo8gwq-gbs5zYoGcWtLUkULQyN0CZYlp2dDdFvvlENiarJuuW_CNdummpv8V9Bnrf0U4KZJai7ajVeBLmFehqQ7f795Lv5ygsVp55xpbrzMgQbsvsXuXquXTk8To4F5dWI0nbcQ4vSAiPZNOdKuRML5ZFmRO39GMPbkG_mbJh1P268WKcHp1Kx_6Y-Pa7typAMFo4TY6j-MQl5s8KVLZRXaKfMB5HjxnShXDlvCMIF1L1KKaoaesAc5GjqtekWrWpsMuHDmj2e6pEq10KXqkZxhQAyPWoR5OesXnQqc0vdhHR8s70svD_NSbwcJY8U89ATOmSdmssAlz1awztKxKTdpEdB7GACOXDbbQM798sILNYISQTYcpw1TjB0mZdHeiKlLpdnIKsA0MkIyuOUhMJoGz5uoqrLt67K1H6UeZNqzX-96_XP_fKC1axm5ehydbCLToW1eREph33qwhV8TyUebcK5tYWhYOW_oRlbvg3FLBmDx2S-Jz8aJuJUGol0SrueUR97eWhz94m8wvGy2rGSWhWE9gSDbRcHjoZii0mpccEq53mRl5vIw=w389-h393-no)
<br><br>
By creating visualizations, we can quickly get a sense for what the data can tell us. It can help take us from a spreadsheet full of numbers to an actionable recommendation or a specific understanding, which is the ultimate goal in processing and analyzing data.

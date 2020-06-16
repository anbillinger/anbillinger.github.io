---
layout: post
title:      "Explaining QQ Plots"
date:       2020-06-16 00:20:41 +0000
permalink:  explaining_qq_plots
---


To start with, the qq stands for quantile-quantile, or a comparison of quantiles between two populations. A quantile represents how many of the data points fall below this value, compared to the total number of data points. To simplify discussion, I will be discussing percentiles, or dividing up a data set into 100 equally sized groups. A percentile represents what percent of data points fall below the given value.<br><br>

Primarily, a qq plot is used to compare the distribution of a data set to a standard type of distribution. Often, it is used to answer the question: is the data set in question normally distributed? This is important, as many kinds of data analysis fail if the data is not normal.<br><br>

QQ plots are extremely technical-while they are very useful for analyzing our assumptions about data (and thus, if a particular kind of analysis will work), it is very difficult to use them to communicate knowledge in any non-technical capacity, nor does it give us information about the relationships between variables.<br><br>

To explain, let's set up an example. We'll use percentiles as the kind of quantile, and compare a data set's distribution to a true normal distribution. Each point represents a certain percentage, where both populations (data set and normal) have that percent of data values at or below that value. The x-axis value is the value of the normal distribution that cumulatively account for said percent of the data, and the y-axis value is the same, but for the data set rather than true normal.<br><br>

This is what allows us to compare the distributions of the population. If the distributions are the same, then the cumulative density functions will increase at about the same rate, which will make all the points lie very close to a 45 degree angled line.<br><br>

For an example, here is a data set which combines two different normal random sets, one has a very narrow standard deviation compared to the other, creating a narrower peak. This dataset is represented in blue, and true normal in orange.<br>

![](https://uitdbw.ch.files.1drv.com/y4mFUBd308e3KF3c71k3YksD7nTcJHIx-s1zoPeCYBBISrRqXHtCm6090VWgbZ1JyKZSeeVCI-7dtU3sm-Gc-aJITFB1R5mtCHiZFjINOZR2bSlNv2vp2SEw61a82FdnjBy-W5wak_iuEIjLtMdWFLOAFSgo5bUG7uFD9ZoeumZvvkDyK9E6R1gQ23NYej2pM-q4pIChljWtCNtzRkj-6d-IQ?width=372&height=248&cropmode=none)<br><br>

Here are the cumulative density plots, which is closely related to what a qq plot shows:<br>

![](https://uisumg.ch.files.1drv.com/y4mPs4_6QMc18xoXGMHbobI7aZoRNf3jPs7m1jBKB9rhvvLkDYwqYahcHyQy4OCoM4lf3c9pM3rPkqpB2mHmCWse8s3zBDarLctQCXl6QbfCqqaBeIDmrxMa0QzADpDnqW8UeOtDSEh7-sZghrgf4606sRSkd1UQx_Dc_aGnbi5cHGrCsHGwsUKXLCjFfC8YnyDzm0PA4r4nQcDFevob-QzeA?width=372&height=248&cropmode=none)<br><br>

The dotted red line represents 20% of the data: 20% of the data points fall below it, the other 80% above it. The vertical blue line represents where that 20% meets the dataset, this is the y-value of the 20% mark on the qq plot. The orange line is where 20% meets the normal distribution: this is the x-value of the 20% point on the qq plot.<br><br>

Here is the qq plot for this dataset:<br>
![](https://uivjdg.ch.files.1drv.com/y4mbxCYu2xfInS69Wk-H5WFmslH9YBEEMA5SIb66LEoz1V82pC0fpexBEo0S-lPHGpBc_aav9eW93PTCdl4HUXv4SKtaLaz4_xS-W3t0Kv71-nFiU83qkTjTLkmUq2ioCFKjuCwgElAl1qVzdDXlY7f5XwZn4vn1SIQJ_NtWNEH5vdmSy9vTeRIT2Qkc7c5rSEAn9VLOCfrk79qtT9LWDBVKA?width=372&height=248&cropmode=none)<br><br>

The orange spot represents the 20% value highlighted in the previous paragraph.<br><br>

The actual values that are plotted in the qq plot (and thus, what the ticks on the axes represent) is number of standard deviations away from the mean.<br><br>

Obviously, the plot does not lie perfectly on the red line, because the data set is not normally distributed. While we can easily see that is not normal, it is hard to tell in what way it isn't normal: which is what makes a qq plot so technical, it is very difficult to build an intuitive understanding of what it represents.<br><br>

To demonstrate what shapes produce what qq plots, I'll provide a few sample histograms and resulting qq plots.<br><br>

A combination of a uniform distribution and a normal distribution results in a distribution that looks like this:<br>
![](https://uiuhsw.ch.files.1drv.com/y4m8p1W4EwhhCXrvjVhBB5xrGOO9CTjonh0U31BOBbCH9PvaRzyib_OgB7S-SxfMbHuSpcw5l1HkGa2jBdQS3EledaeMCAj6UAyujzwhFCT_4ez74xXfxUF62t1ZFmbW6r9_9bHT5PCWmnM_CtAEMO1Ys00lrYn7e8nFVOvh-HIdzb90lYehozEdA6s40U-B15FtOtRABmJh-W6BCnhb9BjQA?width=372&height=248&cropmode=none)<br><br>

And produces a qq plot like this:<br>
![](https://uivxna.ch.files.1drv.com/y4mws-vaZjp9EsR5MTs70fob8AsSRfbWSAc5F7gA25qY9hKtYBGu1n5Z1zumapt1ePiwl7WEvQkylnjN6cgYGIch00lszUYbzwjqxbRo4rg0euTqtzajzllLdDxEtxd8opBSFGRnXDnzkmYMEytj0rWaSI-OoCfD_C3bUL0HD2BxmBnznLOrcD7WK1dPhVLw4YvyED9SBzN4z7ZBIkrZek-PA?width=372&height=248&cropmode=none)<br><br>

Data with a positive skew:<br>
![](https://uiuopg.ch.files.1drv.com/y4mjIMnIczwerSMwzoFZdfBC-1SflpGl5-BDteSX1iXo-V5JwWsteRCSU4b-FVM3NOhFRSJwGS-nHcrjD__bolX-Ykmhhq5R561cupkZ_tOfMt1Zd3ngc-Gl7h82I_w75LNX202X50AOoVgom6ilbZqw9_8DshH-PL-CyMFPJIfbnXyF8YlJHhgZWv8wF17e3JB5YRzwR5txwWcxzSJ_khnrg?width=372&height=248&cropmode=none)![](https://uisnhg.ch.files.1drv.com/y4mW62nzqh6Nes5X6h5EyMiA44tmj5M21gvMvv4xQxDyDnSmwzI5-aQGZ9seZ-hz_bhDDceJbzKlDK6Xh08G-Ipd-FL7HwSvLJHRNHlP_XogygoSpa4CCL0uocgZQrDtXuq6L8vXqNvMB4960Tb75dZxmiq_i9e6BLDhCmRxgYtb3SlKKi_GMYQSATgMw8Ty4m96JWpC2JN7d1pwkZfmvpeCw?width=372&height=248&cropmode=none)<br><br>

Data with a negative skew:<br>
![](https://uis8ka.ch.files.1drv.com/y4mbpqGdrj1YRIxmXI8qoL4sPjWO_dTz3ULgwAvmEaimNXPnSqhzcx9W6wXN-RdIgZ736UHhI-W8Y0Ezf8rrb_oqe5RlanVd_DqNvjkNKjVpm4hrO-uRo580GrAZKIdgCGnCV6VG70qGsIhAAC15vNsQOSdrKci8ta4GPQFWDmSiP1It_9axQHQv6BNOGkd7HnaL9wI_tDDyQWRduaidHQkZA?width=372&height=248&cropmode=none)![](https://uityeq.ch.files.1drv.com/y4mPmiX16Mfwt8m3oqi_YEmQHSr7s5bSCmBIj063bPvDeuwDnLhtAUcli7oENokqutsK_h1bz8xxzVJn3zb-6p8MfZ6hfwjB3XVkXi2vOAkmxupjOf23dLAW9TzrFho9FVJJgc0JaRCrYjf5Qxkhz_iGOXUF0ElUxdKPkTbvf6BAia_c_Uj1nvI5W882VzPkOnEb-jobjE1O0Xn3ObsuSEpAw?width=372&height=248&cropmode=none)<br><br>

Which group of data points has more points in a particular range has a much more noticeable impact on the slope of the qq plot than it does on which side of the 45 degree line the plot is on, which is one of the main reasons that intuitive understanding of a qq plot is hard to develop. It basically requires an intuitive understanding of calculus, and as someone who has a high level of technical understanding of calculus, it's still not super intuitive. With my technical understanding of the math behind these things, I believe that my intuitive understanding will grow with time.

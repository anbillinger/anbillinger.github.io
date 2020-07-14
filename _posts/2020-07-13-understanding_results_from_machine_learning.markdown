---
layout: post
title:      "Understanding Results from Machine Learning"
date:       2020-07-14 00:45:53 +0000
permalink:  understanding_results_from_machine_learning
---


Machine learning is an incredibly powerful tool, but it's important to remember that computers will never understand the data they look at. It's up to the humans working with the data to look at the results to understand what information can be gleaned.

### Minority Classes

One thing to note before training even begins is the relative frequency of classes in the target category. When one class is a very low percentage of the total data set, it makes analysis more complex. If category 1 only represents 5% of the data, a computer could report back that it has 95% accuracy. This certainly sounds like very high accuracy... but it got there by simply skipping category 1 completely. While there are ways to train around this relatively low amount of data, it is something that still needs to be taken into account. Generally, the two ways to account for a minority class are undersampling (taking the entire minority class and an equal number of samples of other classes) and oversampling (creating duplicate entries of the minority class). Undersampling can work well for very large datasets, but even then, it can make testing uneven, which will require further attention at later stages. Oversampling often means that the algorithm will put too much weight on only a few samples, which can lead to....

### Overfitting

An algorithm is said to be overfit when it learns every detail in the dataset, even the parts that are just random noise. For instance, if we try to teach a computer to recognize a human from an image, but if we either tell it to pay super close attention to every detail, or only give it a very small number of images, it may lead to the algorithm insisting that humans must have very specific skin and hair colors, or that anyone who has lost a limb wouldn't count. <br><br>

One possibility to counteract overfitting is to simply tell the algorithm to ignore some of the details. If it is training from the dataset until it can accurately predict every single sample in the training set, it often won't be able to adapt to new data, so we can program to stop before that point, and accept some unknowns in the original data. This can potentially lead to underfitting, when the algorithm doesn't take enough details into account to be able to sort the data. Continuing on the example of an algorithm trying to recognize a human, an underfit algorithm could be fooled by Diogenes presenting a plucked chicken (who declared “Behold! I've brought you a man” when Plato described humans as featherless bipeds).<br><br>

Sometimes, tweaking the amount of detail can balance a model out between overfitting and underfitting. However, it's also possible that there is simply not enough data-either too few samples or perhaps a variable that has a strong effect on the results but was not recorded in the original dataset. The difference between these cases is something that a computer will almost never be able to detect-it requires a complex kind of pattern recognition that people are good at, but computers aren't there yet. Which goes back to the original point-it's important to think about what the data and numbers mean, since a computer cannot tell us that, and it can have a huge impact on how we treat the data and how we go about improving the model.

### False Positives and False Negatives

Another example of results that can only be decreased by increasing the chance of a different nonideal value, is false positives and negatives. A false positive is when the algorithm predicts that something is true when it is false (for instance, trying to find if someone has a certain illness, and it reports that they're sick when they're completely healthy). A false negative is the opposite-when the actual value is true, but the algorithm predicts false. Generally, if you want to make sure every time an example is category A is properly predicted as category A instead of B, you will have to tell the algorithm to predict B less often, and thus more samples of B will be incorrectly labeled as A as well. If we want to make sure every sick person is correctly labeled as sick, it is going to greatly increase the number of healthy people who are incorrectly labeled.<br><br>

Confusion Matrices are a way to visual the relative rates of true to false for both positives and negatives. Here is an example of a confusion matrix:<br>
![](https://t7b5ea.ch.files.1drv.com/y4mh8cjvCSchj_mM08xrRtDVbG_PuQgnsI-Rpyp9zvk7SKt0JaRbB47Rq0bXlyQaBT2pDdyzTzLbIN5z0e6YPp6QA3IWtWwoi56VS7fVeOZjLWwPif7ryENiSQPWNYRLb_k1I7JbTSNtPBWHsNF4gqa-QMhJ2-5Qne_dEr2zNDoXd-RcFGv1wxk9w3hihhaX_wKXe0z6WpQMfzIVBJbIuw5yA?width=322&height=278&cropmode=none)<br>
(Where “func” represents functional water wells, “rep” represents repairs required but still functional, and “non” represents non functional)<br><br>

The diagonal line from top left to bottom right represent the correctly predicted values, the other squares represent incorrectly predicted values. The shade represents the frequency that that particular combination of actual value and predicted value occur. Rows show the actual label, so the top row represents all the functional wells, with the first being those correctly labeled, and the following two values as those that are functional but were predicted to require repairs or be non functional. Columns represent the predicted label: so the far left column represents all samples predicted to be functional, whether or not they actually are.<br><br>

Given that there are multiple categories, which incorrect values represent false positives and which are false negatives is not immediately obvious. We have to consider a specific label to determine relative positives and negatives. If we consider the label functional, then we need to look at both the top row and left column. The intersection are the correct values. The row shows false negatives: actually positive for the “functional” label, but predicted as something else. The column contains the false positives: predicted as functional, but actually a different label.<br><br>

Note how pale the entire center row is: this ties back into the original topic of minority classes. The middle square will never be dark blue, because it is relative to the entire dataset. It cannot have a high total percentage of correct predictions because there is not a high percentage of actual values to be correctly predicted. The rest of the center row shows that there are fairly few false negatives for repairs required; if repairs are needed it is usually correctly predicted as such. However there are quite a few false positives: other categories that are incorrectly predicted as needing repairs.<br><br>

Minority classes, overfitting vs underfitting, and false positives vs false negatives are some of the examples of why a human understanding is always necessary to go over a model built by a computer: a model will almost never be perfect, and establishing which errors are more acceptable than others requires a kind of understanding that computers cannot do.

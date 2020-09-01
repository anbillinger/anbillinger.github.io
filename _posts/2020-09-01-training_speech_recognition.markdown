---
layout: post
title:      "Training Speech Recognition"
date:       2020-09-01 22:19:04 +0000
permalink:  training_speech_recognition
---


![](https://eozt5q.ch.files.1drv.com/y4mOHUzwJVErQWol5EJXvbe7-EKwA3R-7JSkRr47iMA4SI_8EBz84tYygJuiZkxZYlILRC8ULxvE2vT4icrXAB11kKAhWo5reVKyj-mXK7WUDGhxy6k32wDwh5X_A73P9jXfWOB56WA1-0wu5uqaUinh-5I1usjyFck7Snpg1zNeEl6csPW5CT1QIxlfl3qrgRVqxA2fGYLYPsUHrDMe_aZ2A?width=412&height=355&cropmode=none)
<br><br>
Many people have difficulty with spoken words, whether hard of hearing or even just checking voice mail in a noisy place. Speech recognition is a powerful tool with modern technology; training a computer to understand audio files and print the words, so that the information is accessible in a different format. Using technology to improve accessibility is a passion of mine, so I decided to develop my own algorithm for speech recognition prediction. My goal was not to create a better tool than what's available on the market today, but to build an understanding of the process involved. Being limited to my own computational resources meant I simply don't have the computing power to develop a highly accurate model. <br><br>

My approach was to start with audio data, in the form of labeled phrases, from a variety of speakers. The data set I used can be found here: [link](https://www.kaggle.com/mozillaorg/common-voice). Since predicting phrases is not broadly applicable for speech recognition, the first step after getting the data into a jupyter notebook, was to split the phrases into individual words. To do this, I first cleaned up the audio by normalizing the volume and cutting out the silence. Then, using the text labels, I found syllable counts for each word, and the total in the phrase, and used this as a percent of the total time of the audio. This method is approximate, but by checking the resulting clips, I found it was reasonably accurate. I then lowered the quality of each clip (the frames per second) so that each clip had the same number of values. These values, converted to an numpy array, were used for training the model.<br><br>

Here's a sample of what the process looks like, for the phrase “learn to recognize omens and follow them the old king had said”, and the clip of this audio that contains just the word "recognize".<br>
![](https://eobsca.ch.files.1drv.com/y4m2-Kw6CRS5iAXUBTA2Cp8xzcp8uPGrojn_-34R07coiNvW1fxeFHvtdPaxEKRsp8OlWoFdpwJKBAe9muUCT3T59wlx2e_uqOW-Kz8VHqQ4AszXm2rV3Qycrz65N2RjQDOPsq1PtetvUBHCdKduVBLBedFnN78TZ8w-PQ3OoYyYI3CZAvdVrCCo5ZUo5wYsCaYV3PM0jgy6XpyUOYanqVpeQ?width=421&height=293&cropmode=none)
<br>
![](https://eoyiwg.ch.files.1drv.com/y4mrv-4uCIJbCvioKleMD4xDwxKsBv_olI9g3r7rkF9uFC08hfs2fNQ3j00zSYSU4vFyk1eBD_WJ9ZIMtaDJinSarwzkHgEcTl0NbCsIrHYx5fGA2fE4Rh1nPXn4YV-FfjSD0-1Y-wpq5Xw8rrsfJZ1yvECWEFeeTgJufXBtTig7GYKxAyxppbXF53nOTvG5180S4LABN7XToau4n2LCFPPtw?width=396&height=278&cropmode=none)<br>
![](https://eobzha.ch.files.1drv.com/y4mPNUm5fsHlBiEhMHrcEOhbDGN6A8D62NTYbJWxoW71x18HH8aJY7v6ihUE0Yl9dag-8OmxUUgIRU1AGbfPunIriglrFOZbierB3IP1ZewqhKbXJ4WbsNNW4VQC4Xo1hvrp7nwVAgQtOPrbUpAwxsPfYlOnDhqmJqLbXm4LIHaH4AciBAeDYsicl65TYfzHqNDaQLCl-PtgLFdpW9anSIZ8Q?width=396&height=278&cropmode=none)

<br><br>
For the text data, there were a total of 8000 unique words. I found the 1000 most common to use as the labels for prediction, as well as an [UNRECOGNIZED] category.
<br><br>
This is where I started to run into computer limitations. Even using 5000 phrases (the training data set from kaggle has 195776 phrases), resulted in 0.7 GB for the file (or 3000 * 47000 values!), which meant that even using this small fraction of the total data, it could take hours for my computer to train one model. Given that there were slightly over 1000 possible labels to predict, it meant that trying to get even a reasonably high accuracy involved testing many parameters. I also consistently ran into a problem of overfitting, even with fairly heavy regularization.
<br><br>
To build on this project in the future, I would love to return to such a project with more computation resources. This would allow both a possibility of using more data, as even my data intensive models used less than 10% of the available data, as well as making it possible to test more models. Another area where I would like to try to improve is in how the data is split-the current splitting method is approximate, but more than that, it only works on labeled data, which would make parsing a phrase impossible for my current model.
<br><br>
This project has really given me perspective on the scope and power available with big data. While modern speech recognition tools are far from perfect, training a computer to recognize words is an incredibly complex and resource intensive task. I look forward to seeing how accessibility tools like speech recognition improve in the future, and contributing the data science skills I have developed to be a part of their improvement.
<br><br>
Footnote: for code and more information, my repository can be found here: [link](https://github.com/anbillinger/capstone)

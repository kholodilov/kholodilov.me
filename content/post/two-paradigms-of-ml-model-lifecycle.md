---
title: "Two paradigms of ML model lifecycle"
date: 2019-06-15
draft: true
tags: []
---
Tech mainstream - "engagement" models
Enterprise - "risk" models

As a data scientist at typical bank or insurance company you build your typical risk model using wide horizon of historical data - at least half a year, probably a couple or more. You have two reasons for this. First, there is not so much data in the first place, so with bigger timeframe there are more samples to train the model. Second, you need to make your model to behave well over time in future - for example, learn seasonality of business from data, but more importantly, be stable over time (not to use any unreliable signals). You need reliability, because it's critical for business. As a bank, you don't want to suddenly start giving significantly more (or less) loans for no good reason (assuming nothing changed in the real world, only in your data), as you either giving money to bad loaners with higher probability than before, or leaving money on the table by cutting off good ones. Following this principle of the least surprise, you most probably don't use anything sophisticated like neural networks - I'd bet in majority of cases it's logistic regression or, for the most adventurous, gradient boosting trees.

Cool story starts after your model is deployed to production. You don't get any feedback on its real performance any time soon. Usually you predict something like 3 to 12 months probability of credit default, i.e. you can check whether your prediction turned out right or wrong only after 3-12 months. Sure, there are cases with faster feedback, like fraud prediction or monitoring of existing credit portfolio for sudden risks, but in my understanding these typically rely less on machine learning and more on simple, easily interpretable signals.

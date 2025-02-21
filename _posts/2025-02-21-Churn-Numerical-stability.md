---
title: "Predicting Customer Churn with Bayesian Models: A Data Science Team Innovation"
tags:
  - Statistics
  - Churn
toc: true
---

# Predicting Customer Churn with Bayesian Models: A Data Science Team Innovation
![Customer Purchase Patterns](/assets/images/articles/churn_1_header_pexels-rostislav-30767251.jpg)

Customer churn – it's a challenge every business faces. Losing customers impacts revenue and growth, making customer retention a top priority.

One of the key models is the BG/NBD model, a powerful Bayesian statistical approach for understanding customer behaviour and predicting future purchasing patterns. This model helps us estimate the probability of a customer remaining active over a certain period.

## Simplifying Churn Prediction
In a recent research paper, our team tackled some practical limitations of the BG/NBD model, especially in industries like iGaming where customer activity can be sporadic and influenced by events. We focused on a specific question: what is the probability that a customer makes no purchases within a given time frame?

While a general formula exists for calculating the probability of any number of purchases (Equation 34 in the original BG/NBD model documentation), we discovered that focusing on the "no purchase" scenario allowed for significant simplification. By setting the number of purchases to zero, we dramatically reduced the equation's complexity. This simplification is important because it enables more efficient and accurate churn prediction.

## Addressing Computational Challenges

![Computational Challanges](/assets/images/articles/churn_2_numerical_stability_pexels-karolina-grabowska-5238079.jpg)

Another significant contribution of our work was addressing potential numerical issues. The calculations involved in churn prediction can sometimes lead to extremely large or small numbers, causing unexpected behaviour due to the limited precision of floating-point arithmetic [Goldberg, 1991](https://dl.acm.org/doi/10.1145/103162.103163). This can manifest as "overflow," where a number exceeds the maximum representable value, or "underflow," where a number is smaller than the minimum representable value and gets rounded to zero.

To overcome this, we implemented a clever numerical technique using logarithms and exponentials to rewrite the equations to avoid these extreme values, ensuring the accuracy and stability of our churn predictions. Avid readers are urged to have a look at the paper referenced below.

## From Theory to Practice: Implementation and Impact
This research isn't just theoretical. We've translated our findings into practical code, with an implementation accepted as part of the open-source [PyMC Marketing](https://github.com/pymc-labs/pymc-marketing/releases/tag/0.11.0) library. 

The mathematical motivation, derivation, and numerical techniques referred to above, including examples of different customer behaviours, are available on [ArXiv](https://arxiv.org/abs/2502.12912).

By improving the accuracy and efficiency of churn prediction, we're empowering our operators to make data-driven decisions, personalise customer interactions, and ultimately, build stronger, more lasting relationships. This work represents a significant step forward in our ongoing efforts to leverage data science for churn prevention and enhanced customer lifetime value.


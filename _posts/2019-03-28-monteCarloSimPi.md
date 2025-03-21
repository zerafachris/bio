---
title: "Approximate Pi numerically using Monte Carlo Simulations"
tags:
  - MLOps
  - Productionisation
  - API
link: https://github.com/zerafachris/playGround/blob/master/published/monteCarloSimPi/readme.md
---

In this article, I demonstrate a Monte Carlo simulation approach to approximate $\pi$ by calculating the ratio of points within a unit circle to points in a surrounding square. The method involves randomly sampling points within a defined space and measuring their distribution relative to the circle boundary. Using Python, I iteratively increase the sample size to show how the simulation’s accuracy gradually converges to the true value of $\pi$, illustrating the Central Limit Theorem in action. The code calculates approximations of $\pi$, displays results for varying sample sizes, and visualizes convergence through error analysis, providing a clear example of Monte Carlo simulation in practice.

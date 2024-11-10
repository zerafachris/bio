---
title: "Hash Code 2018 Pizza Slicer Practice Problem"
tags:
  - ML
  - Optimization-Algorithms
# link: https://github.com/zerafachris/playGround/blob/master/published/deployingML/0_readme.ipynb
---

The Hash Code 2018 Pizza Slicer Practice Problem challenges participants to cut a large pizza into slices that contain a valid mix of ingredients, aiming to maximize the score by creating the largest valid slices possible. The solution involves a "Scan and Grow" algorithm, which scans unsliced pizza positions, identifies the largest valid slice from a starting point, and grows the slice outward. The algorithm checks each slice for validity, ensuring the required ingredients are included. To optimize performance, type annotations and Pythran (a C++ compiler for Python) speed up key functions, while efficient data structures like sets and lists streamline slice validation and scoring. This iterative, greedy approach works to maximize scoring by expanding valid slices across the pizza without compromising the ingredient requirements.


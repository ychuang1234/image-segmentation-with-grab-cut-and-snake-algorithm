 <h1 align="left">Image segmentation with Grab-cut and Snake algorithm </h1>
<h2 align="center"> 
  
  ## Goal
Implementing Snake algorithm in python and compare the performance with Grab-cut algorithm provided in OpenCV.
 
  ## Introduction
  
**Dynamic programming (DP)** is one of efficient way to solve 0/1 knapsack problem (**maximization problem with constraint**). However, when the selected items and contraint become larger, it **increases computation time** and **takes more memory to store the result of subproblem**. In real case, the weights (cost) distribution of items is **not uniform**. Normally, the distribution is skewed toward the lower half of the possible range of the weights. I utilize this characteristics and make some items with small cost to merge into one new item with bigger cost, resulting in smaller number of items being considered.

 ![](http://latex.codecogs.com/svg.latex?\int_{0}^{1}E_{snake}(v(s))\mathrm{d}s=\int_{0}^{1}(E_{internal}(v(s))+E_{image}(v(s))+E_{con}(v(s)))\mathrm{d}s
 
 ![](http://latex.codecogs.com/svg.latex?E_{internal}=\alpha(s)\leftv_{s}(s)\right^{2}
  
  
  ## Description
First, I create a binomial tree to each bucket of weights (e.g., bucket1: [w:1 - w:9], bucket2: [w:10 - w:19],...). The reason of choosing binomial heap to record the items is because it only takes **O(1) time** for **deleting**, **inserting**, and **merging operation**. Second, traverse the heaps to search if there are possible sub-heaps that could be merged into the bucket with higher range of cost. After compression, I also quantized the cost in the same bucket to trim some variability in weights, accelerating the process in solving problem.
 
## Experiment and Result

This is the output from .ipynb file with various experiment settings.
<p align="center">
 <img src=https://github.com/ychuang1234/image-segmentation-with-grab-cut-and-snake-algorithm/blob/5a57fe4ae9e521f14e831821d398cf6ce723df8e/procedure.JPG " height="80%">
 </p>

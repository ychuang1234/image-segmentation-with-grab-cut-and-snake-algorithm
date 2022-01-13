 <h1 align="left">Image segmentation with Grab-cut and Snake algorithm </h1>
<h2 align="center"> 
  
  ## Goal
Implementing Snake algorithm in python and compare the performance with Grab-cut algorithm provided in OpenCV.
 
  ## Introduction
  
 Snake algorithm (a.k.a **active contour algorithm**) is one of the algorithm for **image segmentation**. Its main idea is to find the **contour** minimizing deformation (defined as internal energy) and pull the spline toward contour of objects at the same time (defined as external energy). Therefore, snake could be considered as one of algorithm in fields of matching deformable model to an image by energy minimization.

 
  ## Description
 The object function in Snake algorithm is defined as followed, which is comprised of 3 parts: internal energy, external energy, and optional contraint energy defined by engineer:  
 ![](http://latex.codecogs.com/svg.latex?\int_{0}^{1}E_{snake}(v(s))\mathrm{d}s=\int_{0}^{1}(E_{internal}(v(s))+E_{external}(v(s))+E_{constraint}(v(s)))\mathrm{d}s)
 
 ### (1) Internal energy is used to defy deformed spline by penalizing more when spline become less smooth and more winding. 
 
 ![](http://latex.codecogs.com/svg.latex?E_{internal}=E_{uniformity}+E_{curvature}=\alpha(s)\left|v_{s}(s)\right|^{2}+\beta(s)\left|v_{ss}(s)\right|^{2})
 
  ### (2) External energy become larger as the spline pass through the salient features in image, such as line, corner, and termination in image. Therefore, this energy would try to pull the spline toward the contour of objects and avoid to include images' line and corner. 
  
 ![](http://latex.codecogs.com/svg.latex?E_{external}=E_{image}=w_{line}E_{line}+w_{edge}E_{edge}+w_{term}E_{term})

 ![](http://latex.codecogs.com/svg.latex?E_{line}=I(x,y))
 
 ![](http://latex.codecogs.com/svg.latex?E_{edge}=-\left|\mathbf{\nabla}I(x,y)\right|^{2}=-\left|\frac{\partial{I_{x}}}{\partial{x}}+\frac{\partial{I_{y}}}{\partial{y}}\right|^{2})
 
 ### (3) Contraint energy (optional) : In this project, I used random gaussian noise as the contraint energy 
 ![](http://latex.codecogs.com/svg.latex?E_{constraint}=G(\mu,\sigma))
 
 ### (4-1) Optimization step (thereoretically): Gradient decent
 ![](http://latex.codecogs.com/svg.latex?\bar{v(s)_{i}}\longleftarrow{v(s)_{i}-\mathbf{\nabla}E_{snake}v(s)_{i}}=v(s)_{i}-w_{internal}\mathbf{\nabla}E_{internal}v(s)_{i}-w_{external}\mathbf{\nabla}E_{external}v(s)_{i})

  ### (4-2) Optimization step (in this project): trust region optimization
 Search in pre-defined range to find if there is any new position that could lower snake energy and update. 
 <p align="center">
 <img src="https://github.com/ychuang1234/image-segmentation-with-grab-cut-and-snake-algorithm/blob/5ddcdb5a28b30120e567e35b57c5ed3f371123d4/TRO.JPG" height="80%">
 </p>

## Experiment and Result
This is the procedure in experiment but **not yet adjust the weights** of each designated energy term.
<p align="center">
 <img src=https://github.com/ychuang1234/image-segmentation-with-grab-cut-and-snake-algorithm/blob/5a57fe4ae9e521f14e831821d398cf6ce723df8e/procedure.JPG " height="80%">
 </p>

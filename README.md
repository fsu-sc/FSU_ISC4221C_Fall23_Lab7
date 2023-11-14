# FSU_ISC4221C_Fall23_Lab7

Part 2 of Data Mining 

Your report should be a self-contained markdown file with a description of your answers, 
relevant code copied inside of it and the images embedded.


# Part II - Image Compression using K-Means

If we have a grayscale image then each pixel is represented by an integer between 0 and 255; if we have a color image we know that each pixel is represented by three RGB values creating a myriad of colors. Our strategy now is to choose just a few colors to represent the image. An obvious application of this data compression is when you print an image using a color printer with many fewer colors than are available on your computer. After we choose these colors then the image chart for the picture must be modified so that each color is replaced by the new color that it is “closest” in color space.

We can use K-Means (or a discrete CVT) to accomplish this image compression. For example, suppose we have a grayscale image and decide that we want to represent it with 32 shades of gray. Our job is to find which 32 colors (out of 256) best represent the image. We then initiate our probabilistic Lloyd’s algorithm with 32 generators which are numbers between 0 and 255; we can simply choose the generators randomly. In Lloyd’s algorithm we need to sample the space so in our application this means to sample the image; i.e. sample a random pixel. If the image is not too large then we can simply sample every pixel in the image. We then proceed with the algorithm until convergence is attained. After convergence is achieved we know the best 32 colors to represent our image so our final step is to replace each color in our original matrix representation of the image with the converged centroid of the cluster it is in. For this application we will just use a constant density function and the standard Euclidean distance for our metric.

We will need routines to generate the image chart (i.e. our matrix) from an image and to generate an image from our approximation.  There are various ways to do this. You can Python libraries PIL, OpenCV, or scikit-image. And you can use Matplotlib to display the images.

Remember that when you read an image the format may be in unsigned integer format i.e. (uint8). You should convert this to floats before writing to a file or using it. 

## (30 pts) Problem 1
In this problem, you will generate a CVT using a probabilistic Lloyd’s method and plot it to see that everything is working correctly.
 Modify your K-Means algorithm (from last lab) to perform a probabilistic Lloyd’s iterative approach to form a CVT for a region which is an n-dimensional box and calculate the cluster variance. 

 As a suggestion, you can make a function with the following prototype:

    ```python
        def probLloyds(dims, m, a, b, maxIter, tol):
    ```
        where dims is the dimension of the box, m is the number of generators, a and b are the lower and upper bounds of each dimension, maxIter is the maximum number of iterations, and tol is the tolerance for the stopping criteria. The function should return the generators and the cluster variance. 

Test your code by generating a CVT diagram in the region (0 2) × (0 2) using 100 generators. You can use *Voronoi* from 
*scipy.spatial* to plot the CVT (as in the class example). Use a maximum number of iterations 300 and a stopping criteria of distance between current and previous clusters ($\max_{j = 1, ..., k} ||c^{k+1}_j - c^{k}_j || \leq \text{tolerance}.$) with a tolerance of 0.005 for each case. 

 1. Use 10 sampling points per generator, display your tessellation. 
 2. Use 100 sampling points per generator, display your tessellation.  
 3. Use 1000 sampling points per generator, display your tessellation. 
 4. Tabulate the number of iterations required to converge in each case. 
 5. Plot the cluster variance for each iteration.
 6. 6. Describe What conclusions can you draw from your result?

## (20 pts) Problem 2
Use the grayscale image boat.tiff and modify your algorithm (you can create new functions)
 to obtain approximations to the image using **4 8 16** and **32**
 shades of gray. Display your results along with the original 
 image. As generators choose e.g. 8 random points between
  0 and 255 and because there are a reasonable number of pixels
   in your image ($512^2$) you can sample the image by simply choosing each pixel 
   to determine which of the 8 shades of gray it is closest to. Use $10^{-2}$ as a
    tolerance in your stopping criteria. After your algorithm has converged don’t 
    forget to replace each entry in the image matrix with the center of your cluster.

In your report, show the original image and the approximations for each case.

## (20 pts) Problem 3
Use your favorite color image (or mandrill.tiff) and modify your algorithm to obtain 
approximations to the image using **4 8 16 32** and **64** colors. Display your results along 
with the original image. As generators, you will choose e.g. 8 random points in the RGB 
color space and as long as there are a reasonable number of pixels in your image 
(such as $512^2$) you can sample the image by simply choosing each pixel to determine
 which of the 8 colors it is closest to; you can use the standard Euclidean length 
 treating each point as a three-dimensional vector. Use $10^{-2}$ as a tolerance in your stopping criteria.


In your report, show the original image and the approximations for each case.

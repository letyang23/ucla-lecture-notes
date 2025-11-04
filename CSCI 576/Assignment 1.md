# Programming Part: (100 points)

This assignment will help you gain a practical understanding of Quantization to analyze how it affects visual media like images and video. We have provided you with a Microsoft Visual Code project and a java class to display two images side by side (left - original and right - output of your program). Currently both left and right correspond to the same input image. You will need to modify the input per this assignment and display your output on the right image. You are free to use our provided setup, or design a new one as long as you use C++ / Java.

**Input to your program will be six parameters where**

*   The first parameter is the name of the image, which will be provided in an 8 bit per channel RGB format (Total 24 bits per pixel). You may assume that all images will be of the same size for this assignment, more information on the image format will be placed on the class website
*   The second parameter is a "color mode" C which can take on values 1 or 2. 1 indicates working in RGB space, 2 indicates working in YUV space.
*   The third parameter is a "quantization mode" M which can take on values 1 or 2. 1 indicates a uniform quantization mode and 2 indicates an optimized advanced or smart mode Refer to details for each mode.
*   The last three parameters (Q1, Q2, Q3) control quantization bits in each channel whether RGB or YUV. Each Q_i (0 < Q_i <= 8) specifies the number of bits required for the respective channel. The quantization is assumed to be uniform when M = 1. For M=2 you need to develop an optimized quantization technique for each channel. Please refer to the lecture discussion of this assignment for details.

To invoke your program, we will compile it and run it at the command line as

`YourProgram.exe C:/myDir/myImage.rgb C M Q1 Q2 Q3`

**Examples calls to your program**

1.  `YourProgram.exe image1.rgb 1 1 8 8 8`
    This shows color mode C=1 (RGB), quantization mode M=1 (uniform quantization) and output 8 bits per channel. Since the original input has 8 bits per channel, this implies that the output is the same as the input.

2.  `YourProgram.exe image1.rgb 1 1 2 2 2`
    This shows color mode C=1 (RGB), quantization mode M=1 (uniform quantization) and outputs 2 bits per channel. This would imply 4 specific values each for R, G and B channels after uniform quantization is applied which should yield utmost 64 unique colors in the output.

3.  `YourProgram.exe image1.rgb 2 2 2 3 3`
    This shows color mode C=2 (YUV), a smart quantization mode M=2 and having 2 bits for Y and 3 each for U and V. would imply 4 specific values for Y, and 8 for U and V. channels. The distribution of quantization boundaries would be non-uniform and would depend on your algorithm to maximize quality (minimize error).

Now for the details - In order the display an image on a display device, the normal choice is an RGB representation. This is what the format of the input image is. Depending on the input parameters you could perform quantization in the RGB space. If you need to process in YUV space, you will have to convert the image in YUV space, process your quantization and reconvert it back to RGB space to show the output to display. Here is the dataflow pipeline that illustrates all the steps.

1.  Read Input Image
    *   Display Input Image (This code is already provided to you, if you choose to make use of it)

2.  Convert to YUV space if needed
    *   The RGB to YUV with the conversion matrix is given below should the input parameters require this

3.  Process quantization of channels
    *   Process quantization of channels - uniform for M-1 and smart non-uniform for M-2

4.  Convert to RGB space if needed
    *   Display Input Image
    *   The YUV to RGB with the conversion matrix is given below should the input parameters require this.

##### Conversion of RGB to YUV
Given R, G and B values the conversion from RGB to YUV is given by

$$
\begin{pmatrix} Y \\ U \\ V \end{pmatrix} = \begin{pmatrix} 0.299 & 0.587 & 0.114 \\ -0.417 & -0.289 & 0.436 \\ 0.615 & -0.515 & -0.100 \end{pmatrix} \begin{pmatrix} R \\ G \\ B \end{pmatrix}
$$

Remember that if RGB channels are represented by n bits each, then the YUV channels are also represented by the same number of bits. RGB values are positive, but YUV can take negative values!

##### Conversion of YUV to RGB
Given R, G and B values the conversion from RGB to YUV is given by

$$
\begin{pmatrix} R \\ G \\ B \end{pmatrix} = \begin{pmatrix} 1.000 & 0.000 & 1.1398 \\ 1.000 & -0.3946 & -0.5806 \\ 1.000 & 2.0321 & 0 \end{pmatrix} \begin{pmatrix} Y \\ U \\ V \end{pmatrix}
$$

Remember that if YUV channels are represented by n bits each, then the RGB channels are also represented by the same number of bits. YUV channel can have negative values, but RGB is always positive!

##### Quantization Details:
For M=1 you will need to perform uniform quantization in either RGB space or YUV space depending on the prior input value of C. This means that, for a channel with input quantization value $Q_i$, the range of each channel will be uniformly divided into $2^{Q_i}$ uniform regions. Eg in our case, the input range of R varies from 0-255, then for $Q_i=2$, you have 4 uniform regions: 0-63, 64-127, 127-192, 193-255.
The center value of each region may be chosen as the represented value for that region. In our example here, each region will have a representative value respectively corresponding to 32, 96, 160, 224 respectively.
All image channel values in a region should be replaced by the represented value. In our example, all values (0-63) in the first region will be replaced with a value 32. Similarly, the other regions will need to be remapped to their representative color.

For M=2, you will need to devise a way to perform non-uniform or non-linear quantization in either RGB space or YUV space depending on the prior input value of C. This means that, for a channel with input quantization value $Q_i$, the range of each channel will be non-uniformly divided into $2^{Q_i}$ non-uniform regions. **While there are many ways to divide the range into meaningful non-uniform regions, some better than others, our expectation is that your output for M=2 is quantifiably better than your output for M=1.**

Let's take a hypothetical example where we have a bias towards the mid-range of gray values in the R channel. In this case, while the input range of R varies from 0-255, for Q = 2, you could arrive at 4 non-uniform regions: 0-131, 131-157, 158-181, 181-255. This is because in our hypothetical example most values are concentrated between 131 and 181. The ideal bounds of each region will depend on the distribution of values in the specific channel and is left to you as a thought process as to the best way to decide on them.

Finally, as in the uniform quantization process, all values in each region should be mapped to the representative value (typically the center) for that region. In our hypothetical example, all values (0-131) in the first region will be replaced with a value of 66. Similarly, the other regions will need to be remapped to their representative colors 144, 169 and 218 respectively.

**What should you submit?**

*   Submit source code ONLY (no binaries) with README file.
*   One analysis document for the analysis part below that shows results and discussion (paste output images directly into the document).

# Analysis Part: (100 points)

(Do not submit code, Submit only results as suggested):

In our implementation, given a value for C (1 for RGB and 2 for YUV), we perform quantization based on M (1 for uniform and 2 for smart non uniform). The number of regions for each channel depends on Q1 Q2 Q3. When the final display outputs are considered, the total number of bits used matters. While our input bits per pixel is 24, the total number of output bits per pixel will be N= Q1 + Q2 + Q3. (0<Qi<=8) In this analysis question, we want to understand how to make use of our total bits N more intelligently by spreading them appropriately over the channels so as to provide the best possible output.

Write a program to evaluate a quality metric. This should be as simple as $Error = sum (abs(originalValue - outputValue))$ for all pixels for all channels The lower the error, the better the quality of your output. This error should be computed in the same RGB representation between the input and output.

### Analysis Question 1:

In this analysis question you want to analyze given a value for N, what distribution of values (which sum to N) for Q1, Q2, Q3 gives the least error and best quality. Consequently, given an N, write a program to enumerate all possible values of the tuple <C, M, Q1, Q2, Q3 >. For each tuple, run your program to get an output image and compute the error metric above. Plot a table with first column showing N, second column showing <C, M, Q1, Q2, Q3>, third column showing the result image and fourth column showing the error as shown in the table below. Using one good example image, fill in all possible values for N=4,6,8. Remember, the output image is for you to perceptually understand the output quality for the given input values. The combinatorics may result in a lot of tests for N=6 and 8. Consequently, for the purposes of submission, you need to show the output images only for N=4. For N=6 and 8 you may just have three columns showing only the error, without showing the output image.

| N    | <C, M, Q1, Q3, Q5> | Output Image | Error |
| ---- | ------------------ | ------------ | ----- |
| 6    | <2,1,4,1,1>        | (Image)      |       |
| --   | --                 | --           | --    |
# Dynamic-LPBoost-for-TCR-Classification

To run the code you will need to install Matlab toolbox CVX. Download and documentation can be found at the website: http://cvxr.com/cvx/.


Description of functions:

1. Data Processing
(1). DataProcessing.py
A python file to compute the p-spectrum string kernel between substring of length p and amino acid documents.

Please note data generated by DataProcessing.py has NOT been normalised. For a simple p-spectrum kernel of length p in our experiment, the normalised data matrix can be computed by the following code:

data_norm = bsxfun(@ridivide, data, sqrt(sum(data.^2, 2)))

where data_norm is normalised data matrix.


2. LPBoost
This folder contains functions of LPBoost with explicit feature space.
(1) LPBoostYS.m
A Matlab funtion to perform LPBoost. Please note that since the data matrix contains only non-negative values, we duplicate the matrix data_dup = [data_norm, -data_norm] and use data_dup in LPBoost.

(2) LPcvx.m
A Matlab function to perform convex optimisation during LPBoost iterations.


3. Dynamic Programming LPBoost
This folder contains functions of LPBoost, where the features are selected by an efficient dynamic programming procedure.

(1) dynamicLPBoostUnnorm.m
A Matlab function that calls dynamic programming technique during LPBoost iterations.

(2) dynamicPosNegUnnorm.m
A Matlab function that select over matrix data_norm and -data_norm, and returns the feature (either positive or negative) that can give the maximum in LPBoost.

(3) dynamicPUnnorm.m
A Matlab function that performs dynamic programming given data_norm.

(4) featSelectUnnorm.m
A Matlab function that returns the kernels of selected substrings.


4. SampleCode.m
A Matlab script that shows the steps of both LPBoost and dynamic LPBoost. Please note this script does NOT contain code for LPBoost in conjunction with SVM. A better performance can be achieved by using the features selected by LPBoost in SVM.


5. Varying Transition Probabilities (not used anymore)
This folder contains function of dynamic programming LPBoost over Fisher kernels. Functions inside this folder is not used anymore and will be replaced by dynamic programming over the DAG in the future.


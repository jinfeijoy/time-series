# Notes for Sequence, Time series, and Prediction

## Week3
* Shape of the inputs to the RNN:
  * ![image](https://user-images.githubusercontent.com/16402963/210624921-74fd7164-9e84-4732-a01f-c9892e342270.png)
  * units: dimension of output, the more units, model is more complicated with more parameters. 
  * return_sequence: 
    * true: sequence to sequence 
       * ![image](https://user-images.githubusercontent.com/16402963/210625421-8405e618-1c5c-4cc4-b961-313f6438f0a0.png)
    * false: sequence to vector  
       * ![image](https://user-images.githubusercontent.com/16402963/210625507-b8f5e3b7-cdb8-4882-a59a-0ddffdf11504.png)
    * dense: sequence to vector only output single dense, while senquence to sequence output multiple dense
       * ![image](https://user-images.githubusercontent.com/16402963/210625839-cceb8776-0211-493e-be0e-ed7f6b83c2cf.png)
       * ![image](https://user-images.githubusercontent.com/16402963/210625921-cdd6a9d3-1652-47c6-9b81-30de83c83513.png)
* Adjusting the learning rate dynamically
  * tune learning rate to find out best learning rate
    * ![image](https://user-images.githubusercontent.com/16402963/210627316-a46392b5-2c24-458a-b44f-493666bb6e82.png) 
  * find out best epoc based on mae 
     * ![image](https://user-images.githubusercontent.com/16402963/210627404-b854b90d-ce84-497d-8f7e-90d40788ab0f.png)
* [Huber loss function](https://en.wikipedia.org/wiki/Huber_loss): less sensitive to outliers than squared loss and absolute loss. 
  * Two very commonly used loss functions are the squared loss, {\displaystyle L(a)=a^{2}}L(a) = a^2, and the absolute loss, {\displaystyle L(a)=|a|}L(a)=|a|. The squared loss function results in an arithmetic mean-unbiased estimator, and the absolute-value loss function results in a median-unbiased estimator (in the one-dimensional case, and a geometric median-unbiased estimator for the multi-dimensional case). The squared loss has the disadvantage that it has the tendency to be dominated by outliers—when summing over a set of {\displaystyle a}a's (as in {\textstyle \sum _{i=1}^{n}L(a_{i})}{\textstyle \sum _{i=1}^{n}L(a_{i})}), the sample mean is influenced too much by a few particularly large {\displaystyle a}a-values when the distribution is heavy tailed: in terms of estimation theory, the asymptotic relative efficiency of the mean is poor for heavy-tailed distributions.
  * As defined above, the Huber loss function is strongly convex in a uniform neighborhood of its minimum {\displaystyle a=0}a=0; at the boundary of this uniform neighborhood, the Huber loss function has a differentiable extension to an affine function at points {\displaystyle a=-\delta }a=-\delta  and {\displaystyle a=\delta }a=\delta . These properties allow it to combine much of the sensitivity of the mean-unbiased, minimum-variance estimator of the mean (using the quadratic loss function) and the robustness of the median-unbiased estimator (using the absolute value function). 
* RNN, GRN
  * ![IMG_0220](https://user-images.githubusercontent.com/16402963/210908414-f3fb9e26-13b3-46fe-bf60-17035c466c2a.JPG) 
* LSTM
  *  ![IMG_0221](https://user-images.githubusercontent.com/16402963/210908428-fed00513-7f19-450a-ac45-8e5f1822e399.JPG)
## Week 4
* Mini batch: for regular batch, 1 epoch will have 1 gradient descent, for mini batch, 1 epoch will have multiple gradient descent (n_gradient = N/batch_size)

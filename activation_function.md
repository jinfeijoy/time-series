# Activation Function

* All hidden layers usually use the same activation function. However, the output layer will typically use a different activation function from the hidden layers. The choice depends on the goal or type of prediction made by the model.
* Purpose of activation function: add non-linearity to the neural network
* if we cannot get an output from neural network, which means the gradient is too small

## 3 Types of neural networks activation functions
### Binary step function
    * <img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60be0e9ab5cab603f27e8f4a_math-20210607%20(3).png"  width="120" height="100">
    * limitation: 
        * cannot provide multi-value outputs - for example, it cannot be used for multi-class classification
        * The gradient of the step function is 0, which cause a hindrance in the backpropagation process
### Linear activation function (just simple linear regression model)
    * limitation:
        * not possible to use backpropagation as the derivative of the function is a constant and has no relation to the input x
        all layers of the neural network will collapse into 1 if a linear activation function is used. So, essentially, a linear activation function turns the neural network into just 1 layer.
### Non-Linear activation functions (10 functions)
* Sigmoid/Logistic
    * <img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60be196326da6e49a7a15661_math-20210607%20(7).png"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d24547f85f71e3bd2339f8_pasted%20image%200%20(5).jpg"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d2458396cfc63d0a02b0c8_pasted%20image%200%20(6).jpg"  width="120" height="100">
    * Input: any value
    * Output: 0-1
    * Commenly Use: to predict the probability as an output
    * Limitation: 
        * The derivative of the function is , the gradient values are only significant for range -3 to 3, it implies that for values >3 or <-3, the function will have very small gradients.
        * The output of the logistic function is not symmetric (对称) around zero, so the output of all the neurons will be of the same sign. This makes the training of the neural network more difficult and unstable.
* Tanh Function (Hyperbolic Tangent)
    * <img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60be1a9bac9b73842964585e_math-20210607%20(8).png"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d246555e0bd43f4bf17b77_Group%2022.jpg"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d245b38d468ca69828e8f5_pasted%20image%200%20(7).jpg"  width="120" height="100">
    * Input: any value
    * Output: zero centered -> we can easily map the output values as strongly negative, neutral, or strongly positive
    * Commenly Use: usually used in hidden layers of a neural network as its values lie between -1 to 1, therefore, (gradients is large in central and makes the training of the neural network easier)
    * Limitation:
        * it face the same prorblem of vanishing gradients similar to the sigmoid activation function. And the gradient of the tanh function is much steeper as compared to the sigmoid function.
        * tanh is zero centered, and the gradients are not restricted to move in a certain direction. Therefore, in practice, tanh nonlinearity is always preferred to sigmoid nonlinearity
* ReLU Function (Rectified Linear Unit)
    * <img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60be1b236a3731df9b1d43c9_math-20210607%20(11).png"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d24d1ac2cc1ded69730feb_relu.jpg"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d2472c7c7683854f329e45_pasted%20image%200%20(9).jpg"  width="120" height="100">
    * Input: any value
    * Output: (the neurons will only be deactivated if the output of the linear transformation is less than 0)
    * Commenly Use: since only a certain number of neurons are activated, the ReLU function is far more computationally efficient. ReLU accelerates the convergence of gradient descent towawrds the global minumum of the loss function due to its linear, non-saturating property
    * limitation:
        * all the negative input values become zero immediatly, which decrease the model's ability to fit  or trian from the data properly
        * Dying ReLU: NOT able for backpropagation
* Leaky ReLU
    * <img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60be1b96b195d1119c30eddf_math-20210607%20(12).png"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d2474e3a0f7a4010b6129e_pasted%20image%200%20(10).jpg"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d248619e91e2238803bb97_pasted%20image%200%20(11).jpg"  width="120" height="100">
    * Input: any value
    * Output: it has a small positive slope in the negative area
    * Common Use: same as Relu, but also enable backpropagation. 
    * Limitation: 
        * predictions may not be consistent for negative input values
        * the gradient for negative values is a small value that makes the learning of model parameters time-consuming
* Parametric ReLU
    * <img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60be2bc6703d396502ae28b2_math-20210607%20(21).png"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d24887a3d0cc7966aa0aa7_pasted%20image%200%20(12).jpg"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d248d0a17eb381ecce9489_pasted%20image%200%20(13).jpg"  width="120" height="100">
    * Input: any value
    * Output: 
    * Common Use: The parameterized ReLU function is used when the leaky ReLU function still fails at solving the problem of dead neurons, and the relevant information is not successfully passed to the next layer.
    * Limitation: it may perform differently for different problems depending upon the value of slope parameter a.
* ELUs (Exponential Linear Units)
    * <img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60be1d44cdd90474e0430225_math-20210607%20(14).png"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d248d0a17eb381ecce9489_pasted%20image%200%20(13).jpg"  width="120" height="100"><img src="https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/60d248fe0377d17681762682_pasted%20image%200%20(14).jpg"  width="120" height="100">
    * Commen Use: ELU becomes smooth slowly until its output equal to -alpha whereas RELU sharply smoothes. Avoid dead ReLU by introducing log curve for negative values of input. It helps the network nudge weights and biases in the right direction
    * Limitation:
        * increase computational time because of the exponential operation included
        * No learning of alpha value takes place
        * Exploding gradient problem
* Softmax Function

## Reference
* [Activation Functions in Neural Networks [12 Types & Use Cases]](https://www.v7labs.com/blog/neural-networks-activation-functions#:~:text=An%20Activation%20Function%20decides%20whether,prediction%20using%20simpler%20mathematical%20operations.)
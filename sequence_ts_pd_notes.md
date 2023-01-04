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
* Huber loss function: less sensitive to outliers  

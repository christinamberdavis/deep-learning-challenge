# Overview 
The nonprofit foundation Alphabet Soup wants a tool that can select applicants for funding with the best chance of success in their ventures. Alphabet Soup will use the tool to help predict which applicants are likely to be successful and therefore should be given funding. 

The dataset consists of over 34,000 applicants who have applied to Alphabet Soup in the past and whether their venture was successful or not. 

* EIN and NAME: Identification columns
* APPLICATION_TYPE: Alphabet Soup application type
* AFFILIATION: Affiliated sector of industry
* CLASSIFICATION: Government organization classification
* USE_CASE: Use case for funding
* ORGANIZATION: Organization type
* STATUS: Active status
* INCOME_AMT: Income classification
* SPECIAL_CONSIDERATIONS: Special considerations for application
* ASK_AMT: Funding amount requested
* IS_SUCCESSFUL: Was the money used effectively

# Results: 
I was unable to achieve 75% accuracy. 


## Data Preprocessing

* What variable(s) are the target(s) for your model?
The target variable is: 
    * IS_SUCCESSFUL: Was the money used effectively

* What variable(s) are the features for your model?
Features used to determine the success of an applicant are: 
    * APPLICATION_TYPE: Alphabet Soup application type
    * AFFILIATION: Affiliated sector of industry
    * CLASSIFICATION: Government organization classification
    * USE_CASE: Use case for funding
    * ORGANIZATION: Organization type
    * INCOME_AMT: Income classification
    * SPECIAL_CONSIDERATIONS: Special considerations for application
    * ASK_AMT: Funding amount requested

* What variable(s) should be removed from the input data because they are neither targets nor features?
Removed variables are: 
    * EIN: This is a randomly generated identifier for each applicant and therefore has no value in determining the applican't success.
    * NAME: Name is another identifier that has no bearing on the rest of the application data, and therefore I removed it.
    * STATUS: This indicates if the application is active or not. Because this is really tied to the application. process and not to the venture's industry, classification, or other venture-specific data, I did not include it in any model. 

## Compiling, Training, and Evaluating the Model

* How many neurons, layers, and activation functions did you select for your neural network model, and why?
    ### Original Model
        * Neurons: The initial input layer includes dummies for each ASK_AMT, which makde for a very large feature set. The initial input layer neurons accounts for each of those features. Additional layers reduce this number drastically.
            * Initial input layer: 8787
            * Hidden layer 1: 80
            * Hidden layer 2: 30
            * Total: 8897
        * Layers: 3 (initial input layer + 2 hidden layers)
        * Activation functions: Relu and sigmoid functions were chosen because the target is binary and feature values are positive. 
            * Initial input layer: relu
            * Hidden layer 1: relu
            * Hidden layer 2: sigmoid
        * Optimizer: adam
        * Results: Loss: 0.9265857338905334, Accuracy: 0.7149854302406311
### Optimization 1
* Neurons: The initial input layer for this optimization does not include dummies for ASK_AMT, so the total number of features is significantly less than the original model. I added an additional neuron to hidden layer 1 simply to see what would happen, and added an additional hidden layer to see if that produced more accurate results. 
     * Initial input layer: 49
     * Hidden layer 1: 50
     * Hidden layer 2: 30
     * Hidden layer 3: 10
     * Total: 139
* Layers: 4 (initial input layer + 3 hidden layers)
* Activation functions: I tried relu in the initial and first 2 hidden layers but swtiched to sigmoid to see if that would help increase accuracy. 
     * Initial input layer: relu
     * Hidden layer 1: relu
     * Hidden layer 2: relu
     * Hidden layer 3: sigmoid
* Optimizer: adam
* Results: Loss: 0.5614355802536011, Accuracy: 0.7325947284698486

The results for Optimization 1 are 2 points higher than the original model. 

    ### Optimization 2
        * Neurons: I added more CLASSIFICATION and APPLICATION_TYPE features, but removed ASK_AMT and SPECIAL_CONSIDERATIONS to see if this would have any impact on the results. I started with 67 features, which I used for the number of neurons in the initial input layer. 
            * Initial input layer: 67
            * Hidden layer 1: 68
            * Hidden layer 2: 40
            * Hidden layer 3: 10
            * Total: 185
        * Layers: 4 (initial input layer + 3 hidden layers)
        * Activation functions: I tried all sigmoid to see if that would help increase accuracy. 
            * Initial input layer: sigmoid
            * Hidden layer 1: sigmoid
            * Hidden layer 2: sigmoid
            * Hidden layer 3: sigmoid
        * Optimizer: sgd
        * Results:  Loss: 0.563554584980011, Accuracy: 0.728396475315094

The accuracy for Optimization 2 is better than the original model but worse than Optimization 1. 

    ### Optimization 3
        * Neurons: I dropped CLASSIFICATION, ASK_AMT and SPECIAL_CONSIDERATIONS to see if this would have any impact on the results. I kept the same APPLICATION_TYPE features as Optimizer 2. I started with 67 features, which I used for the number of neurons in the initial input layer. 
            * Initial input layer: 30
            * Hidden layer 1: 42
            * Hidden layer 2: 21
            * Hidden layer 3: 10
            * Total: 103
        * Layers: 4 (initial input layer + 3 hidden layers)
        * Activation functions: I alternated relu and sigmoid.
            * Initial input layer: relu
            * Hidden layer 1: sigmoid
            * Hidden layer 2: relu
            * Hidden layer 3: sigmoid
        * Optimizer: adam
        * Results:  Loss: 0.571895182132721, Accuracy: 0.7259474992752075
    
    The results were slightly worse than Optimization 2. 

    ### Optimization 4
        * Neurons: I used the same preproccessing as Optimization 2 for a total of 70 features. I doubled the number of neurons in the first input layer because the best optimizations use 2-3 times the number of features. I added 2 additional layers to see if I could get more accurate results. 
            * Initial input layer: 70
            * Hidden layer 1: 140
            * Hidden layer 2: 70
            * Hidden layer 3: 35
            * Hidden layer 4: 18
            * Hidden layer 5: 9
            * Total: 342 
        * Layers: 6 (initial input layer + 5 hidden layers)
        * Activation functions: I used sigmoid for all layers
            * Initial input layer: sigmoid
            * Hidden layer 1: sigmoid
            * Hidden layer 2: sigmoid
            * Hidden layer 3: sigmoid
            * Hidden layer 4: sigmoid
            * Hidden layer 5: sigmoid
        * Optimizer: adam
        * Results:  Loss: 0.5630967617034912, Accuracy: 0.7278134226799011
    
* Were you able to achieve the target model performance?
    I was not able to achieve the target model performance. I think the dataset is simply too small.

* What steps did you take in your attempts to increase model performance?
    * I changed preprocessing to increase or reduce the number of features. 
    * I changed the number of hidden layers. 
    * I changed the number of neurons. 
    * I changed the activation functions. 
    * I changed the optimizer. 
    * See above for the configurations of the original model and each optimization. 

# Summary
The best results of these was Optimization 1, but barely so. There was not a significant difference between the original model and the 4 optimizations. I think the limitation is that the dataset is still very small, only 34,000 records. I recommend continuing to collect data and fine-tune the model over time to achieve more accurate results. 

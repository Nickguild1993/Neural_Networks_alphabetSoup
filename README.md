# Exploring Neural Networks, Module 19.


## Overview of the analysis

The purpose of this analysis was to create a model that could be trained on prior projects that AlphabetSoup had funded and better understand what parameters/features of a company hold predictive value for determining if going forward with a monetary investment in company X is prudent. If the model we build is successful in predicting whether a company is a good investment or not, AlphabetSoup will be able to allocate it's finanical resources much more efficiently leading begetting not only more positive outcomes, but also *reducing* negative outcomes that end up being cash burns.  

## Results: 

### Data Preprocessing
What variable(s) are considered the target(s) for your model?

- the target variable was **IS_SUCCESSFUL** as that determines in a binary manner whether the money was a wise investment or not. 

What variable(s) are considered to be the features for your model?

- The features that I thought would be predictive are the following: - **APPLICATION_TYPE, AFFILIATION, INCOME_AMOUNT, SPECIAL_CONSIDERATIONS, ASK_AMOUNT, STATUS, USE_CASE, CLASSIFICATION and ORGANIZATION** 

What variable(s) are neither targets nor features, and should be removed from the input data?

- I removed the following two columns because they should have zero effect on whether the investment is successful or not: **EIN** and **NAME**.  
- Additionally, after merging the *one-hot encoded* features with the original dataframe, I removed the following **INCOME_AMT** bins: **INCOME_AMT_1M-5M, INCOME_AMT_5M-10M, INCOME_AMT_10M-50M, INCOME_AMT_50M+.  
The reason being is that there were no companies that requested funding that reported income in those ranges, so their continued presence wasn't helpful and could of even been unhelpful in training my model. In order to test if those **INCOME_AMOUNT** columns truly were without any non-zero values, I ran the following line of code to find the max value in that particular column, for example: ``app_df["INCOME_AMT_1M-5M"].max``  If the max value returned was 0, that meant that there are no companies who reported an income within that range (if they did, they would have a value of 1 instead).  Below is a screenshot of how the code looks in my jupyter notebook.

![Alt_Text](https://github.com/Nickguild1993/Neural_Networks_M19/blob/main/M19_removal_income_columns.png)
      

### Compiling, Training, and Evaluating the Model

![Alt_img](https://github.com/Nickguild1993/Neural_Networks_M19/blob/main/M19_model_table_excel.png)

- As viewable in the excel table above, I tried six different variations of neurons, layers, epochs and features to try to reach the target model performance of 75%.  Disappointingly, each iteration I tried failed to reach that threshold.  For my original neural network model I chose 12 neurons for my first hidden layer, and then 8 for my second hidden layer.  I used Relu for my activation function in the hidden layers and then sigmoid for the output layer.  I based the parameters on what we had done so far in the module, and in retrospect, I think maybe in retrospect I should've started out with more neurons given the number of input features I had was 42.  The decisions to use Relu and Sigmoid also just came from using them in the past consistently- I tried using the **LEAKY ReLU** in place of Relu and I just couldn't get it to run.  I tried a bunch of different ways to import it, and each time it kept throwing me an error, so after trying to utlize the Leaky version, I just went with the normal Relu one.

Were you able to achieve the target model performance?

- No, I was unable to reach the target model performance.  Honestly, the improvements I did make were so negligible that it was deflating.  I must be missing something.

What steps did you take to try and increase model performance?

- The first attempt at optimization involved removing the **INCOME_AMOUNT** features that had zero values in them (There weren't any companies that received funding from AlphabetSoup with incomes in the range of those (4) columns from $1,000,000 to $50,000,000).  That removal ended up not changing the outcome by almost anything at all. 
- So then I thought that perhaps there were too few neurons in the hidden layers, and that by adding more to (what was at first, 2 hidden layers) those layers, I would be able to return a higher accuracy score.  This, like the overall theme of my optimization attempts, was a failure to raise the score enough. Even when I added a 3rd hidden layer on the *third* optimization attempt, I could not get above 75%. Then I thought that perhaps the model wasn't getting enough training so I increased the epochs from 50 to 75 for optimization attempt number 4.  Sadly, increassing the number of epochs in my model literally almost nothing to improve the score. (For the last two atttempts I switched back to 50 epochs).  The last two optimizations I tried were to again increase the neuron count across the (3) hidden layers.  Even going up to 24 in the first layer, 18 in the second, and 15 in the third (like I did on the 6th and final attempt) did little more than change a digit in the ten thousands place. 

Summary:  

![Alt_Img](https://github.com/Nickguild1993/Neural_Networks_M19/blob/main/M19_Optimization3_best_result.png)

- Above are the results from evaluating the test data during my third and most successful optimization.  It's right at 73% accuracy, I just couldn't get those last two percentage points to reach the goal.  Perhaps instead of using a deep neural netowrk I would try to use a SVM (Support Vector Machine) which would be an ideal model to use here because at the core of what we're trying to figure out here is a binary classification- are companies that AlphabetSoup gives money to successful or not?  SVMs excell at solving binary classifcation problems, and since I'm at a loss of how to better improve the deep neural network, maybe the more macro viewed approach of an SVM (which doesn't get hyper-focused on specific trends) will be able to identify broad trends that will lead to a much higher accuracy score which in turn will allow us to create a model that is much more predicitive when it comes to determining which applying companies represent investments that will pan out.

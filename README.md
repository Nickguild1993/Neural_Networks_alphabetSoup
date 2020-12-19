# Neural_Networks_M19


# Overview of the analysis

The purpose of this analysis was to create a model that could be trained on prior projects that AlphabetSoup has funded and better understand what parameters/features of a company hold predictive value for determining if going forward with a monetary investment in company X is prudent. If the model we build is successful in predicting whether a company is a good investment or not, AlphabetSoup will be able to allocate it's finanical resources much more efficiently leading begetting not only more positive outcomes, but also *reducing* negative outcomes that end up being cash burns.  

# Results: Using bulleted lists and images to support your answers, address the following questions.

### Data Preprocessing
What variable(s) are considered the target(s) for your model?
- the target variable was **IS_SUCCESSFUL** as that determines in a binary manner whether the money was a wise investment or not. 
What variable(s) are considered to be the features for your model?
- The features that I thought would be predictive are the following: - **APPLICATION_TYPE, AFFILIATION, INCOME_AMOUNT, SPECIAL_CONSIDERATIONS, ASK_AMOUNT, STATUS, USE_CASE, CLASSIFICATION and ORGANIZATION. **
What variable(s) are neither targets nor features, and should be removed from the input data?
- I removed the following two columns because they should have zero effect on whether the investment is successful or not: **EIN** and **NAME**.  
- Additionally, after merging the *one-hot encoded* features with the original dataframe, I removed the following **INCOME_AMT** bins: **INCOME_AMT_1M-5M, INCOME_AMT_5M-10M, INCOME_AMT_10M-50M, INCOME_AMT_50M+.  
The reason being is that there were no companies that requested funding that reported income in those ranges, so their continued presence wasn't helpful and could of even been unhelpful in training my model.
         ****IMAGE HERE OF REMOVING THOSE COLUMNS****

### Compiling, Training, and Evaluating the Model

How many neurons, layers, and activation functions did you select for your neural network model, and why?

    ****IMAGE OF EXCEL TABLE HERE****
- As viewable in the excel table above, I tried six different variations of neurons, layers, epochs and features to try to reach the target model performance of 75%.  Disappointingly, each iteration I tried failed to reach that threshold. 

Were you able to achieve the target model performance?

- No, I was unable to reach the target model performance.  Honestly, the improvements I did make were so negligible that it was deflating.  I must be missing something.

What steps did you take to try and increase model performance?

- The first attempt at optimization involved removing the **INCOME_AMOUNT** features that had zero values in them (There weren't any companies that received funding from AlphabetSoup with incomes in the range of those (4) columns from $1,000,000 to $50,000,000).  That removal ended up not changing the outcome by almost anything at all. 
- So then I thought that perhaps there were too few neurons in the hidden layers, and that by adding more to (what was at first, 2 hidden layers) those layers, I would be able to return a higher accuracy score.  This, like the overall theme of my optimization attempts, was a failure to raise the score enough. Even when I added a 3rd hidden layer on the *third* optimization attempt, I could not get above 75%. Then I thought that perhaps the model wasn't getting enough training so I increased the epochs from 50 to 75 for optimization attempt number 4.  Sadly, increassing the number of epochs in my model literally almost nothing to improve the score. (For the last two atttempts I switched back to 50 epochs).  The last two optimizations I tried were to again increase the neuron count across the (3) hidden layers.  Even going up to 24 in the first layer, 18 in the second, and 15 in the third (like I did on the 6th and final attempt) did little more than change a digit in the ten thousands place. 

Summary: Summarize the overall results of the deep learning model. Include a recommendation for how a different model could solve this classification problem, and explain your recommendation.  

        *****INSERT PNG OF OP 3 RESULTS HERE*****
- Above are the results from evaluating the test data during my third and most successful optimization.  It's right at 73% accuracy, I just couldn't get those last two percentage points to reach the goal.

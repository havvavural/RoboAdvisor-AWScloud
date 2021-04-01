# The Power of the Cloud and Unsupervised Learning

### Robo Advisor for Retirement Plans

![Robot](Images/robot.jpg)

*Photo by [Alex Knight](https://www.pexels.com/@alex-knight-1272316?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/high-angle-photo-of-robot-2599244/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) | [Free License](https://www.pexels.com/photo-license/)*

### Background

A prominent retirement plan providers in the country want to increase their client portfolio, especially by engaging young people. Since machine learning and NLP are disrupting finance to improve customer experience, I decided to create a robo advisor that could be used by customers or potential new customers to get investment portfolio recommendations for retirement.
In this project, I will combine your new Amazon Web Services skills with Python superpowers, to create a bot that will recommend an investment portfolio for a retirement plan.

Main tasks:


Initial Robo Advisor Configuration: Define an Amazon Lex bot with a single intent that establishes a conversation about the requirements to suggest an investment portfolio for retirement.


Build and Test the Robo Advisor: Make sure that your bot is working and responding accurately along with the conversation with the user, by building and testing it.


Enhance the Robo Advisor with an Amazon Lambda Function: Create an Amazon Lambda function that validates the user's input and returns the investment portfolio recommendation. This task includes testing the Amazon Lambda function and making the integration with the bot.

### Packages Used:

* Amazon Lex [Amazon Lex Bot](https://aws.amazon.com/lex/)
* Lambda [Amazon Lambda](https://aws.amazon.com/lambda/)

### Files

* [lambda_function.py](Starter_Files/lambda_function.py)
* [correct_dialog.txt](Test_Cases/correct_dialog.txt)
* [age_error.txt](Test_Cases/age_error.txt)
* [incorrect_amount_error.txt](Test_Cases/incorrect_amount_error.txt)
* [negative_age_error.txt](Test_Cases/negative_age_error.txt)

---

#### Tasks Performed:

<details>
<summary>Initial Robo Advisor Configuration</summary>

<br>1. Define an Amazon Lex Bot with a single intent that establishes a conversation about the requirements to suggest an investment portfolio for retirement</br>

<br>2. Sign in into AWS Management Console and create a new custom Amazon Lex bot `RoboAdvisor`.</br>

<br>3. Setup the following parameters:</br>
* **Bot name:** RoboAdvisor
* **Output voice**: Salli
* **Session timeout:** 5 minutes
* **Sentiment analysis:** No
* **COPPA**: No

<br>4. Create the `RecommendPortfolio` intent, and configure some sample utterances as follows: </br>
* I want to save money for my retirement
* I'm ​`{age}​` and I would like to invest for my retirement
* I'm `​{age}​` and I want to invest for my retirement
* I want the best option to invest for my retirement
* I'm worried about my retirement
* I want to invest for my retirement
* I would like to invest for my retirement

<img src="Images/sample_utterances.png" width="500" />  

<br>5. Slots used by the bot, three using built-in types and one custom slot named `riskLevel`. The three initial slots as follows:</br>

| Name             | Slot Type            | Prompt                                                                    |
| ---------------- | -------------------- | ------------------------------------------------------------------------- |
| firstName        | AMAZON.US_FIRST_NAME | Thank you for trusting on me to help, could you please give me your name? |
| age              | AMAZON.NUMBER        | How old are you?                                                          |
| investmentAmount | AMAZON.NUMBER        | How much do you want to invest?                                           |

  <br> The `riskLevel` custom slot will be used to retrieve the risk level the user is willing to take on the investment portfolio; create this custom slot as follows:</br>

   > * **Name:** riskLevel
   > * **Prompt:** What level of investment risk would you like to take?
   > * **Maximum number of retries:** 2
   > * **Prompt response cards:** 4

<img src="Images/slots.png" width="500" />

<br>Configure the response cards for the `riskLevel` slot as is shown bellow:</br>

| Card 1                              | Card 2                              |
| ----------------------------------- | ----------------------------------- |
| <img src="Images/card1.png" width="400" />  | <img src="Images/card2.png" width="400" />  |

| Card 3                              | Card 4                              |
| ----------------------------------- | ----------------------------------- |
| <img src="Images/card3.png" width="400" />  | <img src="Images/card4.png" width="400" />  |


<br>6. Move to the *Confirmation Prompt* section, and set the following messages:</br>
   * **Confirm:** Thanks, now I will look for the best investment portfolio for you.
   * **Cancel:** I will be pleased to assist you in the future.

<br>7. Leave the error handling configuration for the `RecommendPortfolio` bot with the default values.</br>

<img src="Images/error_handling.png" width="500" />

</details>


<details>
<summary>Build and Test the Robo Advisor</summary>
<br>Build the bot and test it in the chatbot window to ensure accurate user conversation.</br>

</details>

<details>
<summary>Enhance the Robo Advisor with an Amazon Lambda Function</summary>

<br>1. Create an Amazon Lambda function `recommend_portfolio()` to validate the data provided by the user on the RoboAdvisor.</br>

<br>2. Starter code provided on [lambda_function.py](Starter_Files/lambda_function.py)</br>
    
<br>3. User input Validation guidelines to complete `recommend_portfolio()`</br>
* The `age` should be greater than 21 and less than 65.
* the `investment_amount` should be equal to or greater than 5000.

<br>4. Investment Portfolio Recommendation based on the selected risk level criteria, response from the bot should be as:</br>
* **none:** "100% bonds (AGG), 0% equities (SPY)"
* **very low:** "80% bonds (AGG), 20% equities (SPY)"
* **low:** "60% bonds (AGG), 40% equities (SPY)"
* **medium:** "40% bonds (AGG), 60% equities (SPY)"
* **high:** "20% bonds (AGG), 80% equities (SPY)"
* **very high:** "0% bonds (AGG), 100% equities (SPY)"

<br>5. Test the Lambda function using the [sample test cases](Test_Cases/) provided.</br>

<br>6. Open the Amazon Lex Console and navigate to the `RecommendPortfolio` bot configuration, integrate the lambda function `recommend_portfolio()` by selecting it in the _Lambda initialization and validation_ and _Fulfillment_ sections.</br>


---


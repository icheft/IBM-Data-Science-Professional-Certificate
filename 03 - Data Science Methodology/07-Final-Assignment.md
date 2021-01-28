# Final Assignment

In this Assignment, you will demonstrate your understanding of the data science methodology by applying it to a given problem. Pick one of the following topics to apply the data science methodology to:

1. Emails
2. Hospitals
3. Credit Cards

You will have to play the role of the client as well as the data scientist to come up with a problem that is more specific but related to these topics.



## Project Title

## Which topic did you choose to apply the data science methodology to? (2 marks)

Next, you will play the role of the client and the data scientist. 

> I have chosen Emails as my topic since sorting and reading all emails in the inbox is generally tedious and time wasting. 
## Using the topic that you selected, complete the Business Understanding stage by coming up with a problem that you would like to solve and phrasing it in the form of a question that you will use data to answer. (3 marks)

You are required to:

1. Describe the problem, related to the topic you selected.
2. Phrase the problem as a question to be answered using data.

For example, using the food recipes use case discussed in the labs, the question that we defined was, *"Can we automatically determine the cuisine of a given dish based on its ingredients?"*.

> As mentioned in the previous section, sorting, reading, organizing, etc. emails in our inbox can be tedious as the number of emails increases. It would be optimal and more efficient for us, if we can automate the process of organizing those emails and determine which emails are worth dealing with, We can categorize the emails into "important", "spam", "miscellaneous", "social", "ads", "receipts", and so on. In Google's email service, it is categorized into "primary", "social", "updates", "promotions", and "forums".
> 
> So, the question here is *"Can we classify/organize the emails into different categories based on its email address and contents?"*

## Briefly explain how you would complete each of the following stages for the problem that you described in the Business Understanding stage, so that you are ultimately able to answer the question that you came up with. (5 marks):

1. Analytic Approach
2. Data Requirements
3. Data Collection
4. Data Understanding and Preparation
5. Modeling and Evaluation

> 1. Analytic Approach
>       Since there is a yes-or-no answer to each email, we can build a decision tree and use a classification model.
> 2. Data Requirements
>       As mentioned, the data required for the analysis include email address (account name, domain, etc.), subject, contents (texts), contexts (the number of emails in one's inbox), time, mailing list sender, attachment, etc. 
> 3. Data Collection
>       On an individual level, we can collect one's personal emails prior to date. For mass analysis on a more general level, we can collect emails from different individuals, with each email labeled as one of the categories we wish to identify. 
> 4. Data Understanding and Preparations 
>       We shall remove the redundant entries. Also, if the same email from the same providers appear more than once in our merged data set, we can first accumulate the duplicate emails, and then preserve only the first appearance of the mail. 
> 5. Modeling and Evaluation                         >        At this step, we build the classification model. It can be done with a decision tree discussed in the lecture. We would draw some entries out from the sample as our testing data with the rest being the training data. 
You can always refer to the labs as a reference with describing how you would complete each stage for your problem.
>       After modeling and deployment, we need to gather feedbacks and seek possible manipulations or refinement and perform necessary changes to our data or model in order to ensure a more optimal results.                                                     
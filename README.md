# Why Are People Anti-Work?

## Shania Thomas


## Background

Latent Dirichlet Allocation (LDA) is topic modeling using Natural Language Processing which finds hidden, latent, topics within bodies of text. Documentation for LDA can be found [here](https://radimrehurek.com/gensim/models/ldamulticore.html). In overview, LDA uses direchlet algorithms to find distributions of words, and then distributions of those words over topics. The model outputs probabilities that the document belongs to each topic (because every document belongs to every topic, but there is one topic that will have the highest probability), and probabilities that each word denotes the topic.

## Problem Statement

This model is applied to the subreddit r/Antiwork which contains posts centered around employee concerns. The problem I attack using this model is:

> *What are the root causes of employees being unhappy at their workplaces? Have these been recurring issues, or have they changed over time?*

## Methods

#### Data
The dataset was downloaded from Kaggle and includes posts from r/Antiwork's inception in August 2013, up until February 2022. 

#### Preprocessing

After cleaning and EDA which showed exponential increase in posts beginning in 2019, I used Gensim & Regex libraries to tokenize, NLTK libraries to stem and lemmatize tokens, as well as to include stop words.

#### Modeling

The first parameter of the LDA model is the dictionary. Using the .Dictionary method, Gensim sweeps through the corpus, giving each token an ID. Secondly, the model needs a corpus which is a vector. Using the .doc2bow() method, Gensim converts each document into a vector the size of however many unique tokens there are in the corpus. The corpus output is then a list of tuples. The last required parameter for model training is the number of topics. When training, I trained with 3-5 topics depending on topic overlap.

I trained an LDA model on the entire corpus with posts from 2013-2022, then on the individual years of 2019, 2020, and 2021, I chose these years because 2019 is when the exponential increase began, and I was curious if the pandemic or other world events had an effect on the topics. I visualized the results of each model using the pyLDAvis package.

#### Reading the pyLDAvis

pyLDAvis is a visualization method used to simplify visualizing the topics the LDA model produces. On the left side of the visual, each circle represents a topic where the larger the circle, the more documents the topic has so to speak. The closer the circles are, the more closely related the topics are. If there is overlap, the topics have something in common.

On the right side, the most common terms are shown. If no topic is selected, it's the most common terms of the whole corpus. When you select a topic from the left, the terms most prevalent to that topic appear. The red bar is showing how the frequency of that term within that topic, whereas the blue bar is showing the term frequency within the corpus. If you hover/click a term, the topic circles where that term is found grow larger. The larger the circle, the more frequently that word is in that topic.

The relevance metric slider, denoted lambda, ranges on a scale of 0.0 to 1.0. As you move the scale towards 0, the terms that will appear are more exclusive to the topic that is selected meaning you will start to see more red bars. As the scale is moved toward 1, the terms that appear are not only relevant to the topic, but to the corpus as a whole.

## Conclusions
All in all, there are three recurring root causes of employees being unhappy at their workplaces. The most consistent topics were the employees' time, financial stability, and systemic concerns within their workplace. The concerns of time were incredibly and profoundly consistent, whereas the concerns of financial stability had slight change throughout the years, and the systemic concerns varied as the years went on. Below are specific conclusions and recommendations on these concerns.
The topic of time was the #1 topic in the entire corpus, and consistently the number 1 topic in every model for the years 2019-2021. Terms that continuously appeared when discussing time were:
- day, 
- hour, 
- week, 
- shift, 
- time, 
- home, 
- sick,  
- break
- sleep, 
- weekend, 
- mental, and
- month

Potential recommendations for an employer to handle the concern of employees' time could first be to have clear and strict working hours. If your company has working hours of 8 am to 5 pm Monday through Friday, encourage and support clocking out at 5 pm. If its noticed work is still being done after 5 pm, an employer could ask what support they could provide in assisting the employee in accomplishing their tasks and goals within the work day. This build to another recommendation of ensuring an employer is being cognizant of their time when providing tasks, scheduling meetings, etc. For example, if tasks and responsibilities require 6 hours of an 8 hour work day, it would not be cognizant to schedule more than 2 hours of meetings in a day. Another recommendation could be to ensure an employer is providing appropriate time off. That could mean sick time is different from traditional paid time off/vacation time. Provide the opportunities for employees to take time, but also encouraging taking time off. Like we noticed in 2019, there was a lot of talk about Japan's workplace reform laws which included time off _requirements_ for employees. These could all be steps in showing that employers don't need nor expect an employee to give _all_ of their time to their place of work.


The second largest and consistent topic of concern was the financial stability an employee feels they have. This topic was talked about in some way shape or form throughout the years. The terms seen in this topic were: 
- money, 
- wage, 
- profit,
- life,
- live, 
- income, 
- wealth, 
- freedom, 
- retire, 
- buy, 
- value, 
- house
- education, and
- "capit"

These are all about money, but with a connotation of the future. Employees want to know their future in being invested in, the same way they invest their time with an employer. Recommendations for employers to give the message of being invested in their employees' futures could include doing something to ensure that your employees don't see themselves as "just a number" or "part of the system". Do things that make them feel appreciated, important, and valuable such as asking their opinions when possible, giving bonuses for the holidays or for returning next fiscal year, and regularly providing opportunities for employees to provide meaningful feedback, then acting on it. Employers could provide opportunities for professional development without having to take time off, or provide access to and encourage use of online learning places such as Coursera or Udemy. Another way an employer could show they care about the financial stability of their employess is to offer some type of student loan forgiveness, or assistance/encouragement of employees furthering their education. These are some ideas that could make employees feel as if their companies are sharing the wealth opposed to withholding the fruits of their labor.

Lastly, the third most consistent topic was centered around systemic concerns. Sometimes these concerns were political and concerning capitalism, like we saw in the year 2021 where Jeff Bezos was brought up often. Other times the concerns were centered around workplace culture like we were seeing in 2020 where union and strike were very common, and especially in 2019 where employees were talking very heavily about the new Japanese workplace reform policies. The terms that were seen in this topic were: 
- strike, 
- union,
- "societi", 
- capitalist
- american, and
- "economi"

While these terms were found consistently, the specifics of the systemic concerns changed between 2019 and 2021 depending on what was going on in the world at the time. The biggest recommendation to remedy this topic is to host surveys that are without reprimand that allow for data to be collected and changes to be made. Without reprimand also includes not requiring employee time on trainings that won't benefit the employees because taking time is a reprimand. When big events are happening, such as a pandemic, not only could employers ask employees if they feel physically and mentally safe in the workplace, and/or what could make them feel safer, they should also put actions behind those questions. Employers could make it systemic to be concerned about their employees instead of employees being concerned about the systemics of their employers.

## Next Steps
This model can be fed new documents without having to be retrained, so I would continue to monitor r/Antiwork and add documents to the corpus. This would allow me to see how the topics are shifting, or remaining the same, with time. I would also like to extract text from images as there a lot of meaningful words within the images. Additionally, I would like to retrain the model using n grams, including other stop words that coud be interfering with the model, and increasing the iterations of the model during training.

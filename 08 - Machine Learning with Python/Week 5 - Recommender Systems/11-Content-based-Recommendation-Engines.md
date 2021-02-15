# Content-based Recommendation Engines

## Intro to Recommender Systems

> Recommender systems capture the pattern of peoples' behavior and use it to **predict what else they might want or like**.

### Applications
+ what to buy?
    + e-commerce, books, movies, beer, shoes
+ where to eat?
+ Which job to apply to?
+ who you should be friends with?
+ Personalize your experience on the web

### Pros
+ Broader exposure
+ possibility of continual usage or purchase of products
+ Provides better experience

### Two Types
+ Content-based 
    ![Image](https://i.imgur.com/89NbkEb.png)
+ collaborative filtering
    ![Image](https://i.imgur.com/7DyF69K.png)
+ Hybrid 

### Implementation
+ Memory-based 
    + uses the entire user-item dataset to generate a recommendation
    + Uses statistical techniques to approximate users or items
        + e.g. Pearson Correlation, Cosine Similarity, Euclidean Distance
+ Model-based
    + Develops a model of users in an attempt to learn their preferences
    + Models can be created using Machine Learning techniques like regression, clustering, classification, etc.


## Content-based Recommender Systems

![Image](https://i.imgur.com/DfjPaL4.png)

Similarity between those items. 

Weighted Genre Matrix:
![Image](https://i.imgur.com/TDKpK3E.png)



Content-based recommendation system tries to recommend items to the users based on their profile built upon their preferences and taste. 


## Collaborative Filtering

+ User-based collaborative filtering
    + based on users' neighborhood
+ Item-based collaborative filtering
    + based on items' similarity

### User-based collaborative filtering

![Image](https://i.imgur.com/C8JBxGR.png)

User ratings matrix:

![Image](https://i.imgur.com/eTEARGL.png)

![Image](https://i.imgur.com/9lPOdtx.png)

**Item-based?**

+ Not based on content
+ If User 1 and User 2 both show positive ratings for Item 1 and Item 3 and User 3 shows great interest in Item 3, Item 1 is more likely to be recommended to User 3. 

![Image](https://i.imgur.com/K6NFCMC.png)

### Challenges
+ Data Sparsity
    + Users in general rate only a limited number of items
+ Cold Start 
    + Difficulty in recommendation to new users or new items
+ Scalability
    + increase in number of users or items
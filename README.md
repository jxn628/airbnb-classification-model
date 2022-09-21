# Using Predictive Modeling to Get More 5-Star AirBnb Reviews

Airbnb has revolutionized the hotel and vacation industries by allowing people to easily rent their own houses out to other travelers. However, it can sometimes be hard for Airbnb Hosts to be as successful as they would like to be. The most common question from AirBnb Hosts is "What can I do to get more 5-star reviews and a 5.0 Overall Rating?" This project uses data for the city of San Diego from [InsideAirbnb.com](https://insideairbnb.com) to create a model which can predict whether a Rental Unit will get a 4.9-5.0 Overall Rating with 83% Precision.

![Solutions to Problem](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/Solutions%20to%20Negative%20Trend.png)

Oceanside Property Management is a property management company located in San Diego California. Their main business is managing rental properties. However, they have recently noticed that a lot of Airbnb hosts have been reaching out to them for guidance. These hosts are mostly uninterested in having OPM manage their rentals, however they want some help in increasing their success as Airbnb hosts.

There have been so many Airbnb hosts reaching out that OPM has decided that AirBnb host consulting could be a good side-business for them. They plan to officially add Airbnb consulting as a service that they provide. In their initial research they found that the top questions that potential clients who wish to utlize this service are:
- <b>1) "What can I do to get more 5 star ratings?"</b>
- <b>2) "Can you help me reach Superhost status? (or maintain Superhost status)</b>

These questions are understandable because Airbnb puts a huge focus on getting 5 star overall ratings. They also highly publicize the benefits of getting (and maintaining) Superhost status.

Oceanside Property Management has decided that the main focus of their service will be helping clients get more 5 star reviews. Therefore they have tasked me with providing the following: 
- <b>1)A model</b> that will predict whether a specific rental unit will get a 5 Star Overall score based on other available information.
- <b>2)An industry analysis of AirBnb in San Diego.</b> Specifically looking for any insight that they can give to their clients that will give them a leg up on people who don't use their consulting service.

They also want me to answer the following questions:
- 1)Is there a significant advantage to being a Superhost? (is it worth all the effort to get this status and maintain it?)
- 2)How do we determine whether a Host "should" be getting 5 Star reviews?
- 3)What factors are most important in determining a 5 Star Overall Rating? (what aspects should they most focus on)

And finally, they want to know where their consulting service can make the most impact, so they know which features to market and/or which hosts to market to.

## About AirBnb
Information from: https://listwithclever.com/research/airbnb-vs-hotels-study/ accessed 7/7/22

- Airbnb is becoming the preferred choice of vacationers — <b>60% of travelers who use both Airbnb and hotels prefer Airbnb over comparable hotels when going on vacation.</b>
- 68% of business travelers prefer staying in hotels when traveling for work, and they're more likely to have a negative experience at an Airbnb

### Importance of 5 Star Reviews
AirBnb focuses on exceeding customer expectations, which is why they strictly <b>require that hosts maintain a near perfect rating in order to remain on the service.</b>

### Importance of Superhost
- information from https://www.airbnb.com/d/superhost. Accessed 6/16/22

<b>Advantages: </b>
- Superhost badge to stand out among other hosts.
- Customers can filter search results to show only superhosts.

<b>Requirements:</b>
- Minimum 4.8 overall rating.
- 10 stays over the last year.
- < 1% Cancellation Rate.
- At least 90% Response Rate.
- Reassessed every 3 months.

### Problems with the AirBnb Review Scale
The review data is incredibly skewed because Airbnb requires such a high rating. <b>Even though there is a 5 point scale, Anything lower than a 4.8 is seen as "bad".</b>
- So while this is technically a 5 point scale (as a reviewer can give 1 - 5 stars, with no partial stars allowed), getting a 4.0 average could result in being de-listed from the service!

The major problem with this review system is that <b>airbnb guests often assume that airbnb's review scale functions similarly to a hotel review scale, which also uses 5 stars</b>, with 3 considered average, 4 above average, and 5 star being the best possible experience.

from https://medium.com/@campbellandia/how-to-avoid-the-dreaded-4-star-review-a-guide-for-airbnb-hosts-cdf482d083fe
- <i>The problem stems from the fundamental difference in what most people think a 5-star rating system is, and what AirBnB’s system actually is. The vast majority of people think that a 4-star review is perfectly appropriate; Their stay was good, they enjoyed themselves, but your place wasn’t the Vanderbilt Suite at the Plaza. What they don’t understand is that if a listing gets too many 4-star reviews the AirBnB platform begins to send warnings to hosts that their listing will be removed.</i>


## The Problem
![The Problem: Relationship between Overall Rating and Number of Listings](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/Trend%20with%20Units%20Listed%20Annotated.png)


## Target: Elite Units
- <u>Elite Units</u>: Any Unit with a 4.9-5.0 Overall Rating.
- - 4.9 is still an incredibly high score, and is above thresholds for success (4.8 rating, etc), so it is worth capturing units with a 4.9 Rating as high performers as well.


## Choosing Model Evaluation Metrics
- My goal is to predict whether a person will get a 4.9-5.0 Airbnb Overall rating.
- Which is worse?
    - Model predicts that a unit is an Elite Unit, but they actually aren't? (more false Positives)
    - Model predicts that someone is NOT an Elite Unit but they actually are? (more false negatives)
    
<b> Decision </b>
- I want false Positives to be as low as possible.
- If my model says that a property is an Elite Unit, I want it to be true.
- If it misses some of the Elite units in the process, that is fine.
- <b>Therefore, I am most concerned with Precision, balanced out by F1 score.</b>

## Final Model Evaluation: Decision Tree 2
- <b> Precision: </b> This Model correctly picks whether a rental will have an overall AirBnb rating between 4.9-5.0, 83% of the time.
    - This is 33% better than random guessing.
    - The Final Model is also a improvement over the baseline model. (about 7% better)
- <b>F1 Score: </b> While other models had slightly better F1 Scores, Decision Tree 2's F1 Score is only slightly worse. The F1 Score indicates that Precision is reasonably balanced with Recall, so I don't need to worry about this being an unbalanced and un-usable model. Therefore I'm fine choosing a model with a lower F1 in order to get more precsision.
- <b> ROC AUC Score: </b> Shows the True Positive Rate vs. the False Postive Rate. Some models had slightly higher scores than my Final Model, but again, it was very slight.
- <b> Cross Validation Score: </b> This model performs fairly well on data that it was not trained on and is comporable to the Cross Validation Scores of the other models. 

![Final Model Confusion Matrix](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/Final%20Model%20Confusion%20Matrix.png)

## How to use This Model going forward:
- OPM can take the data from new clients and run this model to determine whether they are performing at 5-Star level or not.
- If they are, they should be able to obtain Superhost status and OPM can focus on helping them <b> maintain </b> everything that they are doing right.
- If they are not an Elite Unit, OPM can give them advice and help get them closer to a 5.0 Overall Rating.

<b>Caveats: </b>
- No model is perfect, and this one certainly isn't.
- This model relies on review scores from the 6 review categories. <b>If you don't have that data, the model does not perform reliably enough to be used.</b>
- That said, it can be reliably trusted as only 133 records from the test set of 1,953 were incorrectly labeled as being Elite Units when they were, in fact, not. (We aren't worried about the ones that were predicted to be not Elite incorrectly)


## Top Features
![Top Features](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/Top%20Features%20Annotated.png)

#### Analysis: 
- <b>Accuracy is by far the most important feature</b>
- It is <b>5.5 Times more important</b> than the next features.
- <b> Value and Cleanliness are also important, but not nearly as much as Accuracy</b>
- <b>Communication</b> also has importance, but not nearly as much as the others.

## Top Feature Accuracy Score

Accuracy is by far the most important feature in my model. Let's look at the relationship between Accuracy Score and Overall Rating.

![Accuracy Score vs. Overall Rating](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/Accuracy%20v%20%20Overall%20Rating.png)

### Analysis:
-  There is a linear relationship between the two. Whatever the Accuracy Score is, the Overall Rating will likely be very similar as there is a nearly direct linear relationship.
- <b>Therefore, focusing on Accuracy is the best way to get 5 Star Reviews.</b>
- This matches what I found in my research. <b>The most important aspect of renting an AirBnb unit is that the listing is accurate, to ensure that Guest expectations are met.</b>
- Nearly all units that have an accuracy score of 4.9-5.0 also scored high in the other 5 review metrics.
- Nearly all units that did not have an accuracy score of 5 did not score highly on others as well.
- <b>Significantly more likely to be Elite Units and/or SuperHosts</b>
- More likely to have a 100% Response Rate
- <b>73% of units that scored 4.9-5.0 on accuracy were in our target 5-star range.</b>
- They are less likely to use the instant book feature, although 41% of units with 5.0 accuracy do each.


## Questions Answered

### Is there a significant advantage to being a Superhost? (is it worth all the effort to get this status and maintain it?)

![SuperHosts v. Non-SuperHosts](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/SuperHostsvNotSuperhosts.png)

- <b>YES!</b>
- <b>Superhosts are 21% more likely to be Elite Units than non-superhosts.</b>
- <u>Superhosts and the 4 Most Important Features:</u>
- 81% of Superhosts have at least 4.9 Communication Score. (30% better than non-superhosts)
- 64% of Superhosts have at least 4.9 Accuracy Score. (26% better than non-superhosts)
- Superhosts have similar Value Scores to Non-Superhosts.
- Superhosts are better able to to handle higher numbers of listings.
- Most Superhosts can have 10 listings before it affects their 3 Month Booking Rate.
- Most Superhosts are also able to have 10 listings before their Overall Rating Drops below 4.8.

### Is there a significant advantage to having Elite Units?

![Elite Units v. Non-Elite Units](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/Elite%20Units%20vs.%20Units%20Listed.png)

#### Analysis: 
- While Elite Units perform slightly better in booking rate, <b>being an Elite unit is the best solution to the negative trend between Overall Rating and Number of Units.</b>
- <b> As long as you can keep your units performing at the highest levels, there is no limit on how many units you list.</b>
- The catch is of course, learning how many that you can manage and keep at that level. <b>This is an area where OPMs service will be invaluable!</b>
- Offer resources to help Hosts. (Preferrred cleaners, stagers, contractors for emergencies. Maybe even a dedicated customer service phone number)
- Most Notably, <b>Elite Units have the biggest increase in the Top Features: accuracy, cleanliness, value, and communication.</b>
- <b>This shows that the Target Feature does a good job of capturing the features that lead to more 5 Star Overall Reviews!</b>
- Elite Overall units score much higher in review metrics. This makes sense because they should have to score high in all of them to get a high overall score (even though it is a seperate metric in terms of AirBnb).
- They are also more likely to be a superhost, and more likely to have less than 5 listings.
- They are less likely to have high Capacity, or use Instant Book feature, but the differences aren't major.

![Analysis of Elite Units](https://github.com/jxn628/dsc-phase-5-project/blob/main/Images/AirBnb_Project_Images/Annotated_Features.png)

## Conclusion

In my analysis of Airbnb rentals in San Diego California, I found that having a high overall rating (4.9-5.0), as well as having SuperHost status, were both beneficial to success on the platform.
- I also found that Accuracy was the biggest factor in getting a high overall rating, with a nearly 1 to 1 linear relationship.
- Other important features were Value, Cleanliness, & Communication.

<b> Key Areas for OPM's AirBnb Host Consulting Service :</b>
- <b>Accuracy:</b> By providing a listing service which assesses client's rental units and lists their units in such a way as to maximize the accuracy. 
- <b>Bridging the Gap between Owner-Managed and OPM Managed:</b> OPM can provide a la carte services which help owners who wish to keep managing their own properties, but can't handle doing so at the highest quality levels. <b> This is also beneficial to OPM in creating a pipeline of potential fully managed units as hosts take on more properties that they can manage. </b>
-- This can be structured in such a way to incentivize clients transitioning to OPMs full management service at certain thresholds (ie, 10 properties, etc).
- <b>Communication: </b>OPM can train hosts on what they can do to set expectations properly, and then exceed them with service (AirBnb's goal). This is done through how they communicate and how often they do it.
- <b> Provide Resources to Help Hosts Set Guest Expectations, and Then Exceed Them!</b>
- accurate listing
- explanation of airbnb's skewed review system.
- do this without being deceptive or cooercive.
- It doesn't matter if Hosts have all the metrics and analysis to <b>know</b> that their unit deserves 5-star reviews. Their fate is in the hands of the reviewers. If they really care about getting 5 star reviews (and they should since they are critical to success on AirBnb), they need to explain this to their guests. 

## Further Work

### Use Natural Language Processing to analyze amenities.
- This DataSet includes <b>amenities, which would be very benefical to both the model and industry analysis.</b> 
- However, they are all in string format and getting them into a useful format will be time intensive. 
- Get them into a format where they can be one-hot encoded and fed into the model.

### Increase the scope of this model.
- Incorporate data from the rest of California, and then the rest of the US.

## Links

[Video Presentation of this Project with Q&A](https://youtu.be/1LiVc96g69g?t=880)

[Final Jupyter Notebook](https://github.com/jxn628/dsc-phase-5-project/blob/main/EDA-Modeling-Evaluation.ipynb)

[Presentation Slides](https://github.com/jxn628/dsc-phase-5-project/blob/main/Airbnb_Classification_Model_Presentation.pdf)







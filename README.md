![](images/pets.jpg)
# Petfinder: Adoption Speed Prediction

### Background and Problem Statement

Shelters in California are statistically underfunded and overcrowded. Many are staffed predominantly by volunteers and due to understaffing and protocols, shelter dogs spend much of their time alone. Over 100,000 dogs are euthanized per year in California alone for reasons like shelter overcrowding and extended stays. Shelters are doing their best, but studies show that after a month in a shelter most dogs experience long term or permanent behavioral effects from their time in rescue conditions which can make it harder to find them a forever home..

To tackle this problem I used the Petfinder API and petpy wrapper to collect Bay Area dog adoption data for dogs adopted 2019 through 2020.  I endeavor to discover the most influential features that contribute to a speedy dog adoption as well as what features tend to lead to a dog spending more time in rescue before finding their forever homes. I will accurately predict which dogs will be adopted in less than 2 weeks, and which will not.\
\
If we can better understand the features with the potential to reduce the amount of time a dog spends in rescue, we can reduce the strain on shelters, provide better services to dogs and humans alike and minimize the sad practice of euthanizing shelter dogs due to lack of space.
---

### Contents
| Notebook | File Name | Description |
|----|----|----|
|**1**|[1-PetfinderClean.ipynb](https://github.com/jessicabow/Capstone/blob/main/1-PetfinderClean.ipynb)|Data collection using Petfinder API and Petpy wrapper. Data cleaning and feature engineering. EDA, exploratory LogReg and TFIDF model|
|**2**|[2-Models.ipynb](https://github.com/jessicabow/Capstone/blob/main/2-Models.ipynb)|Exploratory data analysis of clean Petfinder data for Northern California 2019-2020.|
|**3**|[3-FeatureUnion.ipynb](https://github.com/jessicabow/Capstone/blob/main/3-FeatureUnion.ipynb) Regression(numerical) and TFIDF + Naive Bayes(ordinal) binary classification prediction models.|
|**4**|[4-Inference.ipynb](https://github.com/jessicabow/Capstone/blob/main/4-Inference.ipynb)|TBD|
---

### Analysis Summary

![Age](https://github.com/jessicabow/Capstone/blob/main/images/Age.png)

![Size](https://github.com/jessicabow/Capstone/blob/main/images/Size.png)
\
These plots show the distribution of age, size and coat type in adopted dogs adopted off Petfinder from 2019 through 2020. The most highly coveted and populous age is a puppy (0-4 months), while small dogs are the most prevalent, as is a short coat.\
![Breed](https://github.com/jessicabow/Capstone/blob/main/images/Breed.png)\
Chihuahuas and Terriers lead the primary breed population of adopted dogs throughout the bay area. These are very common breeds in general and two of the most common particularly when mixed with another breed (ie. Chieweenie, Chug)\
![Month](https://github.com/jessicabow/Capstone/blob/main/images/AdoptMonth%20(1).png)\
No surprise the most dogs are adopted around the holidays in December, followed by April. A big dip in both population and adoption speed in the summer highlights possible area for improvement.\
![AvgDays](https://github.com/jessicabow/Capstone/blob/main/images/map_daysonpetfinder.png)\
Amador County (darkest color), has by and far the slowest adoption speed with the average dog waiting almost 5 months for adoption. In contrast, Merced County has the fastest adoptions with each dog spending on average of 14.3 days in rescue. This merits a deeper look as of course local population and demographics in addition to overall county dog population play a role. Higher concentrations of dogs with features seen here to bring down adoption speed could be a factor as well as how local shelters in these counties are run and what population of dogs they shelter.

I ran many models including, Logistic Regression, Bagging Classifier, Random Forest, AdaBoost and XGBoost. My best accuracy score was acheived when I ran my listing description column through TFIDF and my numerical data using Logistic Regression and then performed a Feature Union. While other models scored higher, they were far more overfit. I plan to revisit and tweak hyperparameters as well as run more models to try and increase my accuracy, but in the meantime my TFIDF + Logreg model resulted in 0.76 and 0.73 Training and Testing score, respectively. This is 21% over the baseline of 0.52.\
![Coef](https://github.com/jessicabow/Capstone/blob/main/images/Screen%20Shot%202021-01-27%20at%2010.32.12%20AM.png)\
While predictive ability and a high accuracy are important, more important in this case is the feature importance. While breed and location by zipcode  were found to be the features that gave the strongest odds of a speedy or slow adoption, we are here to look at actionable steps shelters and communities can take to minimize time from rescue to adoption. This table represents some of the standout features that highlight areas of possible growth or reform. For context, we can see that a dog being a puppy makes the odds of a speedy adoption 1.92. While a dog being verified as good with kids and/or cats increases the likelihood of a speedy adoption by 1.32 and 1.40, respectively, it turns out just having this information is enough to increase the odds of being adopted slightly. Shelters who do not test and/or report a dog's interaction success with other vulnerable demographics tend to be adopted slower. While size, age, disability and breed are features we can't expect to shift in our shelter dog population, we can make some informed decisions by looking closer at misclassified listings.\
![Confusion](https://github.com/jessicabow/Capstone/blob/main/images/download.png)\
73% prediction accuracy is a good start in this particular situation, particularly considering that the listings that were misclassified as being slow adoptions that were actually speedy adoptions can be used to explore what features are contributing and what it is we can learn from these shelters. The shelters that were positively misclassified tend to focus on public and volunteer education, they test their dogs for compatibility with children, cats and other dogs and they have more stringent application processes to find potential adopters the perfect match and weed out noncommittal applicants. Another positive attribute is the smaller shelters who specified- for example one of the most positively misclassified shelters prioritizes adopting and rehabilitating senior and disabled dogs. Many of these are in a more metropolitan area, which highlights the possibility for struggling rural shelters to team up with shelters in more populated locations. And the largest takeaway is that the bulk tended to have lower quantity of dogs, meaning staff and volunteers are not spread so thin - another standout suggesting shelters should work with one another to evenly distribute and support the shelter dog population.

Alternatively, negative misclassified listings appeared to come from shelters that didn't provide much in the way of information or details on their Petfinder specific rescue page. As we saw with positive misclass shelters, more robust dog adoption applications are potentially correlated to quicker adoption as it may isolate more motivated adopters. One of the worst performing shelters was also a shelter with one of the highest dog populations, this was common with the shelters for which dogs were predicted, but failed to have speedy adoptions. The shelter that seems to highlight this point the most is also self touted as very grassroots, volunteer led and even includes a warning on response time, indicating they are understaffed. These poor performing shelters also seemed to have less information overall, the information they did provide about the shelter was more generic, less specialized, and many of these did not test or report compatibility of their shelter dogs with children or cats.

After performing sentiment analysis on the description column it seems while there is not a strong correlation with description length (to a point, no description hurts adoption speed), the positively misclassified shelters had descriptions more than 2x as positive as the compound polarity score for the negative misclass.

---

### Conclusions + Recommendations

-Specify and spread out. By targeting a specific demographic of shelter dog in your area shelters can better support their dogs and make quicker matches with potential adopters. \
-Transfer pets based on local demand. Better supply and demand model by working with shelters in neighboring counties. \
-Volunteer outreach and training. Dogs with some level of training are adopted much quicker! Recruit and train more volunteers for more support and so that every dog gets some level of training reinforcement on their daily walks. \
-Work with and eventually test dogs for interaction with vulnerable populations like kids and cats. \
-More in depth application process. Weed out all but serious adopters to reduce strain on limited staff. \
-Include details and unique mission statement on your Petfinder shelter page. \
-Seek sponsorship with local business/corporation to incorporate more enrichment, better outreach and more funding (tax deductible for them!) \
-See the bright side - end descriptions on a positive note! \

---

### Sources:
* [Petfinder](https://www.petfinder.com/)
* [Maddie's Fund](https://www.maddiesfund.org/behavior-problems-and-long-term-housing.htm)

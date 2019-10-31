# Natural-Language-Process
### Goal

To provide suggestions for NYT where to put advertisement to maximize profit, predicted popularity of news in NYT by constructing machine learning predictive models, get F1 score of 0.75, Precision-Recall Curve area of 0.8
### Data Preparation

Using NYT archives API and community API, we have extracted articles of 2015 and have extracted comments made on each article as an indication of popularity. Among the many features we generated, we calculated the positive and negative polarity for the headline, abstract and leading paragraph of each article and also generated dummy variables for sections, day of week, etc. We also scraped 2013 - 2014 archives to extract the number of articles published in 2013-14 by each author to generate a new feature “auth_c”. Though this feature only boosted validation F1 score by 1%, it appears to be quite important.(See feature importance).
We categorize the number of comments into 3 classes: 0, 1 and 2. And find it is highly unbalanced with 72%, 14%, 14% of class 0, 1 and 2.

### Built model and do selection

Given our classes are ordinal, the penalty for misclassification is not constant, and we can only maximize our gain by predicting every class correctly. Hence we chose macro F1 score as our evaluation standard which approaches 1.0 only when both precision and recall are high. 
Since our feature space contains both numeric and categorical variables, we believe decision tree and random forest perform better than multiclass SVM. When we build trees and random forests, we set the class weight according to our gain metric so that class 2 accounts for more impurity in comparison to other classes at each split.   

### Result Analysis
We select an optimal Random Forest Model as our final prediction model. It achieves an f1 score of 0.731 and we note an increase in gain in accordance with our evaluation metric from the baseline 67%(27249) to 86%(34842) with the optimal being 40481.
By drawing Precision-Recall curves for each class, the areas under the curves are 0.97, 0.70, 0.72. They indicate our model has better prediction power for class 0, and moderate prediction power for class 1 and 2. This is reasonable because the class 0 accounts for the majority of the population and so it is hard to distinguish 1 and 2 from them.
Although amongst the top 20 important features, 15 are numeric, we notice that the binary features are quite important. Especially the indicator for the opinion section which resonates the fact that people are instigated to comment on that section type. It is also worthwhile to notice that polarity is very important.



![image](https://user-images.githubusercontent.com/46982385/67976143-eb97ef00-fbeb-11e9-9990-f844230df4cd.png)

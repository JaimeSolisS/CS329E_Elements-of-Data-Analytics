# Bookings cancellation prediction

Tourism and travel related industries, like Hotels, aim to optimize their room bookings and revenue. Hoteliers understand, however, that alongside these bookings is an uncertainty in regards to guest cancellations and no-shows. Regardless of the reason behind guest no-shows and cancellations, these occurences largely impact revenue in a number of ways.

As such, our work seeks to employ various classification algorithms to develop predictive models which classify hotel bookings to determine whether or not they will cancel or no-show. These models could help hoteliers keep their businesses optimally booked, avert financial risk, and promote increased revenues.

## Data

The data used in this notebook comes from an open hotel booking demand dataset collected by [Antonio, Almeida and Nunes, 2018](https://www.sciencedirect.com/science/article/pii/S2352340918315191) and downloaded from [R for Data Science online learning community](https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-02-11/hotels.csv).

The dataset is a combination of two datasets with hotel demand data. One of the hotels is a resort hotel and the other is a city hotel. Its structure is formed with 32 variables describing the 40,060 observations of resort hotel and 79,330 observations of city hotel. Each observation represents a hotel booking.

The dataset stores bookings due to arrive between the 1st of July of 2015 and the 31st of August 2017, including bookings that effectively arrived and bookings that were canceled. Since this is real hotel data, the authors deleted all data elements pertaining hotel or costumer identification.

## Result and conclusion

| Model                   | Accuracy Scores |
| ----------------------- | --------------- |
| Neural Network          | 79.629997       |
| SVM                     | 79.150002       |
| Random Forests Ensemble | 79.120003       |
| Boosting ensemble       | 78.449997       |
| Decision Tree           | 78.400002       |
| KNN                     | 78.091003       |
| Naive Bayes             | 52.900002       |

In conclusion, we chose Neural Network as the best model with which to evaluate our dataset. We made this decision because this model had the highest accuracy when evaluated with a cross validation.

A few other models came quite close, but we decided not to proceed with them for the reasons listed below:

a) Decision Trees provided a lower accuracy compared to the other models due to their simplicity and the variance in the data

b) KNN was less accurate that the other models due to the curse of dimensionality drastically affecting the algorithm

c) Naive Bayes fails to work on datasets with as high dimensionality as ours

d) SVM and Ensemble methods' accuracies depend largely on setting the parameters correctly. If the parameters are not optimal, there is a risk of overfitting or having a biased model with ensembles or having varying
accuracies with SVM.

With accuracies above 79%, SVM and ensemble method models could also be relatively strong models for our dataset as both classifiers scale well to data with high dimensionality. NN, however, provided higher accuracies than both SVM and Ensemble Methods. Neural Nets are susceptible to overfitting and extremely time consuming, but they thrive with large datasets and numbers of features. Once trained, a NN model makes accurate predictions (assuming a quality dataset) with extreme speed relative to the other algorithms. As such, we decided that Neural Networks would be an ideal model to facilitate predictictions on future booking data.

To further evaluate the accuracy of this model, we tested it with our test dataset produced through Principal Component Analysis, and display a confusion matrix for further analysis.

Note: Accuracy scores reported is for the test set, not entire dataset.

Looking at the confusion Matrix we predicted

**True positive: 11597**
**True negative: 2350**
**False positive: 2467**
**False negative: 1020**

**Accuracy = (TP+TN)/total**
**Accuracy = (11597+2350)/17434 ~ 80%**

**Error Rate = (FP+FN)/total**
**Error rate = (1020+2467)/17434 ~20%**

_Given a canceled booking prediction, how likely is it to be correct?_
**Precision(-) = TN/(TN + FN) = ~70% of times**
_Given a canceled booking example, will the classifier detect it?_
**Recall(-) = TN/(TN + FP) = ~49% of times**

Examining the results above, we can see that our Neural Net model performs poorly when predicting on our test data.

A ~70% precision could have some value to a hotel business by encouraging preventative and risk mitigation measures in the event the model predicts a cancelation. But a recall of approx. 49% indicates that we failed to detect half of our canceled bookings. This recall calls into question the magnitude of our model's worth.

We could attempt, however, to better our model by training it with the entire dataset or using more neurons in the hidden layers. Hopefully, these changes would serve to improve our predictive accuracy and add greater value to hotel and resort owners.

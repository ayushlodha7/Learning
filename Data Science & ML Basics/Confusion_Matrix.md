# Confusion Matrix and Related Metrics

# Confusion Matrix Using Example of Cardiac Arrhythmia

---

**Actual: It is what is known as labeled data**

**Predicted: It is what is expected using the Algorithm.** 

|  | Actual | Actual |
| --- | --- | --- |
| Predicted | Have Cardiac Arrhythymia | Does not have Cardiac Arrhythymia |
| Have Cardiac Arrhythymia | True Positive | False Positive |
| Does not have Cardiac Arrhythymia | False Negative | True Negative |
- **True Positive (TP):  Predicted that the patient would have “Cardiac Arrhythmia”; it has one.**
- **True Negative (TN): Predicted that the patient won’t have “Cardiac Arrhythmia”; it does not have one.**
- **False Positive (FP): Predicted that the patient would have “Cardiac Arrhythmia”; but it does not have one.**
- **False Negative (FN): Predicted that the patient won’t have “Cardiac Arrhythmia”; but it does have one.**

# Metrics Derived from the Confusion Matrix.

---

## Sensitivity (True Positive Rate or Recall)

$$
\text{Sensitivity} = \frac{\text{True Positive}}{\text{True Positive} + \text{False Negative}}
$$

|  | Actual |
| --- | --- |
| Predicted | Has Cardiac Arrhythymia |
| Have Cardiac Arrhythymia | True Positive |
| Does not have Cardiac Arrhythymia | False Negative |

*In this case, Sensitivity tells us what percentage of patients having “Cardiac arrhythmia” are correctly predicted by the algo.* 

---

## Specificity (True Negative Rate)

$$
\text{Specificity} = \frac{\text{True Negative}}{\text{True Negative} + \text{False Positive}}
$$

|  | Actual |
| --- | --- |
| Predicted | Does not have Cardiac Arrhythymia |
| Have Cardiac Arrhythymia | False Positive |
| Does not have Cardiac Arrhythymia | True Negative |

*In this case, Specificity tells us what percentage of patients not having “Cardiac arrhythmia” are correctly predicted by the algo.* 

---

## Accuracy

|  | Actual | Actual |
| --- | --- | --- |
| Predicted | Have Cardiac Arrhythymia | Does not have Cardiac Arrhythymia |
| Have Cardiac Arrhythymia | True Positive | False Positive |
| Does not have Cardiac Arrhythymia | False Negative | True Negative |

$$
\text{Accuracy} = \frac{\text{True Positive}+\text{True Negative}}{\text{True Positive} + \text{True Negative}+\text{False Positive}+\text{False Negative}}
$$

- The metric's name shows us the accuracy used to judge model performance.
- However, it won’t be an ideal metric if the dataset is unbalanced,
    - For Example, Since the ECG signals show that it is of the cardiac arrhythmia patient, there are 90% of cases in which signals are false, which don’t have cardiac arrhythmia, and 10% of cases in which signs are true, which do have cardiac arrhythmia. Hence, the accuracy would be 90%. However, it won’t be a good performance metric.

---

## Precision

|  | Actual | Actual |
| --- | --- | --- |
| Predicted | Have Cardiac Arrhythymia | Does not have Cardiac Arrhythymia |
| Have Cardiac Arrhythymia | True Positive | False Positive |

$$
\text{Precision} = \frac{\text{True Positive}}{\text{True Positive}+\text{False Positive}}
$$

Rate of which your positive predictions are actually positive.

---

## F1 Score

**Precision: (TP/TP+FP) The proportion of predicted arrhythmia cases that were actual arrhythmias.**

**Recall/ Sensitivity: (TP/(TP+FN)) The proportion of actual arrhythmia cases correctly identified by the model.**

- For our case, we would require a model with high sensitivity because we don’t want our model to say that it missed cardiac arrhythmia, which may cause the patient's life.
- However, false alarms may be said, “Sorry for the inconvenience.” You might not face a heart attack. It was our mistake.
- **The F1 score is the harmonic mean between precision and recall.**
- **It is a single metric that considers both false positives and false negatives.**

$$
\text{F1 Score} = 2*\frac{Precision*Sensitivity}{Precision+Sensitivity}
$$

---

## ROC

### **Why do we need it?**

To Explain this, let me give you an example: Suppose I use logistic regression for the above classification (0 and 1); not having cardiac arrhythmia or having cardiac arrhythmia. What are the implications of the threshold?

|  | Actual | Actual |
| --- | --- | --- |
| Predicted | Have Cardiac Arrhythymia | Does not have Cardiac Arrhythymia |
| Have Cardiac Arrhythymia | True Positive | False Positive |
| Does not have Cardiac Arrhythymia | False Negative | True Negative |

### There are low and high threshold scenarios, which we should discuss before moving further.

### Low Threshold (e.g., 0.1 or 0.2)

- The Number of patients correctly predicted having cardiac arrhythmia (and they also have one) increases. (Hence Higher True Positive and Lower False Negative)
    - But those who don’t have cardiac arrhythmia are also wrongly predicted to have one. (Higher False Positive and Lower True Negative)
- ***Higher Sensitivity since True Positives increase and False Negatives decrease.***
- ***Lower Specificity since False Positive increases and True Negative decreases.***
- ***More cases of actual ones are detected, but false ones are also seen, which may lead to more unnecessary medical interventions or additional tests.***

### High Threshold (e.g., 0.8 or 0.9)

- The number of patients correctly predicted not having cardiac arrhythmia (and they also don’t have one) increases. (Hence Higher True Negative and Lower False Positive).
    - But those with cardiac arrhythmia are also wrongly predicted as not having one. (Hence, Lower True Positives and Higher False Negatives)
- ***Lower Sensitivity since True Positives decreases and False Negatives increase. (which shows it might miss several actual cases of arrhythmias)***
- ***Higher Specificity since False Positive decreases and True Negative increases. (Higher precision, most of the positive predictions are actual arrhythmias)***
- ***It could be dangerous if undetected arrhythmias have several implications.***

**So, we must create a confusion matrix for each threshold and calculate the True Positive Rate and False Positive Rate for each scenario.

For each threshold, we plot the x-axis as the False Positive Rate and y-axis as the True Positive Rate.** 

![Untitled](Confusion%20Matrix%20and%20Related%20Metrics%20575067b2b65049cb9f85450aee6d303d/Untitled.png)

---

## AUC: Area under Curve

- It is simply the area under the curve of the ROC graph.
- It helps us compare two roc curves (maybe they both are from two different algorithms, hence helping us know which classification algorithm is better)

---

## 📈 Example of the above-understood Metrics:

You can see the notebook for the implementation [here:](https://www.kaggle.com/code/ayushlodha18110031/cardiac-arrhythmia-classification) 

### Data

- Cardiac Arrhythmia Dataset, reduced columns, for example case:
- Screenshot of the dataset overview, X_columns = [age,sex, height, weight] and Y_columns = [diagnosis]

![Untitled](Confusion%20Matrix%20and%20Related%20Metrics%20575067b2b65049cb9f85450aee6d303d/Untitled%201.png)

### Confusion Matrix of the Model: Logistic Regression

![Untitled](Confusion%20Matrix%20and%20Related%20Metrics%20575067b2b65049cb9f85450aee6d303d/Untitled%202.png)

### Classification Report of the Model: Logistic Regression

![Untitled](Confusion%20Matrix%20and%20Related%20Metrics%20575067b2b65049cb9f85450aee6d303d/Untitled%203.png)

### ROC Curve of the Model: Logistic Regression

![Untitled](Confusion%20Matrix%20and%20Related%20Metrics%20575067b2b65049cb9f85450aee6d303d/Untitled%204.png)

### Comparison of the two ROC Curves of the Models (Logistic Regression and Random Forest Classifier)

![Untitled](Confusion%20Matrix%20and%20Related%20Metrics%20575067b2b65049cb9f85450aee6d303d/Untitled%205.png)

- For this case, we can see that the Random Forest Area under the curve is greater than the Logistic Regression one.
- Hence, Random Forest is performing better in this case.
- That’s how we use AUC.😉

# References:

- [https://towardsdatascience.com/guide-to-confusion-matrices-classification-performance-metrics-a0ebfc08408e](https://towardsdatascience.com/guide-to-confusion-matrices-classification-performance-metrics-a0ebfc08408e)
- [https://www.youtube.com/watch?v=jJ7ff7Gcq34&ab_channel=DataScienceDojo](https://www.youtube.com/watch?v=jJ7ff7Gcq34&ab_channel=DataScienceDojo)
- [https://www.youtube.com/watch?v=Kdsp6soqA7o&ab_channel=StatQuestwithJoshStarmer](https://www.youtube.com/watch?v=Kdsp6soqA7o&ab_channel=StatQuestwithJoshStarmer)
- [https://www.youtube.com/watch?v=vP06aMoz4v8&ab_channel=StatQuestwithJoshStarmer](https://www.youtube.com/watch?v=vP06aMoz4v8&ab_channel=StatQuestwithJoshStarmer)

![](https://komarev.com/ghpvc/?username=ayushlodha7&color=yellow)


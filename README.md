# Machine-Learning-Project
In this project, I analyze a dataset containing information about short textual entries submitted to an online discussion system. The dataset includes the content of each entry, engagement signals from other users, and outputs from automated analysis components.

The goal: to use this information to predict how each entry was ultimately categorized by the system.

### Data Files

The dataset consists of the following files:
https://drive.google.com/drive/folders/1kq06XTUOoB58-sVOoDW_SpCnwZpyEYJ4

train.csv: The training set, including the target variable label along with all feature columns.

test.csv: The test set, containing the same feature columns but excluding the target variable label.

### Columns Description

comment : The raw text content of the comment.

created_date : The date and time when the comment was posted.

post_id : A unique identifier linking the comment to a discussion thread or parent post.

emoticon_1 : Indicator for the presence of symbols from the first internal emoticon group.

emoticon_2 : Indicator for the presence of symbols from the second internal emoticon group.

emoticon_3 : Indicator for the presence of symbols from the third internal emoticon group.

upvote : Number of positive reactions received by the comment.

downvote : Number of negative reactions received by the comment.

if_1 : Internal feature one that is hidden by the platform.

if_2 : Internal feature two that is hidden by the platform.

race : Indicator showing whether the system detected references to a specific group identity.

religion : Indicator showing whether the system detected references to a belief-related topic.

gender : Indicator showing whether the system detected references to a gender-related topic.

disability : Indicator showing whether the system detected references to an ability-related topic.

label : The final category assigned to the comment by the platform (Target Variable). This variable can take four distinct values, each corresponding to a different internal handling category.

Missing text was replaced with empty strings because TF-IDF requires string input. An empty string contributes no features and avoids introducing artificial signal.

### Findings

- The comment length distribution is right-skewed with high variability. Median is significantly lower than mean, indicating presence of long comments. Length-based features were therefore engineered as they may carry predictive signal.

- Frequency analysis revealed that the most common tokens were stopwords such as "the", "to", and "and", which is expected in natural language corpora. This justified the use of stopword removal during TF-IDF vectorization to reduce noise and dimensionality.

- The dataset is highly imbalanced, with class 0 comprising 57% and class 3 only 2.7%. Accuracy would be misleading, as a model could achieve high accuracy by predicting the majority class. Therefore, Macro F1 was used because it gives equal importance to each class and better reflects balanced performance across categories.

- Logistic regression performed best due to linear separability of TF-IDF features and effective regularization tuning. Cross-validation ensured generalization, and feature engineering improved minority class detection.

TF-IDF was used to convert raw text into numerical features. Logistic Regression was selected after comparative evaluation against LinearSVC and LightGBM due to superior macro F1 performance. Hyperparameters were tuned using cross-validation to improve generalization. Feature engineering included vote-based and text-length features to enhance predictive performance. The final model achieved macro F1 greater than 0.79.

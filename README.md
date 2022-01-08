# DM2021-Lab2-HW2
ISA5810 Data Mining Lab 2


## Information
Student Information Name: 姜宏昀

Student ID: 110062592

GitHub ID: hongyuntw

Kaggle Training Code : https://github.com/hongyuntw/DM2021-kaggle

Kaggle name: 四個不同意

Kaggle private scoreboard snapshot:

![snapshot](https://user-images.githubusercontent.com/39511654/148632699-0b2ff663-e1af-4c3c-ae67-b2c9e3bb3772.png)


## Kaggle Report
I use both .py and ipynb files to coding and seperate each steps to make my code easy to follow!

### Preprocessing steps
* preprocess.ipynb
```
def preprocess_tweet(text):
    new_text = []
    for t in text.split():
        if t == '<LH>':
            continue
        t = '@user' if t.startswith('@') and len(t) > 1 else t
        t = 'http' if t.startswith('http') else t
        t = t.lower()
        
        
        new_text.append(t)
    return " ".join(new_text)
````
this is the function i used in preproecssing
* replace all username (@xxxx) to @user
* replace url to http
* lower case
* remove '\<LH>' tag

### Explanation of your model

I use BERT based classification model for this competition
i tried these pretrained BERT based model
* fine-tune roberta-large
* fine-tune  'cardiffnlp/twitter-roberta-base-emotion'

### The feature engineering steps 
* dataset.py
* the model input is
    * [CLS] [tweet text] [hash tags] [SEP]
    * I add all hash tags in text behind the text, it's will has better result 

### Different things you tried and insights you gained.
* I found that in our training data, the data is imbalanced, so I add class weight when calculate cross entropy loss
    * but the special thing is, if we use class_weight when training, we will get wrost on testing set (kaggle)
    * so I dont use class weight when training

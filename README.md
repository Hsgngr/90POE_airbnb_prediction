# 90POE Data Science Take Home Test: AirBnb Price Prediction

This repository outlines my approach to the 90 POE's Take Home Task. The given data is detailed listing information for AirBnb properties in Berlin. The goal of the task was open and an opportunity to showcase my strengths. I aim to answer these questions:

* What insights can you gather ? 
* How can you visualize the data ? 
* What is suprising for you about the data?
* Create a ML model that can predict the listing price from the other information in the data file, then evaluate your model.

## Table of contents
- [90POE Data Science Take Home Test](#90poe-data-science-take-home-test-airbnb-price-prediction)
- [Table of Contents](#table-of-contents)
- [Getting Started](#getting-started)
- [Data Preprocessing and Feature Engineering](#data-preprocessing-and-feature-engineering)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Modelling and Results](#data-modelling-and-results)
- [Future Work](#future-work)

## Getting Started
This repository aims to explain the process of how I handled the project. I used jupyter-notebooks to make my data analysis process more visibly clear and interpretable. Since the task has also a presentation, I included some visualizations on the Exploratory Data Analysis part.(EDA)


* `eda.ipynb` is the exploratory data analysis and preprocessing notebook.
* `training.ipynb` is training of machine learning model for predicting price values also includes feature selection.
* `nlp.ipynb` is my attempt to predict the room size from the space column of airbnb data by utilizing NLP
* `data` folder includes raw and processed data

## Data Preprocessing and Feature Engineering
My steps can be listed as:

Preprocessing:
* Drop useless columns
* Drop text columns for now
* Drop 51 rows with many nan values
* Categorize columns
* Replace NaN rows in cleaning_fee and security deposit as 0.
* Remove $ sign from price columns
* Remove % sign from host_response_rate
* Remove abnormal prices

Feature Engineering:
* Create a distance column from properties coordinates to Berlin's centre
* Create amenities features
* Create host_verification features
* Create a property_size features from the text data by regex


## Exploratory Data Analysis

### Amenities Related
<p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133608303-822eccf3-e8de-4af1-a8c7-dcc18e8bcaaa.png">
</p>
<p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133609722-16907c7f-18cb-468c-ad67-3fd8edc5385f.png">
</p>

### Berlin Map and Neighbourhoods

<p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133525987-ba9d6186-464c-4ca3-838c-0a62e7338e85.png">
</p>

Tells us the distribution of all bookable places on airbnb Berlin but it is hard to generalize. Therefore
I made this interactive map instead of previous plot where you can also see every neighbourhood and their mean prices:

<p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133648909-bd5d16cc-9ede-4f85-a08f-266622fdac39.png">
</p>
 <p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133651065-ebd77cbd-d585-4187-b9f4-73a11b888205.png">
</p>


### Accommodations
 
 <p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133595362-9118d4f0-d533-4b9b-9950-68c1b27e497f.png">
</p>
Well this is suprising, Kreuzberg seems to have the smallest area however have the most airbnb on Berlin. I think this is because of the socio-cultural effect of Kreuzerberg. I know that area is famous with immigrants and also it is in the centre right next to the historical berlin wall.

 <p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133649293-c4097a78-e482-40d7-9d03-dde941c3c1c4.png">
</p>

Distance to the center of the Berlin. The more it gets close the more price varies. Also There are more available airbnbs at the center. 

 <p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133661676-070d4ac3-997f-4744-8f2a-6462635336a6.png">
</p>

 <p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133661609-718ab7dd-bf4d-4a2d-aa04-c4d4a781f561.png">
</p>




## Data Modelling and Results

I selected XgBoost algorithm for my model due to many reasons:
* Can Handle Missing Values
* Easy To Use / Tune
* Fast
* Number of hyper-parameters that can be tuned — a primary advantage over gradient boosting machines.
* Much more interpretable than a neural network, therefore a good start point

I used GridSearch to find the optimal parameters:

  `{'colsample_bytree': 0.6, 'gamma': 0.0, 'learning_rate': 0.05, 'max_depth': 7, 'n_estimators': 400}`

### Results

  `MSE: 26.2054`

 <p align="left">
  <img src="https://user-images.githubusercontent.com/32769732/133750405-a1ed9f5b-dd02-42a4-91da-fe10741ca4fd.png">
</p>

## Future Work

#### Other Datasources
The data has link in it. Most of the links are broken but some of them can be use for data scraping and get other type of data such as images of places.

#### Model
Instead of Xgboost, a neural network can be used to predict the data. We can also create features from text data

#### Text
I would like to explore the text columns and extract more insights especially summary,space and description columns.

Another thing I would like to add is extracting property_size from the text data with Question - Answering Transformers models. I tried one of the huge bert-model which was tuned for Q&A however it didn't give results better than my regex solution.


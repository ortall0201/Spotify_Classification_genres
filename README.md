# Spotify_Classification_genres
Goal of this project: Using ML algorithms for a multi-dimensional Classification of songs' track_genres by features such as energy, danceability, etc. - data taken from a tabular Spotify Dataset from Kaggle.

The latest version combines the best methods from both approaches into a single, consolidated notebook— **Notebook B** —which now serves as the primary analysis and modeling pipeline.

## You can watch the Presentation on this link: [Presentation Link](https://docs.google.com/presentation/d/1hr-RSCL5ESOp1AHJBkojMitimdnu7m9d/edit?usp=drive_link&ouid=108623279518071003366&rtpof=true&sd=true)

# Finding the Genre - Multi-Class Classification
## Date: 12.11.24
## Made by: Ortal Lasry & Or Cohen Raviv

## Business Question:
How can we accurately classify music genres using audio features to improve recommendations and content organization on streaming platforms?

### Background:
We utilized a Spotify dataset from Kaggle, which contains 114 track genres and 14 main numeric features (e.g., duration_ms, danceability). Additionally, it includes a boolean feature indicating explicit content. The dataset originally had 20 columns and 114,000 rows, but after removing duplicates (keeping only the first occurrence), we retained 87,867 rows. The dataset also presents significant class imbalance in the target variable, track_genre.

## Analysis Summary:
Upon preliminary exploration, we observed that certain genres had more track IDs than others, contributing to data imbalance and complicating pattern interpretation due to overlapping characteristics within broader genres. For example, subgenres like 'rock', 'rock-n-roll', and 'alt-rock' fall under the broader 'rock' category. To address this, we grouped them into 10 classes. In addition, we used class imbalance when we fitted the ml models. 

## Feature Engineering and Descriptive Analysis:
Descriptive statistics revealed right-skewed distributions in variables such as duration_ms, speechiness, acousticness, and instrumentalness, while loudness was left-skewed. These patterns guided our feature engineering approach. We applied log transformations to right-skewed variables to capture feature characteristics better and boost model accuracy. We also created polynomial features for tempo and danceability due to their non-linear distributions. We investigated the interaction effects between 'tempo' and 'danceability' (since songs with a higher tempo are more likely to be more danceable) and between 'duration_ms' and 'energy'.
The correlation matrix between all quantitative features revealed a high correlation between energy and loudness (r=0.75) and between energy and acousticness (r=-0.72).

### Bar Chart for the Categorical Feature: 'Explicit' (Presence of Explicit Language):
As expected, some genres have higher frequencies of explicit content than others. For example, Hip Hop and Death Metal show the highest frequencies of explicit content, while Classical music has none.

## Modeling Approach and Evaluation:
In the first step, we split the dataset into training and testing sets (0.3%/0.7%) and used 5 features that exhibited high variance across music genres. We predicted only 5 music genres based on ML models, including Logistic Regression, Voting Classifier, and Random Forest.  We assessed feature importance and found that ‘explicit,’ ‘danceability,’ and ‘speechiness’ made the greatest contributions to reducing Gini impurity. The Random Forest model achieved the highest accuracy (0.8) with a Test ROC AUC score of 0.95.
Following this, we expanded our approach to predict all genres (114 music genres grouped into 10 classes) and included eight features in total. We tested the accuracy score for each model with the original features vs. engineered features. The results showed minor accuracy improvements, leading us to proceed with XGBoost using only the engineered features, which achieved a highest accuracy of 0.5 and a Test ROC AUC of 0.84.

## Project Insights and Future Research:
The main results of our project show:
• Differences in accuracy scores when using small vs. large datasets for music genre classification.
• A stronger contribution of certain features to reducing Gini impurity in music genre classification.
• Some machine learning models outperform others in terms of accuracy (e.g., Random Forest vs. Logistic Regression).
• The importance of using boosting methods to reduce classification bias.
• The need to address data imbalance for better model performance.
• Modest improvements in model accuracy through feature engineering.

## Future Research:
• The strong correlations found between energy, loudness, and acousticness indicate the potential value of performing dimensionality reduction in future studies.
• Exploring additional text-based features or contextual audio data could further enhance model performance.

## For more descriptive details : [Project Details Link](https://docs.google.com/document/d/1s0cfgyKlgBjMYcbDlTA1ioaXl_o8j5se/edit?usp=sharing&ouid=108623279518071003366&rtpof=true&sd=true)

---
# Project Overview (How to view - guidelines)
This repository contains the results and analysis of the genre classification task based on the Spotify dataset. The project is divided into two approaches:

- **Approach A** (Researcher A) uses a preprocessed version of the dataset, including added engeneered features and additional cleanup (this is saved into a file called cleaned_engeneered_dataset.csv being used for the classification in this notebook) for models comparison and evaluation. There is a link activating this file directly in the "Model training" section, so no need to run the initial start of the notebook.

- **Approach B** (Researcher B) uses the raw dataset directly for activation of this notebook, through a direct path created at the beggining of this notebook. This is also the **MASTER notebook** that includes all stages including the part of notebook A and it's direct link (which is mentioned in the related section - see Table Contents).

Both approaches are implemented in separate notebooks, and their results are integrated into a the B notebook which is the MASTER.
---

## Repository Structure

Spotify_Classification_genres/ 

│ 

├── approach_A_notebook.ipynb # Researcher A's analysis notebook (uses EDA-preprocessed-engeneered CSV called 'cleaned_engeneered_dataset.csv')

|       ├── Model_Results (Scoring saved into a csv file for tracking, but are also shown in the evaluation results in the notebook itself. For example the first model_results.csv relates to results of decision tree based models gathered into one csv for convience and tracking). 

├── approach_B_notebook.ipynb # Researcher B's analysis notebook (uses raw CSV) , however the latest version combines the best methods from both approaches into a 
                                                                                 single, consolidated notebook—Notebook B—which now serves as the primary analysis 
                                                                                 and modeling pipeline. Inside you will find a direct link to notebook A.

|

├── data/ 

|    ├── processed_data_for_notebook_A/ # Preprocessed dataset (used in Researcher A's notebook) 

|       ├── dataset.csv # Raw dataset (used in Researcher A's notebook for overview) 

│       ├── final_clean_dataset.csv # Preprocessed dataset after preliminary EDA (This is the file after initial EDA, the same as initial EDA in notebook B) 

│       ├── clean_engeneered_dataset.csv # Preprocessed dataset after preliminary EDA + aditional cleanup + Feature engeneering (used in Researcher A's notebook for the Model training process, which is the comparison between models in different given parameters + evaluation before ensemble)

│    ├── raw_data/ 

│       └── dataset.csv # Raw dataset (used in Researcher B's notebook) 

|

├── documentation/ 

│ ├── Finding_the_genre_Multi_Class_Classification.docx # Detailed descriptions and figures from both notebooks 

│ └── Finding_the_Genre_Project_Report.docx # Project information, context, and goals 

|

├── presentation/ 

│ └── Finding_the_Genre_Project_PresentationNEW.pptx # PowerPoint presentation summarizing project findings 

|

├── LICENSE 

└── README.md # This README file


---

## Notebooks
**approach_A_notebook.ipynb**
This notebook uses a preprocessed dataset, which has undergone initial data cleaning and EDA + added feature engeneered columns. The focus is on comparing classification models (with different given parameters - classes/features) based on this cleaned data before moving on to ensembles.

**approach_B_notebook.ipynb**
This notebook works with the raw dataset directly, and builds a classification ensemble models. - This is also served as the **MASTER notebook** and connects with a link to notebook A model comparison (see Table Contents).

---

## Data

**processed_data_for_notebook_A/**
Contains the preprocessed data used in Researcher A's notebook.

- **dataset.csv**: Raw dataset used initially for an overview (this is also the same dataset from the given link at the intro, taken from Kaggle).
- **final_clean_dataset.csv**: Cleaned dataset after preliminary EDA, used in Researcher A's notebook.
- **clean_engeneered_dataset.csv**: Added feature engeneered columns and another cleanup of duplicates remained in the final_clean_dataset.csv. This is used in the Model training section directly.

**raw_data/**
Contains the raw dataset used in Researcher B's notebook. This is the dataset from Kaggle (a link to this dataset is given in the intro section)

- **dataset.csv**: Raw dataset used directly for model training in Researcher B's notebook.

---

## Documentation
**Finding_the_genre_Multi_Class_Classification.docx**
Detailed descriptions of the classification process, including figures and results from both Researcher A and Researcher B's notebooks.

**Finding_the_Genre_Project_Report.docx**
The project's full report, including context, methodology, goals, and findings.

---

## Presentation
**Finding_the_Genre_Project_PresentationNEW.pptx**
A PowerPoint presentation summarizing the project's methodology, findings, and conclusions.

---

## Requirements
To run the notebooks, ensure you have the following libraries installed:

- pandas
- numpy
- matplotlib
- seaborn

You can also download the notebooks and run them in [Google Colab](https://colab.research.google.com/).

---

## License
This project is licensed under the MIT.

---

## Contact
For questions or further information, please contact:

- **Researcher 1**: [ortalgr@gmail.com]
- **Researcher 2**: [or.cohen.raviv@gmail.com]

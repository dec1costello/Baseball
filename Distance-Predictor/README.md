# **Distance Predictor**
*Author: Declan Costello*

## **[📌 Try Live Model Here!](https://light-weight-distance-predictor.streamlit.app/)**

**Update (Oct 2023)**: I am stoked to announce that Streamlit has hand selected **The Distance Predictor** to be featured in their [gallery of awesome projects!](https://streamlit.io/gallery?category=sports-fun)

## **Project Overview**

Welcome to the **Distance Predictor**. Inspired by [NASA's Distance Predictor](https://www1.grc.nasa.gov/beginners-guide-to-aeronautics/whit/#play-ball), this project harnesses data from [Pybaseball Data](https://github.com/jldbc/pybaseball), specifically from the 2022 MLB Season, to forecast the trajectory of batted ball distances. I am attempting to predict 1st ball contact with ground (or fielder that touches it or stand for homerun, so data set is flawed to begin with in terms of targets im training with, singles doubles most ikely ocasionally too short. With an interest in hitting mechanics and atmospheric influences, the primary aspiration is to contribute meaningful insights to the baseball community). To get a better feel for the visual details, I encourage you to check out the interactive visuals created using [Bokeh](http://bokeh.org/) for [Parts 3-5 on NBViewer](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/). Also, as [Tyler James Burch](https://github.com/tjburch) pointed out, because [Triples are hard to distinguish](http://tylerjamesburch.com/blog/baseball/hit-classifier-1), I combined Triples and Home Runs in my Event visuals.

## **Data Source**

Provided here is a hyperlink to access the processed [CSV dataset](https://drive.google.com/file/d/1tnhLBWTBbbo917c8f9LYwdVHwd-gr5bU/view?usp=sharing) needed for parts 3 through 5. This hyperlink is a much quicker alternative compared to waiting an hour for [Pybaseball's](https://github.com/jldbc/pybaseball) download and it only includes the most important information needed.

## **Table of Contents**

1. [Part 1, Data Exploration](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-1.ipynb)
2. [Part 2, Feature Engineering](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-2.ipynb)
3. [Part 3, Model Selection: XGBoost](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-3.ipynb)
4. [Part 4, XGBoost Parameter Optimization and Insights](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-4.ipynb)
5. [Part 5, Pipeline Synthesis and Results Showcase](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-5.ipynb)


## **Part 1 & 2, [Data Exploration](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-1.ipynb) and [Feature Engineering](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-2.ipynb)**

In Parts 1 & 2, I explore the data and start to feature engineer to help understand, clean, and refine the dataset. It guides model choice and assumption validation, while also revealing insights through visualization. By addressing data quality and understanding patterns early, here I establish a strong foundation for the rest of my project.

<table>

<tbody>
  <tr>
    <td>
      <a href="https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-1.ipynb">
        <img src="https://github.com/dec1costello/Baseball/assets/79241861/b7cee43a-5197-412e-abdb-2f5502605b96" />
      </a>
    </td>
    <td>
      <a href="https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-2.ipynb">
        <img src="https://github.com/dec1costello/Baseball/assets/79241861/4c2d7703-ec7d-4ec4-8e3c-54b8c5ac9941" alt="WOBA Heatmap" />
      </a>
    </td>
</tr>
</tbody>
</table>

## **Part 3, [Model Selection](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-3.ipynb)**

In Part 3, I use grid search to select the best ML model, as it entails choosing the most suitable algorithm for a given task. It ensures optimal use of resources by aligning the algorithm's assumptions with the data characteristics. This leads to better predictive accuracy, efficient training, and successful problem-solving. I trained each model with the same data as well.



<table>

<tbody>
  <tr>
    <td>
      <a href="https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-3.ipynb">
        <img src="https://github.com/dec1costello/Baseball/assets/79241861/11a4414a-7b01-4f05-9625-90a3de21c752" alt="Event Scatter" />
      </a>
    </td>
</tr>
</tbody>
</table>

## **Part 4, [Optimization](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-4.ipynb) & [SHAP](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-SHAP.ipynb)**

In Part 4, I used [Optuna](https://optuna.org/) alongside [sklearn](https://scikit-learn.org/stable/modules/grid_search.html) to achieve optimized hyperparameters for each model. I finally get the magnitude of feature attributions with [SHap's game theoretic approach](https://shap.readthedocs.io/en/latest/) to identified bias and trends.

## **Part 5, [Results](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-5.ipynb)**

In Part 5, I finally [Ensemble](https://scikit-learn.org/stable/modules/ensemble.html) the top four preforming models together using a [VotingRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.VotingRegressor.html#sklearn.ensemble.VotingRegressor) to minimize [Bias](https://towardsdatascience.com/a-quickstart-guide-to-uprooting-model-bias-f4465c8e84bc) and [Variance](https://x.com/akshay_pachaar/status/1703757251474063861?s=20). This iterative process maximized predictive accuracy and ultimately delivered valuable insights leading to a MAE under 10 feet.

```mermaid
graph TB
      FeatureEngineeredData --> CategoricalTransformer;
      FeatureEngineeredData --> NumericTransformer;
      CategoricalTransformer --> OneHotEncoder;
      OneHotEncoder --> Stratify;
      NumericTransformer --> RobustScaler;
      RobustScaler --> Stratify;

      Stratify-->XGBRegressor;
      Stratify-->RandomForestRegressor;
      Stratify-->MLPRegressor;
      Stratify-->GradientBoostingRegressor;
      XGBRegressor-->VotingRegressor;
      RandomForestRegressor-->VotingRegressor;
      MLPRegressor-->VotingRegressor;
      GradientBoostingRegressor-->VotingRegressor;

      VotingRegressor --> Prediction;
```

<table>
<tbody>
  <tr>
    <td>
      <a href="https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-5.ipynb">
        <img src="https://github.com/dec1costello/Baseball/assets/79241861/8f8cfd75-0b0e-42fd-a875-fa9cd5f295f5" alt="Event Scatter" />
      </a>
    </td>
</tr>
</tbody>
</table>

## **[Use Cases](https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-UseCase.ipynb)**

I finally put the [ensemble model](https://scikit-learn.org/stable/modules/ensemble.html) to good use by exploring Optimal PFX for Distance, Optimal Launch Angles by Exit Veloicity for Distance, and Stadium Distance Variation.

<div align="center">
<table>
<tbody>
  <tr>
    <td>
      <a href="https://nbviewer.org/github/dec1costello/Baseball/blob/main/Distance-Predictor/Distance-Predictor-Part-UseCase.ipynb">
        <img src="https://github.com/dec1costello/Baseball/assets/79241861/9fdeb950-71e4-491b-a296-481af8a1076a" alt="Event Scatter" />
      </a>
    </td>
</tr>
</tbody>
</table>
</div>

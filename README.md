# NFL Playoff Appearance Prediction using Neural Networks

<img width="392" alt="Screenshot 2024-10-11 at 2 12 52 PM" src="https://github.com/user-attachments/assets/2334297d-d021-42b2-be30-6846f4a5e9b2">

## Table of Contents
- [Introduction](#introduction)
- [Problem Statement](#problem-statement)
- [Data](#data)
- [Methodology](#methodology)
- [Chosen Model](#chosen-model)
- [Results](#results)
- [Future Work](#future-work)
- [Contributors](#contributors)
- [Acknowledgments](#acknowledgments)

## Introduction
This project aims to predict NFL playoff appearances using Neural Networks. By analyzing team statistics from the 2018 through 2023 NFL seasons, the model generates probabilities for teams making the playoffs. This analysis provides insights into the factors contributing to a team's playoff chances and can aid in strategic decision-making for NFL teams.

## Problem Statement
The goal is to develop a predictive model using Deep Learning to forecast NFL playoff appearances based on relevant team performance metrics. Accurate predictions can assist teams in strategic planning, helping decision-makers target players and coaches who can influence the most critical aspects of the game.

## Data
- **Source**: Data was acquired from [Pro Football Reference](https://www.pro-football-reference.com/)
- **Time Period**: 2018 through 2023 NFL seasons
- **Features**: Include Yards/Play, Net Yards/Pass Attempt, Total Turnovers for Offense/Defense, Penalties Committed by Offense/Defense, and more
- **Target Variable**: "Made_Playoffs" variable was appended from NFL playoff berth data for 2018-2023

<img width="522" alt="Screenshot 2024-10-11 at 2 18 05 PM" src="https://github.com/user-attachments/assets/f04474c9-2f22-443e-8b48-92ca87f233e2">

## Methodology
1. **Data Collection**: Downloaded team stats and web scraped playoff information
2. **Exploratory Data Analysis (EDA)**: Analyzed feature distributions and correlations
<img width="522" alt="Screenshot 2024-10-11 at 2 18 05 PM" src="https://github.com/user-attachments/assets/f04474c9-2f22-443e-8b48-92ca87f233e2"> <img width="474" alt="Screenshot 2024-10-11 at 2 27 12 PM" src="https://github.com/user-attachments/assets/428adfae-0773-4647-97e4-b9fae93f0864">


3. **Feature Engineering**: Created new features like Points Per Play, Yards Per Point, and Turnovers Forced Per Game
4. **Data Preprocessing**: Scaled data using StandardScaler
5. **Model Development**: Experimented with various Neural Network architectures
6. **Model Training and Tuning**: Used training, validation, and test sets; implemented hyperparameter tuning
7. **Model Evaluation**: Assessed models based on Test Accuracy, Test Loss, and overfitting tendency

## Chosen Model
The final chosen model is a Sequential Neural Network with the following architecture and characteristics:

1. **Input Layer**: 
   - Shape determined by the number of features in X_train_scaled

2. **First Hidden Layer**:
   - Dense layer with 64 units
   - Activation function: ReLU (Rectified Linear Unit)
   - Followed by a Dropout layer with rate 0.3

3. **Second Hidden Layer**:
   - Dense layer with 64 units
   - Activation function: ReLU
   - Followed by a Dropout layer with rate 0.4

4. **Output Layer**:
   - Single neuron Dense layer
   - Activation function: Sigmoid (for binary classification)

**Model Compilation**:
- Optimizer: Adam with learning rate of 0.00042644
- Loss function: Binary Crossentropy
- Metric: Accuracy

**Hyperparameters**:
The model's architecture was determined through RandomSearch hyperparameter tuning. The best hyperparameters found were:
```python
{
 'units': 64,
 'dropout': 0.3,
 'units2': 64,
 'dropout2': 0.4,
 'learning_rate': 0.0004264401157975197
}
```

**Training Process**:
- Epochs: 100 (maximum)
- Batch Size: 32
- Early Stopping: Monitored 'loss' with a patience of 5 epochs, restoring best weights

This architecture, with two hidden layers of 64 units each and dropout for regularization, strikes a balance between model complexity and generalization ability. The dropout rates of 0.3 and 0.4 help prevent overfitting by randomly setting a fraction of input units to 0 during training. The use of ReLU activation in hidden layers allows for non-linear transformations of the data, while the sigmoid function in the output layer is appropriate for binary classification, outputting probabilities between 0 and 1. The Adam optimizer with a learning rate of approximately 0.00043 was found to be optimal for this problem, allowing for efficient convergence during training. Early stopping is implemented to prevent overfitting, halting training when the loss stops improving and restoring the best weights found during training.

**Model Performance
This model performed best, compared to other more complex models, in terms of test loss and accuracy. It did the best job at not overfitting to the training data and being generalizable to new data. 

<img width="611" alt="Screenshot 2024-10-11 at 2 43 18 PM" src="https://github.com/user-attachments/assets/9474a6fc-8627-4e31-bae7-77e16a85beb2">
<img width="148" alt="Screenshot 2024-10-11 at 2 43 53 PM" src="https://github.com/user-attachments/assets/934951a1-8a4a-4e6d-b4e6-f33d984bbc8b">
<img width="172" alt="Screenshot 2024-10-11 at 2 47 04 PM" src="https://github.com/user-attachments/assets/de8dd3cb-1858-4067-a101-d1366b7717bb">

## Results
- The model effectively predicts playoff probabilities for NFL teams
- Once playoff probabilities calculated from the model were calculated, the probabilities were appended back to the correct teams in their respective year
- Consistent with real-world outcomes (e.g., Kansas City Chiefs' high average playoff probability)
- Captures nuances of team performance, with some exceptions (e.g., 2023 Pittsburgh Steelers)



<p align="center"><img width="417" alt="Screenshot 2024-10-11 at 2 50 52 PM" src="https://github.com/user-attachments/assets/0e29271f-3fa7-47c9-b2c1-afa41428bf8b"><br><i>Average Playoff Probability From 2018-2023</i>
</p>

## Future Work
- Expand the dataset to include more seasons
- Incorporate injury and weather data for context
- Explore more complex models like LSTM networks to capture temporal dependencies

## Contributors
- Mike Meissner (mmeissner@uchicago.edu)

## Acknowledgments
- Data source: Pro Football Reference (https://www.pro-football-reference.com/)

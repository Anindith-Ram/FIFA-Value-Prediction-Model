[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/ZXxkiClO)

# FIFA Player Rating Machine Learning Modeling Course Project
## Anindith Ram

## BOX LINK FOR VIDEO WALKTHROUGHS: 
https://cmu.box.com/s/rsdfip9kmpv807tyd5j1qic65puyqaj0

## Project Repository Files:
- Course Project.ipynb
- data (FIFA Dataset is contained in this folder)
- KAFKA Consumer (ProjConsumer.ipynb)
- KAFKA Producer (ProjProducer.ipynb)
- FIFA Schema:Dataset Creation.sql (SQL query to create the PostgreSQL database)

## How to use this repository:

### Required Dependencies
#### Core Python Packages:
- pyspark
- numpy
- pandas
- matplotlib
- torch
- streaming
#### Installation Commands
````
pip install pyspark numpy pandas matplotlib torch
pip install mosaicml-streaming
````
**PostgreSQL / pgAdmin**
- Create database and schema in Postgres
- CREATE DATABASE fifa;
- CREATE SCHEMA IF NOT EXISTS fifa;
- CREATE TABLE fifa.player_data (with id SERIAL PRIMARY KEY, all FIFA Dataset columns, plus added year and gender).

**Running Local Code:**
- Inputs are not required to run code apart from Task 2 Part 1, 2, 3 and 4.
- For Task 2 Part 5, please run the consumer before the producer. Make sure you have confluent and in topics add youtube_topic.
- Kafka Producer requires GCP API key. Please insert yours at the top of the ProjectProducer.ipynb Notebook.
- Found in Google cloud console > Youtube API v3 > Manage > Credentials > Show / Create API Key
- Should run for just under 5 mins 30 seconds and returns comments and most popular footballer + json dump with all comments.
- We recommend that when you create your MDS datasets that you organize your local folder.
  

**Using GCP:**
**(Casting for Google Cloud)**
- Only required details are to upload fifa dataset files straight to bucket each (not as a folder).
- Ensure numerical columns are cast to double or int in GCP as the schema inferred by the GCP web instance may possibly miscast feature datatypes
- For our case we had to cast: mentality_composure, wage_eur and value_eur
- Be sure to check the schema has the appropriate datatypes for each feature
  
**Notes:**
- Java is required for PySpark (Java 11 is used in this repository's code)
- The Jupyter notebook (Course Project.ipynb) uses PySpark's Machine Learning library for the Random Forest and Linear Regression Models
- PyTorch is used to create the neural networks (MLPs)
- It is recommended to create a virtual environment with all of the required dependencies installed to ensure ease of use.

## Dataset:
This FIFA dataset contains 112 features spanning multiple categories:
- Player ID and biographic/physical attributes:
    15 features
- Club/National team and contract information:
    17 features
- Player ratings (Overall and Position-specific):
    36 features
- Detailed player attributes:
    37 features
- Additional information (player face, club/national logo/flag urls):
    7 features

| **Feature** | **Data Type** | **Description** |
|--------------|---------------|-----------------|
| sofifa_id | integer | Unique player identifier from the SoFIFA database |
| player_url | string | URL link to the player’s SoFIFA profile page |
| short_name | string | Commonly used player name |
| long_name | string | Full name of the player |
| player_positions | string | List of the player’s preferred positions (e.g., “RW, CF”) |
| overall | integer | Overall rating of the player’s current ability |
| potential | integer | Player’s maximum possible rating based on potential |
| value_eur | double | Market value of the player in euros |
| wage_eur | double | Wage of the player in euros |
| age | integer | Player’s current age |
| dob | date | Date of birth of the player |
| height_cm | integer | Player’s height in centimeters |
| weight_kg | integer | Player’s weight in kilograms |
| club_team_id | double | Unique identifier for the player’s club |
| club_name | string | Name of the club the player belongs to |
| league_name | string | Name of the league in which the player’s club competes |
| league_level | long | League division level (1 = top tier, higher = lower divisions) |
| club_position | string | Player’s primary position in the club’s lineup |
| club_jersey_number | long | Jersey number worn by the player at their club |
| club_loaned_from | string | Name of the club the player is loaned from (if applicable) |
| club_joined | date | Date the player joined their current club |
| club_contract_valid_until | long | Year until which the player’s contract is valid |
| nationality_id | integer | Unique identifier for the player’s nationality |
| nationality_name | string | Player’s nationality (country name) |
| nation_team_id | double | Identifier for the player’s national team (if applicable) |
| nation_position | string | Position played for the national team |
| nation_jersey_number | integer | Jersey number worn for the national team |
| preferred_foot | string | Dominant foot |
| weak_foot | integer | Rating of weaker foot ability (1–5) |
| skill_moves | integer | Rating for skill move proficiency (1–5) |
| international_reputation | integer | Reputation rating on international scale (1–5) |
| work_rate | string | Describes attacking and defensive work rate (e.g., “High/Medium”) |
| body_type | string | Physical body type classification (e.g., “Lean”, “Stocky”) |
| real_face | string | Indicates whether the player’s face is real (scanned likeness) |
| release_clause_eur | long | Player’s release clause value in euros |
| player_tags | string | Special gameplay tags (e.g., “Speedster”, “Playmaker”) |
| player_traits | string | Specific traits influencing in-game behavior (e.g., “Finesse Shot”) |
| pace | integer | Composite rating for player’s running speed |
| shooting | integer | Composite rating for shooting accuracy and power |
| passing | integer | Composite rating for passing ability |
| dribbling | integer | Composite rating for dribbling and ball control |
| defending | integer | Composite rating for defensive ability |
| physic | integer | Composite rating for physical attributes (strength, stamina) |
| attacking_crossing | integer | Accuracy of crosses from wide areas |
| attacking_finishing | integer | Accuracy and consistency in finishing chances |
| attacking_heading_accuracy | integer | Accuracy when heading the ball |
| attacking_short_passing | integer | Accuracy of short-distance passes |
| attacking_volleys | integer | Ability to strike the ball on the volley |
| skill_dribbling | integer | Dribbling control and responsiveness |
| skill_curve | integer | Ability to curve the ball (useful for free kicks) |
| skill_fk_accuracy | integer | Accuracy of free kicks |
| skill_long_passing | integer | Accuracy of long-distance passes |
| skill_ball_control | integer | Ability to control the ball upon receiving it |
| movement_acceleration | integer | Rate at which the player reaches top speed |
| movement_sprint_speed | integer | Maximum sprinting speed |
| movement_agility | integer | Agility and responsiveness to direction changes |
| movement_reactions | integer | Speed of reacting to events on the pitch |
| movement_balance | integer | Stability and control while moving or under pressure |
| power_shot_power | integer | Power behind the player’s shots |
| power_jumping | integer | Jumping height and effectiveness |
| power_stamina | integer | Ability to maintain performance over time |
| power_strength | integer | Physical strength in challenges |
| power_long_shots | integer | Accuracy and power of long-distance shots |
| mentality_aggression | integer | Level of aggression in duels |
| mentality_interceptions | integer | Ability to anticipate and intercept passes |
| mentality_positioning | integer | Off-the-ball attacking positioning |
| mentality_vision | integer | Ability to spot and execute passes |
| mentality_penalties | integer | Penalty-taking ability |
| mentality_composure | long | Player’s composure and decision-making under pressure |
| defending_marking_awareness | integer | Awareness in marking opponents |
| defending_standing_tackle | integer | Effectiveness in standing tackles |
| defending_sliding_tackle | integer | Effectiveness in sliding tackles |
| goalkeeping_diving | integer | Diving ability (goalkeepers) |
| goalkeeping_handling | integer | Handling ability (goalkeepers) |
| goalkeeping_kicking | integer | Kicking accuracy and distance (goalkeepers) |
| goalkeeping_positioning | integer | Positional awareness (goalkeepers) |
| goalkeeping_reflexes | integer | Reflex speed (goalkeepers) |
| goalkeeping_speed | integer | Overall movement speed (goalkeepers) |
| ls, st, rs, lw, lf, cf, rf, rw, lam, cam, ram, lm, lcm, cm, rcm, rm, lwb, ldm, cdm, rdm, rwb, lb, lcb, cb, rcb, rb, gk | string | In-game overall rating of the player when placed in that specific position |
| player_face_url | string | URL to the player’s in-game face image |
| club_logo_url | string | URL to the club’s logo image |
| club_flag_url | string | URL to the club’s flag image |
| nation_logo_url | string | URL to the national team’s logo image |
| nation_flag_url | string | URL to the national flag image |
| gender | string | Player’s gender |
| year | integer | Dataset year |

## NoSQL or PostgreSQL?
In this specific case, it would be better to use a PostgreSQL database instead of a NoSQL database such as Neo4J. This dataset is highly structured and relational, and a relational database like PostgreSQL would allow for efficient querying and filtering, and enable smooth integration into data analytics tools such as Spark and Pandas. A NoSQL database such as Neo4J would be useful if the goal was to analyze the relationships between players and teams or to visually explore the relationships between players, clubs, and leagues.

# Machine Learning Modeling
## Random Forest Regressor
**Why we chose it:** Random Forest is an ensemble method that combines multiple decision trees, making it effective against overfitting and capable of capturing non-linear relationships in the data. It handles mixed feature types and large datasets well.
**Hyperparameter Impact:**
- **Number of Trees (`numTrees`)**: Tested values [10, 20]. More trees generally improve performance by reducing variance through averaging. Our best model used 20 trees, indicating that the extra complexity is ideal for this dataset.
- **Max Depth (`maxDepth`)**: Tested values [5, 10]. Deeper trees can capture more complex patterns but risk overfitting. The optimal depth of 10 suggests that our dataset benefits from the ability to model more intricate feature relationships.

**Performance:** Achieved the best test RMSE of **1.35**, significantly outperforming all other models. This demonstrates that the ensemble approach and non-linear decision boundaries are well-suited for predicting player values.

## Linear Regression Model
**Why we chose it:** Linear Regression serves as a baseline model, providing interpretability and computational efficiency. It helps establish a performance floor and allows us to assess whether more complex models are justified. Also, it's useful for understanding linear relationships between features and target values.
**Hyperparameter Impact:**
- **Max Iterations (`maxIter`)**: Tested values [5, 10]. More iterations allow the optimization algorithm to converge closer to the optimal solution. Interestingly, our best model used only 5 iterations, suggesting that the algorithm converges quickly on this dataset, and additional iterations may lead to slight overfitting.
- **Regularization Parameter (`regParam`)**: Tested values [0.00001, 0.0001]. Higher regularization penalizes large coefficients, reducing overfitting. The optimal value of 1e-05 (the minimum tested) indicates that the model benefits from minimal regularization, implying that overfitting is not a significant concern with this linear model.

**Performance:** Achieved a test RMSE of **3.07**, which is more than twice the Random Forest model. This significant gap highlights the limitations of linear models when dealing with complex, non-linear relationships that exist in the dataset.

**Note:** Due to limited computational resources, only a small set of hyperparameter combinations were tested.

## Deep Multi-Layer Perceptron (4 Hidden Layer)
**Why we chose it:** Deep neural networks can learn complex feature relationships. With architecture 34 → 256 → 128 → 64 → 32 → 1, this model has enough capacity to generalize non-linear relationships. We wanted to explore whether increased model depth would improve performance over simpler models.

**Hyperparameter Impact:**
- **Learning Rate (`lr`)**: Tested values [0.001, 0.005]. The training of this model is quite erratic. Across epochs, RMSE values oscillate rather than steadily decreasing, regardless of learning rate. The best configuration used lr=0.001, achieving a validation loss of 49.47 (validation RMSE ~7.03) and test RMSE of 7.08. The erratic behavior suggests that the model may be sensitive to initialization or that the loss landscape has multiple local minima. The oscillations indicate potential instability in the training process, possibly due to the model's high capacity relative to the dataset size.
- **Batch Size (`batch_size`)**: Tested values [64, 128]. Interestingly, smaller batch sizes (64) performed better than larger ones (128) for this model. The best configuration (lr=0.001, batch_size=64) achieved a test RMSE of 7.08. The smaller batch size may provide more frequent gradient updates, which appears to help the model converge better despite the training instability. This contrasts with expectations where larger batches provide more stable gradient estimates.

**Performance:** Achieved a best test RMSE of **7.08**, which is significantly worse than both Random Forest and Linear Regression. The erratic training behavior and poor performance suggest that the model may be overfitting or struggling to converge effectively, despite its theoretical capacity for complex relationships.

## Shallow Multi-Layer Perceptron (1 Hidden Layer)
**Why we chose it:** A shallow network with architecture 34 → 16 → 1 provides a middle ground between linear models and deep networks. It can capture non-linear relationships while maintaining simplicity and faster training. This model helps us understand whether a small amount of non-linearity is enough for this task.
**Hyperparameter Impact:**
- **Learning Rate (`lr`)**: Tested values [0.0005, 0.001]. The training of this model is consistently smooth. The initial loss value may be large, but after the first few epochs of training, the RMSE values in each epoch improve steadily. The best configuration used lr=0.001, achieving a validation loss of 49.87 (validation RMSE ~7.06) and test RMSE of 7.00. This suggests that a slightly higher learning rate works well for this shallow architecture, allowing for efficient convergence while maintaining stability.
- **Batch Size (`batch_size`)**: Tested values [64, 128]. Tested values [64, 128]. Smaller batch sizes (64) consistently performed better than larger ones (128) for this model. The best configuration (lr=0.001, batch_size=64) achieved a test RMSE of 7.00. This aligns with the deep MLP results, where smaller batches also performed better. The smaller batch size provides more frequent gradient updates, which appears to help the model converge better for this simpler architecture. The hyperparameter adjustments show meaningful impact, with the best configuration achieving a test RMSE of 7.00 compared to other configurations that achieved values around 7.09-7.15.

**Performance:** Achieved a best test RMSE of **7.00**, which is slightly better than the deep MLP but still significantly worse than Random Forest and Linear Regression. The smooth training curve indicates stable optimization, but the performance suggests that the single hidden layer may not be sufficient to capture the necessary non-linear patterns.

**Note:** As seen from our training process, the adjustments of our hyperparameters have marginal effect on the performance of the MLPs, with all configurations achieving test RMSE values around 7. This may suggest that the MLPs may be reaching a performance plateau that is limited by the inherent complexity of the problem/dataset rather than hyperparameter settings.

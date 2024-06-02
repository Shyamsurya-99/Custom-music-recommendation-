# Custom-music-recommendation
# Personalized Automatic Playlist Generation Using AH-DQN

This repository contains the code and methodology for the project "Personalized Automatic Playlist Generation Using AH-DQN". This project leverages reinforcement learning techniques to adaptively suggest songs based on user preferences, enhancing the novelty and diversity of recommendations.

## Team Members

- **K.R. Vishwajith** - CB.EN.U4AIE21020
- **Kishore DM** - CB.EN.U4AIE21024
- **Shyam Surya G** - CB.EN.U4AIE21063
- **Steven J** - CB.EN.U4AIE21066

## Problem Statement

In recent years, music recommendation systems have gained substantial attention, leveraging machine learning techniques to suggest songs that match user preferences. Traditional recommendation systems often rely on collaborative filtering or content-based filtering, which may not effectively capture the dynamic nature of user preferences. Reinforcement learning (RL) specifically works better in sequential decision-making problems, making it suitable for playlist generation.

This project introduces an Action Head Deep Q-Network (AH-DQN) based music recommender system that uses RL to adaptively suggest songs based on user preferences.

## Dataset

The dataset comprises 1000 songs, each described by 21 features representing various musical attributes. These features include temporal elements (e.g., "1980s", "1990s"), genres (e.g., "Pop", "Rock", "Country"), and other stylistic characteristics (e.g., "Love", "Metal", "Acoustic"). The features are binary indicators specifying the presence or absence of each attribute for a given song.

The dataset can be accessed and downloaded from Kaggle using the following link: [VQA-RAD: Visual Question Answering Radiology](https://www.kaggle.com/datasets/mdzeeshanhassan/vqa-rad-visual-question-answering-radiology)

## Methodology

### Virtual Environment and Agent Training

#### Offline Mode

In offline mode, the agent is trained using a simulated environment with virtual users. This training involves:

- **World Model**: A simulated user with randomized preferences across the 21 song features. The reward for recommending a song is calculated as the dot product of the user's preferences and the song's features, representing how well the song matches the user's tastes.
- **Training Process**: The agent interacts with the World Model over many episodes, each starting with the virtual user's initial preferences. In each episode, the agent selects a song (action) based on its current state (user preferences) and receives a reward. The agent updates its experience replay memory with state, action, reward, next state, and done flag. The agent periodically samples batches from this memory to perform gradient descent updates on the neural network, improving its policy over time. The epsilon-greedy policy decays epsilon over time to transition from exploration to exploitation.

#### Online Mode

In online mode, the agent directly interacts with actual users:

- **User Interaction**: Users specify their preferences by selecting features they like. The agent uses the trained model to recommend a playlist of songs that align with these preferences. The agent generates a playlist by sequentially selecting songs, ensuring novelty by avoiding previously recommended songs. Users can provide feedback by updating their preferences, allowing the agent to adjust its recommendations dynamically.

### Action Head Deep Q-Network (AH-DQN) Algorithm

The AH-DQN algorithm enhances traditional DQN with an action head architecture to manage song recommendations effectively.

#### Network Structure

- The input layer combines the state (user preferences) and action (song features) vectors.
- Two hidden layers with ReLU activation functions process the combined input.
- The output layer produces a single Q-value representing the expected reward for the state-action pair.

#### Action Selection

- During exploration, the agent randomly selects actions (songs) ensuring diversity and novelty.
- During exploitation, the agent selects the action with the highest predicted Q-value guided by the trained model.

#### Training Dynamics

- The model's parameters are optimized using the Adam optimizer and mean squared error loss function.
- Periodic updates to the target model ensure stable learning by providing consistent Q-value targets.

## Results

- **Difference Between DQN and AH-DQN**:
  - Results for 500 episodes
  - Results for 1000 episodes
  - Results for 50000 episodes

- **Metrics**:
  - Episodes vs Reward
  - Loss
  - Q-Value
  - How Epsilon decays over Episodes
  - Reward Distribution
  - Loss Distribution
  - Action Distribution
  - How Preferences of Virtual User Aligns with song features over time

## Implementation

For detailed implementation and code, please refer to the Jupyter notebooks provided in this repository.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

Thank you for your interest in our project. If you have any questions or feedback, please feel free to reach out to us.

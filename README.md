# Checkers Reinforcement Learning Agent

A self-learning checkers AI that uses linear function approximation and gradient descent to learn optimal gameplay strategies through self-play.

## Overview

This project implements a reinforcement learning agent that learns to play checkers by training against a random opponent. Using a linear model with hand-crafted features and the Least Mean Squares (LMS) weight update rule, the agent achieves strong performance after minimal training.

## Results

After 100 training games:
- **Player 1 (RL Agent) Wins:** 87%
- **Player 2 (Random) Wins:** 6%
- **Draws:** 7%

**Learned Weights:**
```
[34.44, 9.02, -5.21, 14.78, 4.40, -0.70, -2.54]
```

## How It Works

### Architecture

The system follows a classic reinforcement learning loop:

1. **Experiment Generator** - Initializes game boards
2. **Performance System** - Plays games using learned weights
3. **Critic** - Evaluates game history and generates training samples
4. **Generalizer** - Updates weights using gradient descent

### Features (7-dimensional vector)

| Feature | Description |
|---------|-------------|
| `x[0]` | Bias term (always 1) |
| `x[1]` | Number of player's regular pieces |
| `x[2]` | Number of opponent's regular pieces |
| `x[3]` | Number of player's kings |
| `x[4]` | Number of opponent's kings |
| `x[5]` | Number of capture opportunities for player |
| `x[6]` | Number of capture opportunities for opponent |

### Learning Algorithm

- **Method:** Linear function approximation with LMS gradient descent
- **Learning Rate:** 0.005
- **Reward Structure:** +100 (win), -100 (loss), 0 (draw)
- **Training Opponent:** Random move selection

## Installation

```bash
# Clone the repository
git clone https://github.com/Naveen-1-1/ai-checkers-reinforcement-learning-agent.git
cd ai-checkers-reinforcement-learning-agent

# Install dependencies
pip install numpy
```

## Game Rules Implemented

- Standard 8x8 checkers board
- Diagonal movement only
- King promotion at opposite end
- Jump captures (single jumps)
- Regular moves when no jumps available

## Code Structure

```
checkers_model.ipynb
├── Board Management
│   ├── initializeBoard()
│   ├── displayBoard()
│   └── makeKings()
├── Move Validation
│   ├── checkMove()
│   ├── checkCross()
│   └── getLegalMoves()
├── Game Logic
│   ├── isGameOver()
│   └── getCheckerHistory()
├── Learning System
│   ├── getFeatures()
│   ├── getIntermediateBoardScore()
│   ├── getFinalBoardScore()
│   ├── getTrainingData()
│   └── gradientDescent()
└── Decision Making
    ├── chooseMove()
    └── chooseRandomMove()
```

## Technical Details

**Board Representation:**
- 8x8 2D array
- `'W'` - White piece
- `'B'` - Black piece
- `'KW'` - White king
- `'KB'` - Black king
- `' '` - Empty square

**Training Process:**
1. Generate initial board state
2. Agent (White) makes optimal move based on current weights
3. Opponent (Black) makes random move
4. Repeat until game ends
5. Score all board states in game history
6. Update weights using gradient descent
7. Repeat for N training games

## Limitations & Future Work

- **Training opponent:** Currently uses random moves; could implement minimax or self-play
- **Jump rules:** Does not enforce forced jumps or multi-jump chains
- **Features:** Limited feature set; could add positional strategy features
- **Learning:** Fixed learning rate; could implement adaptive methods
- **Model persistence:** No save/load functionality for trained weights

### Potential Improvements

- [ ] Implement forced jump rule enforcement
- [ ] Add multi-jump chain support
- [ ] Implement TD-learning for better credit assignment
- [ ] Add experience replay for more stable learning
- [ ] Create evaluation suite with multiple difficulty opponents
- [ ] Add visualization of learning curves
- [ ] Implement model checkpointing

## Dependencies

- Python 3.6+
- NumPy
- Standard library: `random`, `copy`

## License

MIT License - feel free to use and modify for your projects.

## Acknowledgments

Based on reinforcement learning principles from machine learning, implementing concepts of temporal difference learning and function approximation for game AI.

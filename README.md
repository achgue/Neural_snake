# Neural network for snake
(in progress...)

This project is based on RL (**Reinforcement Learning**), in other words we are techinng a software agent (in this case our player) how to behave based on how good it's doing.
We actually are going to reward the agent every time he is doing good. By doing this he will understand if he has done good actions.
**Deep Q learining**: approach that extends Reinforcement Learning by using deep neural networks to predict the actions.

Agent
---
    - Game
    - Model
        Training loop:
            -state = get_state(Game)
            -action = get_move(state) --> next action
                -Model.predict() --> is used to predict the next action
            -reward,game_over,score = game.play_step(action)
            -new_state = get_state(game) --> this is calculated with the information above
            -remember --> we store new and old state, game_over state and the score
            -Model.train() --> using remember we train our model
Game
---
we have a game loop, within each iteration called **play_step**(_action_). This procedure takes as argument an action that tells the snake what move it has to do.
After the move the procedure will return the reward, and if the game it's over it will return the score

Model
---
DNQ = contains remember information
We use Linear_QNet(DNQ) which is a function that recives the information we remembered to create a linear neural network (with linear layers). Than we will call Model.predict(state) to predict the next action

Reward
---
Whenever our snake eats food +10
Game over -10
else 0

Action
---
We dont want our snake to make strange moves like going rigth and than imediatly left (it would result in a 180° rotation).
So we are implementing 3 states of movement:
    -straight -> [1,0,0] --> we stay on the current direction
    -turn right -> [0,1,0]
    -turn left -> [0,0,1]

State
---
11 values
    [danger_left, danger_right, danger_straight,
    direction_left, direnction_right,
    directon_up, direction_down,
    food_left, food_right,
    food_up, food_down]

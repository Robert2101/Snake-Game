# Snake Game

## Short Description

A classic Snake game built using Python and the `turtle` graphics library. The player controls a snake that grows in length each time it eats food, with the objective of achieving the highest possible score without colliding with the walls or the snake's own body.

## Features

- Interactive graphical user interface using `turtle`
- Real-time snake movement with keyboard controls (arrow keys)
- Randomly generated food items
- Score tracking and persistent high score saved to file
- Snake grows with each food item eaten
- Collision detection with walls and self
- Game over and restart functionality

## Installation Instructions

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Robert2101/Snake-Game.git
   cd Snake-Game
   ```

2. **Ensure Python is installed:**
   - Requires Python 3.x

3. **Install dependencies:**
   - The game uses Python’s built-in `turtle` module, which is included with most Python installations.
   - No external packages are required.

## Usage

To start the game, run `main.py`:

```bash
python main.py
```

Use the arrow keys (`Up`, `Down`, `Left`, `Right`) to control the snake.

### Example Code Snippets

**main.py** (Game loop and controls):

```python
from turtle import Screen
from Snake import Snake
from Food import Food
from Scoreboard import Scoreboard
import time

screen = Screen()
screen.setup(width=600, height=600)
screen.bgcolor("black")
screen.title("My Snake Game")
screen.tracer(0)

snake = Snake()
food = Food()
scoreboard = Scoreboard()

screen.listen()
screen.onkey(snake.up, "Up")
screen.onkey(snake.down, "Down")
screen.onkey(snake.left, "Left")
screen.onkey(snake.right, "Right")

game_is_on = True
while game_is_on:
    screen.update()
    time.sleep(0.1)
    snake.move()

    # Detect collision with food
    if snake.head.distance(food) < 15:
        food.refresh()
        snake.extend()
        scoreboard.increase_score()

    # Detect collision with wall
    if snake.head.xcor() > 280 or snake.head.xcor() < -280 or snake.head.ycor() > 280 or snake.head.ycor() < -280:
        scoreboard.reset()
        snake.reset()

    # Detect collision with tail
    for segment in snake.segments:
        if segment == snake.head:
            pass
        elif snake.head.distance(segment) < 10:
            scoreboard.reset()
            snake.reset()

screen.exitonclick()
```

## Technologies Used

- **Python 3.x**
- **turtle** (standard library module for basic graphics)

## Contributing Guidelines

1. Fork the repository and create your branch from `main`.
2. Make your changes with clear, descriptive commit messages.
3. Run and test the game to ensure it works as expected.
4. Open a pull request with a summary of your changes.

Feel free to open issues or suggest features!

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

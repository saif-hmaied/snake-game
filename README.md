# Snake Game

A classic Snake game for the Windows console, written in C. The snake is stored as a doubly linked list, and the game can save your progress and keep track of your best score.

The in-game menu and messages are in French.

## Features

- 20 x 20 board with walls (18 x 18 playable area)
- Two pieces of food on the board at all times
- Snake keeps moving on its own, one step about every 0.2 seconds
- Save a game and continue it later
- Best score kept between sessions

## Requirements

- Windows (the game uses `windows.h` and `conio.h`)
- A C compiler such as [MinGW](https://www.mingw-w64.org/) (`gcc`)

## Getting started

Clone the repository:

```bash
git clone https://github.com/saif-hmaied/snake-game.git
cd snake-game
```

Build and run it:

```bash
gcc main.c -o main.exe
main.exe
```

A compiled `main.exe` is also included in the repository.

Run the game from the project folder, because it reads `best_score.txt` and `saved_game.txt` from the current directory and will not work without them.

## How to play

### Menu

| Key | Action |
| --- | --- |
| `1` | Continue the saved game (*Continuer la Partie*) |
| `2` | Start a new game (*Nouvelle Partie*) |
| `3` | Quit (*Quitter le jeu*) |

### Controls

The controls are laid out for an AZERTY keyboard. Keys are lowercase only, so keep Caps Lock off.

| Key | Action |
| --- | --- |
| `z` | Move up |
| `s` | Move down |
| `q` | Move left |
| `d` | Move right |
| `a` | Save and return to the menu |

In a new game, the snake waits for your first key press before it starts moving.

### Board

| Symbol | Meaning |
| --- | --- |
| `#` | Wall |
| `+` | Food |
| `^` `v` `<` `>` | Snake head, pointing in the current direction (`@` before the first move) |
| `*` | Snake body |

### Rules

- Each piece of food makes the snake one segment longer and adds 10 points.
- The game ends if the snake hits a wall or its own body.

## Saved data

| File | Contents |
| --- | --- |
| `best_score.txt` | The highest score so far |
| `saved_game.txt` | `1` if a saved game is available, otherwise `0` |
| `last_saved_game.txt` | The food positions on the first line, then one `row column` pair per snake segment, starting from the head |

A save can be continued once: loading it sets `saved_game.txt` back to `0`.

## Code overview

All of the code is in `main.c`:

| Function | Purpose |
| --- | --- |
| `create_snake`, `add_to_the_tail`, `free_snake` | Build, grow and free the linked list |
| `fill_board`, `draw_snake`, `draw_food`, `print_board` | Draw each frame |
| `read_keyboard`, `get_char_with_timeout` | Read input without stopping the game |
| `move_snake` | Move the snake and handle collisions and food |
| `setup_game`, `setup_saved_game`, `save_game` | Start, load and save a game |
| `get_max_score`, `check_for_best_score` | Read and update the best score |

The board size, starting length and number of food items are defined as constants at the top of the file. The save format and the `Food` struct assume two food items.

## Known issues

- The first game after launching the program starts with 10 points, because the first key press adds a segment.
- If the first key press in a game is not a movement key, the game ends immediately.
- Games started after the first one, in the same session, begin moving straight away in the previous direction.
- Food can appear on top of the snake or on the other piece of food.
- The final score is cleared from the screen as soon as the game ends.

## Authors

- Saif Hmaied
- Ayoub Sliti

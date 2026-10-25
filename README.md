# Alpha & Omega

A turn-based werewolf strategy game for two players, played in the terminal, written in Python during my
first year of computer science at the University of Namur (2022). Two packs fight on a grid: each pack
has an **alpha**, an **omega** and normal werewolves, and the first player whose alpha dies loses.

It was a group project for four students; I wrote most of the code
(1,584 of the 1,590 lines added to the engine and the AI in the original history).

## Rules in short

- Every round, each player gives orders to their wolves: move, eat, attack or pacify.
- Wolves gain and lose **energy**: eating food on the map (berries, apples, mice, rabbits, deer) restores
  it, fights cost it.
- Wolves near their alpha get a +30 bonus, near other pack members +10, so formations matter.
- The **omega** can spend 40 energy to *pacify* the enemy wolves around it for one round.
- If no wolf is hurt for 200 rounds, the pack with the most total energy wins.

Orders are typed in one line, `x-y:<order>x-y`:

```text
3-2:@4-2 1-1:*1-2 3-3:<4-4 2-2:pacify
 move     attack   eat      pacify (omega)
```

## Play

```bash
python -m pip install blessed
python engine_gr_19.py                              # AI vs AI on maps/classic.ano
python engine_gr_19.py maps/vertical.ano human AI   # you against the AI
```

Player types: `human`, `AI`, `remote` (games between two programs over the network, used for the class
tournament, through `distancemodule.py` provided by the course).

## Code

| File | Role |
|---|---|
| `engine_gr_19.py` | rules, map parsing, round loop, terminal board drawn with `blessed` (emoji food, health bars) |
| `ai_engine_gr_19.py` | the AI: sends the pack at the enemy alpha, and sends its own alpha to the best food nearby when its energy drops below 80 |
| `ai_dumb_gr_19.py` | a random baseline used to test the AI |
| `maps/*.ano` | board size, starting positions, food |

The code is kept as it was submitted (French comments, the course's naming), apart from a command-line
entry point added in 2026 so it can be run without the tournament server.

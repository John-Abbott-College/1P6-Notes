# Truth Tables

[spreadsheet for all of them](https://docs.google.com/spreadsheets/d/1C9Gb50xokCsSB5zB3HFcyl2wcMCYBksShtluBjjlf9A/edit?usp=sharing)

| `x`   | `y`   | `x and y` |
| ----- | ----- | --------- |
| **T** | **T** | **T**     |
| T     | F     | F         |
| F     | T     | F         |
| F     | F     | F         |

| `x`   | `y`   | `x or y` |
| ----- | ----- | -------- |
| **T** | **T** | **T**    |
| **T** | F     | **T**    |
| F     | **T** | **T**    |
| F     | F     | F        |

| `x`   | `not x` |
| ----- | ------- |
| **T** | F       |
| F     | **T**   |

If you have three propositions in your logic (`P`, `Q` and `R`), you should follow the pattern shown below: 

| P    | Q    | R    |
| ---- | ---- | ---- |
| F    | F    | F    |
| F    | F    | T    |
| F    | T    | F    |
| F    | T    | T    |
| T    | F    | F    |
| T    | F    | T    |
| T    | T    | F    |
| T    | T    | T    |

| P    | Q    | P `implies` Q |
| ---- | ---- | ------------- |
| T    | T    | T             |
| T    | F    | F             |
| F    | T    | T             |
| F    | F    | T             |

| P    | Q    | P `is equivalent to` Q |
| ---- | ---- | ---------------------- |
| T    | T    | T                      |
| T    | F    | F                      |
| F    | T    | F                      |
| F    | F    | T                      |
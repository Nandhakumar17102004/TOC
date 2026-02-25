## Regular Expression to NFA Transition Table Generator

This program converts a given regular expression into a **Non-Deterministic Finite Automaton (NFA)** transition table.

It is designed for educational use in **Compiler Design / Formal Languages / Automata Theory** to demonstrate how regular expressions are translated into state machines using ε-transitions.

---

## What the Code Does

1. Accepts a regular expression as input.
2. Parses the expression character by character.
3. Builds an NFA transition table using:
   - symbol transitions (`a`, `b`)
   - epsilon transitions (`e`)
   - union operator (`|`)
   - Kleene star (`*`)
   - grouping using parentheses `()`
4. Prints:
   - the transition function in readable form
   - the internal transition table
   - the final accepting state

---

## Supported Regular Expression Symbols

- `a`, `b` → input symbols  
- `e` → epsilon transition  
- `|` → union operation  
- `*` → Kleene closure  
- `( )` → grouping  

---

## How the Algorithm Works

### 1. Transition Table Creation
### Transition Table Structure

The table stores transitions for:

| Column | Meaning |
|--------|---------|
| 0 | transition on `a` |
| 1 | transition on `b` |
| 2 | epsilon transition |

Each row represents a state.

---

### 2. Sequential Parsing

The program scans the regular expression from left to right and constructs the NFA step-by-step.

For example:

- For symbol `a` → create transition from state `j` to `j+1`
- For symbol `b` → create similar transition
- For epsilon `e` → create ε-transition

---

### 3. Union Handling (`a|b` or `b|a`)

When a union operator is detected:

- Create a branching ε-transition  
- Build paths for both operands  
- Merge them using another ε-transition  

This simulates the NFA structure used in Thompson’s construction.

---

### 4. Kleene Star Handling (`a*` or `b*`)

For closure:

- Add an ε-transition to the loop entry  
- Add an ε-transition back to the previous state  
- Allow skipping the loop entirely  

This creates the repeating pattern required for Kleene star.

---

### 5. Parentheses Handling

Parentheses allow grouped expressions.

The program stores the base pointer (`bp`) when `(` appears and uses it to create looping or merging transitions when `)` is encountered.

---

### 6. Output Generation

After processing the expression, the program prints:

- All transitions in the format  
  `q[i,a] → q[j]`

- ε-transitions in the format  
  `q[i,e] → q[j]`

- The final accepting state

```python
transition_table = [[0]*3 for _ in range(20)]

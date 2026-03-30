# 📁 Generate Parentheses

> A Python function that generates all valid combinations of balanced parentheses for a given number of pairs using a queue based BFS approach.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Learning](https://img.shields.io/badge/Learning-Journey-orange)
![DSA](https://img.shields.io/badge/Topic-Algorithms-red?logo=python&logoColor=white)

---

## 📌 About

This project generates every valid combination of `n` pairs of balanced parentheses, a classic problem used in technical interviews. Rather than using recursion, the solution uses a **queue-based BFS (Breadth-First Search)** approach, building each combination character by character and only appending parentheses when the rules for valid combinations allow it. Built to understand BFS, state tracking with tuples, and constraint based generation.

---

## 🧠 What I Learned

- **Queue based BFS for combinatorics** — Using a list as a queue where each element is a state tuple `(current_string, opens_used, closes_used)`, processing states level by level until all valid combinations are found, a different approach from the recursive backtracking solution most developers reach for first
- **State tracking with tuples** — Packing the current string and two counters into a single tuple that gets unpacked cleanly with `current, opens_used, closes_used = queue.pop(0)`, making the state self-contained and easy to reason about
- **Constraint based generation** — Only adding an open parenthesis when `opens_used < pairs`, and only adding a close when `closes_used < opens_used` — these two rules together guarantee every generated combination is valid without any post-filtering
- **`queue.pop(0)` for FIFO ordering** — Using `pop(0)` instead of `pop()` ensures the queue processes states in insertion order (FIFO), which is the defining behavior of BFS vs DFS
- **Input validation before algorithm logic** — Checking both type and value before entering the queue loop, keeping the core algorithm clean and free of defensive branches

---

## 🛠️ Technologies Used

| Tool / Library | Purpose |
|---|---|
| Python 3.x | Core language |

---

## 💡 How It Works

Each state in the queue tracks the string built so far and how many opens and closes have been used. At each step, the function tries to add `(` or `)` only if the constraints allow it. When a string reaches length `2 * pairs` it's a valid combination and gets added to the result.

```
pairs = 2 — target length: 4

Start:  ('', 0, 0)
Add (:  ('(', 1, 0)
  Add (:  ('((', 2, 0)
    Add ):   ('(()', 2, 1)
      Add ):   ('(())' ✅)
  Add ):  ('()', 1, 1)
    Add (:   ('()(', 2, 1)
      Add ):   ('()()' ✅)
```

**Example output:**
```python
gen_parentheses(2)  # ['(())', '()()']
gen_parentheses(3)  # ['((()))', '(()())', '(())()', '()(())', '()()()']
```

---

## 🚀 Future Improvements

- [ ] Implement the recursive backtracking version and compare it to this BFS approach
- [ ] Add a `collections.deque` for more efficient `popleft()` instead of `list.pop(0)`
- [ ] Extend to generate all valid combinations of multiple bracket types `()`, `[]`, `{}`
- [ ] Write unit tests with `pytest` to validate output length matches the Catalan number formula

---

## 📂 Project Structure

```
generate-parentheses/
│
├── BreadthFirstSearchAlgorithm.py    # gen_parentheses function with example usage
└── README.md
```

---

*Part of my Python learning journey 🐍 — exploring BFS, state based generation, and classic interview problems*

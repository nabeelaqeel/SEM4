# Part 1


| Aspect             | QuadTree  | Grid     | Spatial Hash | Probabilistic |
| ------------------ | --------- | -------- | ------------ | ------------- |
| **Speed**          | Variable  | Moderate | Fast*        | Fastest       |
| **Memory**         | Low       | Moderate | High         | Minimal       |
| **Accuracy**       | High      | High     | Good         | Variable      |
| **Real-time**      | No        | No       | Yes          | Yes           |
| **Deterministic**  | Yes       | Yes      | Yes          | No            |
| **Implementation** | Complex   | Simple   | Moderate     | Simple        |
| **Scalability**    | Good      | Good     | Moderate     | Excellent     |
| **Adaptability**   | Excellent | Poor     | Good         | Good          |
# Part 5

In the classic **0/1 Knapsack Problem**, you’re given:

- A list of items.
    
- Each item has:
    
    - A **weight** (something limited — like space or power)
        
    - A **value** (something you want to maximize — like usefulness)
        
- A **weight limit** (you can’t carry more than this)
    
- The goal is to **maximize total value** of selected items **without exceeding the weight limit**.
# Part 6

### ❌ Why **Knapsack** Doesn’t Work Here

| Knapsack Problem                                     | Docking Problem                                    |
| ---------------------------------------------------- | -------------------------------------------------- |
| Items have value (profit) and weight                 | Ships have optional priority and docking time      |
| Goal: Maximize **total value** within a weight limit | Goal: Maximize **number of non-overlapping ships** |
| Dynamic Programming considers combinations           | Greedy needs to avoid overlapping time intervals   |
| Doesn’t care about overlapping intervals             | Must avoid time conflicts (overlaps)               |

### ✅ Code Breakdown

python

CopyEdit

`# Step 3: Greedy selection process tracking selected = [] selection_process = [] current_end_time = 0`

#### 🔹 What it does:

- `selected`: a list to store the **rows** (ship records) that are approved.
    
- `selection_process`: a list to keep track of just the **ship IDs** that got approved (for easy display or debug).
    
- `current_end_time`: keeps track of the **end time of the last approved ship** (starts at 0).
    

---

python

CopyEdit

`for _, row in df_sorted.iterrows():`

#### 🔹 What it does:

- Loops through each row in the sorted DataFrame.
    
- `row` contains the info about one ship (like start and end time).
    
- `_` ignores the row index.
    

---

python

CopyEdit

    `ship_id = row['Ship']`

#### 🔹 What it does:

- Extracts the ship's ID (like 'A', 'B', etc.) from the current row.
    

---

python

CopyEdit

    `if row['Start'] >= current_end_time:`

#### 🔹 What it does:

- Checks if the **current ship can dock** without overlapping.
    
- A ship can dock only if its **start time** is **after or at** the end time of the last ship.
    

---

python

CopyEdit

        `selected.append(row)`

#### 🔹 What it does:

- Adds this ship’s entire row (its data) to the list of approved ships.
    

---

python

CopyEdit

        `selection_process.append(ship_id)`

#### 🔹 What it does:

- Stores just the ship's ID for display/tracking.
    

---

python

CopyEdit

        `current_end_time = row['End']`

#### 🔹 What it does:

- Updates `current_end_time` to reflect the **end time of the ship just approved** — used to check for overlaps with the next ships.
    

---

python

CopyEdit

`df_selected = pd.DataFrame(selected)`

#### 🔹 What it does:

- Converts the list of selected rows back into a DataFrame called `df_selected`.
    
- This makes it easier to display or work with the approved docking schedule.
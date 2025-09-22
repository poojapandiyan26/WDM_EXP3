### EX3 Implementation of GSP Algorithm In Python
### DATE: 22.09.25
### DEVELOPED BY: P.Pooja Sri
### REGISTER NO: 212224230197
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```python
from collections import defaultdict
from itertools import combinations

def generate_candidates(dataset, k, min_support):
    candidates = defaultdict(int)
    for seq in dataset:
        flat_seq = [item for itemset in seq for item in itemset]
        for comb in combinations(flat_seq, k):
            candidates[comb] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}

def gsp(dataset, min_support):
    fp = defaultdict(int)
    k = 1
    while True:
        candidates = generate_candidates(dataset, k, min_support)
        if not candidates:
            break
        fp.update(candidates)
        k += 1
    return fp

dataset = [
    [["a","b","c"], ["b","e"], ["c","f","g"], ["a","b","e"]],   
    [["a","d"], ["b","c"], ["c"], ["f","g"], ["c","h"]],       
    [["b","c"], ["a","d"], ["e","b","f"], ["c","d","f","g","h"]], 
    [["c"], ["e","c"], ["e","h"]]                             
]

dataset2 = [
    [["b","d"], ["c","b"], ["a","c"]],  
    [["b","f"], ["c","e"], ["b"], ["f","g"]],       
    [["a","h"], ["b","f"], ["a","b","f"]],
    [["b","e"], ["c","e"], ["d"]],   
    [["a"], ["b","d"], ["b","c","b"], ["a","d","e"]]
]

min_support = 3

results = gsp(dataset, min_support)

print("Frequent Sequential Patterns for Dataset 1:")
if results:
    for pattern, support in results.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")
    


results = gsp(dataset2, min_support)

print("\nFrequent Sequential Patterns for Dataset 2:")
if results:
    for pattern, support in results.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")
```
### Output:
<img width="1356" height="415" alt="image" src="https://github.com/user-attachments/assets/8d6362ad-7804-48bb-bbb2-a121033753da" />

### Visualization:
```python
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')
visualize_patterns_line(bottom_wear_result, 'Bottom Wear')
visualize_patterns_line(party_wear_result, 'Party Wear')
```
### Output:
<img width="1217" height="411" alt="image" src="https://github.com/user-attachments/assets/33651cd0-5e61-498a-9cd7-a1887db14f6b" />


### Result:
The GSP algorithm in python has been successfully implemented.

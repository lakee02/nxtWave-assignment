### Video Link : 
-https://drive.google.com/file/d/1Wj2lu9lxpfhnszfMON53oZFlA8PRFhDl/view?usp=sharing

### Slide 1: Introduction
- The problem statement requires us to write a function that takes the total score and the test cases data as input and distributes the test case scores appropriately based on the priority order of test case types.
- The test case types are `Edge case`, `Normal`, `Trivial`, and `Non-hidden`.
- The score distribution should follow the priority order of test case types.

### Slide 2: Approach
- Our approach is to first calculate the number of test cases for each type.
- Then, we calculate the score for each type based on the priority order and the total score.
- Finally, we update the scores for each test case in the input data.

### Slide 3: Key Components
- `calculate_type_count`: A function that calculates the number of test cases for each type.
- `calculate_type_score`: A function that calculates the score for each type based on the priority order and the total score.
- `update_test_case_scores`: The main function that updates the scores for each test case in the input data.

### Slide 4: Code Snippet
```python
def calculate_type_count(test_cases):
    type_count = {
        "Edge case": 0,
        "Normal": 0,
        "Trivial": 0,
        "Non-hidden": 0
    }
    for test_case in test_cases:
        type_count[test_case["type"]] += 1
    return type_count

def calculate_type_score(total_score, type_count):
    min_total_score = type_count["Non-hidden"] + (type_count["Edge case"] + type_count["Normal"] + type_count["Trivial"]) * 2
    if total_score < min_total_score:
        raise ValueError(f"The total score ({total_score}) is not sufficient to distribute among the test cases. The minimum required total score is {min_total_score}.")
    edge_case_score = (total_score - type_count["Non-hidden"]) // (type_count["Edge case"] + type_count["Normal"] + type_count["Trivial"])
    normal_score = edge_case_score
    trivial_score = edge_case_score
    non_hidden_score = 1
    return {
        "Edge case": edge_case_score,
        "Normal": normal_score,
        "Trivial": trivial_score,
        "Non-hidden": non_hidden_score
    }
def update_test_case_scores(total_score, test_cases):
    type_count = calculate_type_count(test_cases)
    type_score = calculate_type_score(total_score, type_count)
    for test_case in test_cases:
        test_case["score"] = type_score[test_case["type"]]
    return test_cases
```

### Slide 5: MCQs to assess understanding of the solution
1. What is the priority order of test case types?
    a. Edge case > Normal > Trivial > Non-hidden
    b. Normal > Edge case > Trivial > Non-hidden
    c. Trivial > Normal > Edge case > Non-hidden
    d. Non-hidden > Trivial > Normal > Edge case

2. What is the score of non-hidden test cases?
    a. 0
    b. 1
    c. 2
    d. 3

3. How is the score for edge case, normal, and trivial test cases calculated?
    a. By dividing the total score by the number of test cases.
    b. By subtracting the number of non-hidden test cases from the total score and dividing by the number of edge case, normal, and trivial test cases.
    c. By adding the number of non-hidden test cases to the total score and dividing by the number of edge case, normal, and trivial test cases.
    d. By multiplying the total score by the number of edge case, normal, and trivial test cases.

### Slide 6: Coding Questions
1. Write a function `calculate_type_count` that takes a list of test cases as input and returns a dictionary representing the number of test cases for each type.

2. Write a function `calculate_type_score` that takes the total score and a dictionary representing the number of test cases for each type as input and returns a dictionary representing the score for each type.

3. Write a function `update_test_case_scores` that takes the total score and a list of test cases as input and returns a list of updated test cases with their scores.

### Slide 7: Solution to Problem Statement

```python
total_score = 30

test_cases = {
    "non_hidden_testcases": [
        {
            "input": "Apple\nBanana",
            "is_hidden": False,
            "score": 1,
            "output": "Banana\n---\nApple",
            "testcase_type": "NON_HIDDEN",
            "t_id": 1
        },
        {
            "input": "Car\nBike",
            "is_hidden": False,
            "score": 1,
            "output": "Bike\n---\nCar",
            "testcase_type": "NON_HIDDEN",
            "t_id": 2
        }
    ],
    "trivial_testcases": [
        {
            "input": "Sam\nSam",
            "is_hidden": True,
            "score": 2,
            "output": "Sam\n---\nSam",
            "testcase_type": "TRIVIAL",
            "t_id": 3
        }
    ],
    "normal_testcases": [
        {
            "input": "Television\nSatellite",
            "is_hidden": True,
            "score": 3,
            "output": "Satellite\n---\nTelevision",
            "testcase_type": "NORMAL",
            "t_id": 4
        },
        {
            "input": "Television\nSatellite",
            "is_hidden": True,
            "score": 3,
            "output": "Satellite\n---\nTelevision",
            "testcase_type": "NORMAL",
            "t_id": 5
        },
        {
            "input": "Television\nSatellite",
            "is_hidden": True,
            "score": 3,
            "output": "Satellite\n---\nTelevision",
            "testcase_type": "NORMAL",
            "t_id": 6
        }
    ],
    "edge_case_testcases": [
        {
            "input": "Work\nHome",
            "is_hidden": True,
            "score": 3,
            "output": "Home\n---\nWork",
            "testcase_type": "EDGE_CASE",
            "t_id": 7
        }
    ],
}

updated_test_cases = update_test_case_scores(total_score, test_cases)
```
# Pandas5

1 Problem 1 : Department Highest Salary (https://leetcode.com/problems/department-highest-salary/ )

rite a solution to find employees who have the highest salary in each of the departments.

Return the result table in any order.

The result format is in the following example.

 
------------------------------------------------

import pandas as pd

def department_highest_salary(employee: pd.DataFrame, department: pd.DataFrame) -> pd.DataFrame:
    merged = employee.merge(department, left_on='departmentId', right_on='id')
    max_salaries = merged.groupby('name_y')['salary'].transform('max')
    result = merged[merged['salary'] == max_salaries][['name_y', 'name_x', 'salary']]
    result.columns = ['Department', 'Employee', 'Salary']
    return result

------------------------------------------------



2 Problem 2 : Rank Scores ( https://leetcode.com/problems/rank-scores/ )

Write a solution to find the rank of the scores. The ranking should be calculated according to the following rules:

The scores should be ranked from the highest to the lowest.
If there is a tie between two scores, both should have the same ranking.
After a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no holes between ranks.
Return the result table ordered by score in descending order.

The result format is in the following example.

 
------------------------------------------------
import pandas as pd

def rank_scores(scores: pd.DataFrame) -> pd.DataFrame:
    scores['rank'] = scores['score'].rank(method='dense', ascending=False).astype(int)
    return scores[['score', 'rank']].sort_values('score', ascending=False)


------------------------------------------------



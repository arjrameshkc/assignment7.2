# assignment7.2
a)
emp = LOAD 'employee_details.txt' USING PigStorage(',') AS (emp_id:int, emp_name:chararray, emp_salary:int,emp_rating:int);
dump emp;
sorted_emp_rating = ORDER emp by emp_rating asc;
dump sorted_emp_rating;
five_emp = limit sorted_emp_rating 5;
dump five_emp;

b)filtered_emp_id =  FOREACH emp GENERATE emp_id,emp_name,emp_salary,(
                  CASE 
                  WHEN emp_id % 2 == 0 THEN 'EVEN'
                  WHEN emp_id % 2 == 1 THEN 'ODD'
                  END
                  ) AS F2;
filter_odd = FILTER filtered_emp_id by F2 matches 'ODD';
dump filter_odd;
sorted_emp_sal = ORDER filter_odd by emp_salary desc;

three_emp = limit sorted_emp_sal 3;
dump three_emp;

C)emp_expenses = LOAD 'employee_expenses.txt' AS (emp_id:int, expenses:int);
  max_sal  = ORDER emp_expenses by expenses desc;
  max_one = limit max_sal 1;
  high  = JOIN emp by emp_id, max_one by emp_id; 
  dump high;

D)left_join  = JOIN emp by emp_id LEFT, emp_expenses by emp_id;
  dump left_join;

e) right_join = JOIN emp by emp_id RIGHT, emp_expenses by emp_id;
  dump = right_join;

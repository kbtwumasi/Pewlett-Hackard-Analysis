# **PEWLETT-HACKARD-ANALYSIS**.


## **Overview Of The Analysis**
Pewlett Hackard, a fictitious company, inorder to stay a future proof company, wants to be prepared for the impending “silver tsunami” as many of its current employees are retiring soon. They are counting on this project to provide management with information on who is retiring soon per title and who is eligible to participate in the mentorship program available at the company. 
The purpose of this project is to create databases and query the data to provide the above requested information to the management of the company to be better prepared the number of current employees reaching retirement age. 

## **Results**

![Retiring employees grouped by title] (/Data/retiring_employees_by_title.png)

After the analysis of the employee information, the following conclusions were reached; 

- Based on employees who were born between January 1, 1952 and December 31, 1955, 72,458 current employees will be affected during the ’silver tsunami’
- Out of the total reaching retirement age, majority are senior engineers with total employees of 25,916, followed by Senior staff with 24,926, 9,285 Engineers, 7,636 staffs, 3,603 technique leaders, 1,090 assistant engineers and 2 managers.

![Employees Eligible for Mentorship](/Data/eligible_mentorship.png)

- a total of 1,549 current employees with birth dates between Jan 1, 1965 and December 31,1965 are eligible for the mentorship program. However, that is far less than employees retirng soon. 
- Out of the total current employees eligible for the mentorship program, 417 are senior staff, 401 are engineers, 307 are staff, 284 are senior engineers, 77 are assistant engineers and 63 technical leaders. No current employee is eligible for mentorship program for manager.

## **Summary**

As the silver tsunami begin to impact Pewlett Hackard, management should be aware that in order to maintain the current employment levels, 72,458 positions needs to be filled. Management can focus on which roles that will be impacted the most, that is, senior engineers and senior staff to ensure the company stays future proof.

As to weather the company has enough current employees eligibe for the mentorship programs to fill these roles, only a fraction of the employees are eligible. In short, the 1,549 current employees eligible for the program is just a fraction of the total number of employees who will be affected during the silver tsunami and need to be replaced. Below is a breakdown of the number of employees eligible by titles for the mentorship program.

![Mentorship eligiblity group by title](/Data/mentorship_eligibility_by_title.png)

Since the number of current employees eligible for the mentorship program, management can adjust the birth date rate for more employees to be eligible. This can be achieved by the query quoted below.
 
```
SELECT DISTINCT ON (e.emp_no) e.emp_no,
	e.first_name,
	e.last_name,
	e.birth_date,
	de.from_date,
	de.to_date,
	te.title
--INTO revised_mentorship_eligibility
FROM employees AS e
INNER JOIN dept_emp AS de
ON (e.emp_no = de.emp_no)
INNER JOIN titles AS te
ON (e.emp_no = te.emp_no)
WHERE (de.to_date = '9999-01-01')
	AND (e.birth_date BETWEEN '1960-01-01' AND '1965-12-31')
ORDER BY emp_no;
```
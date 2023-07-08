a) What are the appropriate primary keys?
- branch: branch_name
- customer: c_name
- loan: loan_number
- borrower: (c_name, loan_number) (composite primary key)
- account: a_no
- depositor: (c_name, a_no) (composite primary key)

b) Given your choice of primary keys, identify appropriate foreign keys.
- loan (branch_name) references branch (branch_name)
- borrower (c_name) references customer (c_name)
- borrower (loan_number) references loan (loan_number)
- account (branch_name) references branch (branch_name)
- depositor (c_name) references customer (c_name)
- depositor (a_no) references account (a_no)

c) Write the following query in SQL, using the bank schema.

i. Find the name of all branches located in "Dhaka":
SELECT branch_name
FROM branch
WHERE branch_city = 'Dhaka';

ii. Find the names of all borrowers who have a loan in branch "Mirpur":
SELECT DISTINCT c_name
FROM borrower
WHERE loan_number IN (
    SELECT loan_number
    FROM loan
    WHERE branch_name = 'Mirpur'
);

iii. Find all loan numbers with a loan value greater than BDT100,000:
SELECT loan_number
FROM loan
WHERE amount > 100000;

iv. Find the names of all depositors who have an account with a value greater than BDT60,000:
SELECT DISTINCT c_name
FROM depositor
WHERE a_no IN (
    SELECT a_no
    FROM account
    WHERE balance > 60000
);

v. Find the names of all depositors who have an account with a value greater than BDT60,000 at the "Motejheel" branch:
SELECT DISTINCT d.c_name
FROM depositor d
JOIN account a ON d.a_no = a.a_no
WHERE a.balance > 60000 AND a.branch_name = 'Motejheel';

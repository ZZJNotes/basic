# 牛客网SQL练习

##0428

###01

```mysql
# 题目描述
# 查找所有员工的last_name和first_name以及对应部门编号dept_no，也包括暂时没有分配具体部门的员工
CREATE TABLE `dept_emp` (
    `emp_no` int(11) NOT NULL,
    `dept_no` char(4) NOT NULL,
    `from_date` date NOT NULL,
    `to_date` date NOT NULL,
    PRIMARY KEY (`emp_no`,`dept_no`)
);

CREATE TABLE `employees` (
    `emp_no` int(11) NOT NULL,
    `birth_date` date NOT NULL,
    `first_name` varchar(14) NOT NULL,
    `last_name` varchar(16) NOT NULL,
    `gender` char(1) NOT NULL,
    `hire_date` date NOT NULL,
    PRIMARY KEY (`emp_no`)
);
```

第一眼看到这个题目的时候，觉得这个题目十分的简单，应该放在上一道题目的前面才对，然后就写出了下面的代码

```mysql
select last_name, first_name, dept_no
from employees as a
join dept_emp as b
on a.emp_no = b.emp_no;
```

天真的以为之间连接两个表就可以了，然后结果就是无法通过

看了题解才知道，该题需要使用左联结

- 内联结，两边表同时有对应的数据，即任何一边缺失数据就不显示。
- 左联结，读取左边数据表的全部数据，即便右边表无对应数。即右表d中dept_no即使为NULL，也会读取左表e中的全部emp。

~~~mysql
select last_name, first_name, dept_no
from employees as a
left join dept_emp as b
on a.emp_no = b.emp_no;
~~~
###02

```mysql
# 题目描述
# 查找薪水涨幅超过15次的员工号emp_no以及其对应的涨幅次数t
CREATE TABLE `salaries` (
    `emp_no` int(11) NOT NULL,
    `salary` int(11) NOT NULL,
    `from_date` date NOT NULL,
    `to_date` date NOT NULL,
    PRIMARY KEY (`emp_no`,`from_date`)
);
```

没有搞明白这道题是怎么求出来的

~~~mysql
select emp_no, count(*) as t
from salaries
group by emp_no
having t > 15;
~~~







```mysql
#1
select * from employees
order by hire_date desc
limit 1 offset 0;

#2
select * from employees
order by hire_date desc
limit 1 offset 2;
#3
select salaries.*, dept_manager.dept_no
from salaries 
join dept_manager 
using(emp_no)
where salaries.to_date = '9999-01-01'
    and dept_manager.to_date = '9999-01-01';

#4
select last_name, first_name, dept_no
from employees as a
join dept_emp as b
using(emp_no)
where b.dept_no is not null;
#5
select last_name, first_name, dept_no
from employees as a
left join dept_emp as b
on a.emp_no = b.emp_no;
#6
select emp_no, salary
from salaries as s
join employees as e
using(emp_no)
where s.from_date = e.hire_date
order by emp_no desc;
#7
select emp_no, count(*) as t
from salaries
group by emp_no
having t > 15;
#8
select distinct salary
from salaries
where to_date = '9999-01-01'
order by salary desc;
#9
select dept_no, emp_no, salary
from dept_manager
join salaries
using(emp_no)
where salaries.to_date = '9999-01-01'
    and salaries.to_date = dept_manager.to_date;
#10
select emp_no
from employees
where emp_no not in (
    select emp_no
    from dept_manager
);
```


# Employee Management system

*https://emp-details-systems.in

## Features

*complete database of company_employee_details

### Features 1: Deatils_of_Employee_department

```sql


create table departments
( 
     d_id number ,                                       --primary key
     department_name varchar2(20) not null,
     manager_id varchar2(20) ,
     department_location varchar2(20),
     constraint dept_pk primary key(d_id),
     constraint manager_id_uq unique (manager_id,department_name) 
);
insert into departments(d_id,department_name,manager_id,department_location) values (1,'pchh_it',1,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (2,'pchh_marketing',2,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (3,'pchh_salesforce',3,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (4,'pchh_product',1,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (5,'pchh_testing',4,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (6,'pchh_services',1,'chennai');
insert into departments(d_id,department_name,department_location) values (7,'pchh_networking','null');

select * from departments;
drop table departments;


| department_id | department_name | manager_id | department_location |
|:-------------:|-----------------|------------|---------------------|
|       1       | pchh_it         |      1     |       chennai       |
|       2       | pchh_marketing  |      2     |       chennai       |
|       3       | pchh_salesforce |      3     |       chennai       |
|       4       | pchh_product    |      1     |       chennai       |
|       5       | pchh_testing    |      4     |       chennai       |
|       6       | pchh_service    |      1     |       chennai       |
|       7       | pchh_networking |      -     |          -          |

```

### Features 1: List_Deatils_of_Employees

```sql

create table employee_details
(
    e_id number,	          --PRIMARY KEY 
    department_id number,	  --FOREIGN KEY
    employee_name varchar2(55),
     gender varchar2(20) not null,
    birth_date date not null,
    joining_date date,
    pan_card varchar2(20) NOT NULL,
    adhar_num  number,                  --UNIQUE KEY
    driving_license_num varchar2(20), 	--UNIQUE KEY
    employee_mobnum number,             --UNIQUE KEY
    constraint emp_dept_pk primary key(e_id),
    constraint emp_adhar unique(adhar_num),
    constraint emp_dl_uq unique(driving_license_num),
    constraint emp_mobno_uq unique(employee_mobnum),
    constraint emp_fk foreign key (department_id) references departments(d_id),
    constraint emp_gender check(gender in('male','female','others')),
    constraint proof_chk check (adhar_num is not null or driving_license_num is not null) 
);
create sequence employee_adds start with 14 increment by 1;


insert into employee_details values(1,2,'anbuselvam','male',to_date('03-03-1997','dd-mm-yyyy'),to_date('03-01-2019','dd-mm-yyyy'),'234567891','','WA25728567','9585758494');
insert into employee_details values(2,4,'vinayak','male','22-OCT-98','03-NOV-19','142648797 ','453782827378','1347537WA8','9835353664');
insert into employee_details values(3,1,'vijaykumar','male','12-APR-1996','03-NOV-2019','124367898','242627227388','12145EA5368','9242525643');
insert into employee_details values(4,1,'ramya','female','11-MAR-1998','03-MAR-2019','145678930','353767388992','','8356342526');
insert into employee_details values(5,1,'velan','male','16-JAN-1998','04-NOV-2019','156372890','345362728299','574838393PS','8134556266');
insert into employee_details values(6,3,'alex','male','12-NOV-1997','04-NOV-2019','123456781','252627288899','46373738DW','9562727278');




drop table employee_details;
select * from employee_details;


| e_id |department_id|employee_name| gender| birth_date |joining_date  | pan_card  | adhar_num    | driving_licence_num |employee_mobnum 
|------|----------|---------------|--------|------------|--------------|-----------|--------------|---------------------|----------
| 1    | 1        | anbuselvam    | male   | 30/10/1997 | 03/11/2019   | 234567891 |              | WA25728567          | 9585758494      |
| 2    | 2        | vinayak       | male   | 22/11/1998 | 03/11/2019   | 142648797 | 453782827378 | 1347537WA8          | 9835353664      |
| 3    | 3        | vijaykumar    | male   | 12/05/1996 | 03/11/2019   | 124367898 | 242627227388 | 12145EA5368         | 9242525643      |
| 4    | 4        | ramya         | female | 11/03/1998 | 03/11/2019   | 145678930 | 353767388992 |                     | 8356342526      |
| 5    | 1        | velan         | male   | 16/01/1998 | 04/11/2019   | 156372890 | 345362728299 | 574838393PS         | 8134556266      |
| 6    | 5        | alax          | male   | 12/11/1997 | 04/11/2019   | 163739990 | 252627288899 | 46373738DW          | 9562727278      

```

### Feautures:to find out Employee_Address locations

```sql

CREATE TABLE STATES(
	
		STATES_ID number not null ,               --PRIMARY KEY
		STATE_NAME varchar2(40),
		CONSTRAINT STATE_ID_PK PRIMARY KEY(STATES_ID),
		CONSTRAINT STATE_NAME_UK UNIQUE(STATE_NAME));

INSERT INTO STATES (STATES_ID,STATE_NAME) VALUES (1,'TAMILNADU');
INSERT INTO STATES (STATES_ID,STATE_NAME) VALUES (2,'KERALA');
INSERT INTO STATES (STATES_ID,STATE_NAME) VALUES (3,'ANDRA');
INSERT INTO STATES (STATES_ID,STATE_NAME) VALUES (4,'BIHAR');
INSERT INTO STATES (STATES_ID,STATE_NAME) VALUES (5,'NEPAL');

select * from states;

| states_id | states_name |
|-----------|-------------|
| 1         | tamilnadu   |
| 2         | kerala      |
| 3         | andra       |
| 4         | bihar       |
| 5         | nepal       |
|           |             |




create table employee_addresses(
		address_id number,                       --PRIMARY KEY
		emp_id number not null ,                 --FOREIGN KEY
		address_type varchar2(25),
		address_line1 varchar2(25) not null,
		address_line2 varchar2(25),
		city_name varchar2(55) not null,
		pin_code number not null,
		state_id number not null,
		constraint addr_type_ck check (address_type in ('permanant','temporary','others')),
		constraint states_chk foreign key(state_id) references states(states_id), 
	constraint addr_id_pk primary key(address_id),
        constraint emp_k_fk foreign key(emp_id) references employee_details(e_id) 

);

drop table employee_addresses;
insert into employee_addresses(address_id,emp_id,address_type,address_line1,address_line2,city_name,pin_code,state_id)
	values(1,1,'permanant','#12,kn street','null','chennai',600012,1);
insert into employee_addresses(address_id,emp_id,address_type,address_line1,address_line2,city_name,pin_code,state_id)
	values(2,1,'temporary','#13,mm street','null','chennai',600042,1);
insert into employee_addresses(address_id,emp_id,address_type,address_line1,address_line2,city_name,pin_code,state_id)
	values(3,2,'permanant','#12,raj street','null','cochin',200022,2);
insert into employee_addresses(address_id,emp_id,address_type,address_line1,address_line2,city_name,pin_code,state_id)
	values(4,3,'temporary','#22,kwj street','null','chennai',600012,1);
insert into employee_addresses(address_id,emp_id,address_type,address_line1,address_line2,city_name,pin_code,state_id)
	values(5,4,'permanant','#15,rn street','null','kollam',200012,2);
insert into employee_addresses(address_id,emp_id,address_type,address_line1,address_line2,city_name,pin_code,state_id)
	values(6,5,'temporary','#123,kn street','null','chennai',600112,1);
insert into employee_addresses(address_id,emp_id,address_type,address_line1,address_line2,city_name,pin_code,state_id)
	values(7,6,'others','#13,nn street','null','kadapa',100012,3);
  
	
	
    select * from employee_details;
    select * from employee_addresses;
    
| address_id | emp_id | address_type |  address_line1 | address_line2 | city_name | pin_code | state_id |
|:----------:|:------:|:------------:|:--------------:|:-------------:|:---------:|:--------:|:--------:|
|      1     |    1   |   permanant  |  #12,kn street |      null     |  chennai  |  600012  |     1    |
|      2     |    1   |   temporary  |  #13,mm street |      null     |  chennai  |  600042  |     1    |
|      3     |    2   |   permanant  | #12,raj street |      null     |   cochin  |  200022  |     2    |
|      4     |    3   |   temporary  | #22,kwj street |      null     |  chennai  |  600012  |     1    |
|      5     |    4   |   permanant  |  #15,rn street |      null     |   kollam  |  200012  |     1    |
|      6     |    5   |   temporary  | #123,kn street |      null     |  chennai  |  600112  |     1    |
|      7     |    6   |    others    |  #13,nn street |      null     |   kadapa  |  100012  |     3    |
   
   ```
   ### Features: salary table
    
   ```Sql
   
   CREATE TABLE person_salary_details
(
  SALARY_ID number(5) primary key not null,
  e_id   NUMBER ,
     --CONSTRAINT in_emp REFERENCES hr.employees(employee_id)_ID number(5) references employee_details(e_id),
  SALARY number(8),
  MONTH varchar2(9),
  YEAR number(4),
  constraint e_id_fk foreign key (e_id) references employee_details(e_id)
);
    CREATE OR REPLACE FUNCTION calculate_tax(e_eId NUMBER)
   RETURN NUMBER
   IS tax NUMBER(10,2);
 
BEGIN 
   tax := 0;
   
      SELECT (sum(salary)*10)/100 into tax FROM person_salary_details WHERE e_id = e_eId;
            
      RETURN tax;
      
END calculate_tax;
    
    
 ```
 ### feautures: logintable
 
 create table Manager(
manager_id number not null,
manager_name varchar2(44) unique,
email varchar2(55) unique,
dob date,
mob_num number,
pass_word varchar2(55),
gender varchar2(22)
--constraint m_fk manager_id references employee_details(manager_id)

);
create SEQUENCE Update_sequence start with 1 INCREMENT by 1;

```
    
 ```
### feautures: Queries

```sql
    
--Display manager_name, manager_id, conut(department) under each manager
  
select e.employee_name ,d.manager_id,count(department_name) as department_count 
from departments d 
join employee_details e 
on d.manager_id=e.e_id                                             --(find employee ->manager_id,(?) department)
group by d.manager_id,e.employee_name;

| EMPLOYEE_NAME | MANAGER_ID | DEPARTMENT_COUNT |
|---------------|------------|------------------|
| anbuselvam    | 1          | 3                |
| vinayak       | 2          | 1                |
| vijaykumar    | 3          | 1                |
| ramya         | 4          | 1                |


/********************************************************/

--display dept with out location 
select department_name as department
from departments 
where department_location = 'null';                

| department      |
|-----------------|
| pchh_networking |

/********************************************************/
	
--display dept_name,dept_id , conut(emp in dept)

select d.d_id,d.department_name, count(e.department_id)
from departments d                                        
left join employee_details e
on d.d_id=e.department_id                                           --(employee count in department)
group by d.d_id,d.department_name;  


| D_ID | DEPARTMENT_NAME | COUNT(E.DEPARTMENT_ID) |
|:----:|:---------------:|:----------------------:|
|   1  |     pchh_it     |            3           |
|   2  |  pchh_marketing |            1           |
|   3  | pchh_salesforce |            1           |
|   4  |   pchh_product  |            1           |
|   5  |   pchh_testing  |            0           |
|   6  |  pchh_services  |            0           |
|   7  | pchh_networking |            0           |
    
 /*******************************************************/
    
--display department name which has atleast one employee name starts with 'A'    
  
select d.department_name
from departments d 
join employee_details e                                       --(employee_name in a starting -> dept_name)
on d.d_id=e.department_id 
where e.employee_name like 'a%' 
group by (e.department_id,d.department_name); 

| DEPARTMENT_NAME |
|:---------------:|
| pchh_it         |



/************************************************************/

--display employee detail whose joining date is "dd/mm/yyyy"
select d.department_name,e.employee_name,e.birth_date,e.joining_date,e.pan_card,e.adhar_num
from employee_details e 
inner join departments d 
on e.department_id=d.d_id                                                  --(who join those fix date)
where e.joining_date='03/mar/2019';

| DEPARTMENT_NAME | EEMPLOYEE_NAME | BIRTH_DATE | JOINING_DATE | PAN_CARD  | ADHAR_NUM    |
|-----------------|----------------|------------|--------------|-----------|--------------|
| pchh_product    | ramya          | 11-MAR-98  | 03-MAR-19    | 145678930 | 353767388992 |

/******************************************************/



--list the department ID and name of all the departments where no employee is working
SELECT * FROM departments 
WHERE d_id 
NOT IN (select department_id FROM employee_details);                      --(no employee in department)
    
    
| D_ID |  DEPARTMENT_NAME | MANAGER_ID | DEPARTMENT_LOCATION |
|:----:|:----------------:|:----------:|:-------------------:|
|   5  | pchh_testing     |      4     |       chennai       |
|   6  |  pchh_services   |      1     |       chennai       |
|   7  |  pchh_networking |      -     |          -          |


--employee_who belong to 'kerala' using triple join

select e.e_id,e.employee_name,e.birth_date,e.joining_date,e.pan_card,s.states_id,s.state_name,ad.city_name
from employee_details e 
left join employee_addresses ad
on e.e_id=ad.emp_id 
left join states s 
on s.states_id=ad.state_id
where s.state_name='KERALA';                            --(kerala)

| e_id | employye_name |  birth_date | joining_date |  pan_card | states_id| state_name |  city_name   |
|:----:|:-------------:|:-----------:|:------------:|:---------:|:--------:|:----------:|:-------------:
|   2  |    vinayak    |  22-OCT-98  |   03-NOV-19  | 142648797 |     2    |   kerala   |   cochin     |
|   4  |     ramya     | 11-MAR-1998 |  03-MAR-2019 | 145678930 |     2    |   kerala   |   kollam     |




```

/*******************************************/

### feautures: EXTRACTING TABLE
```sql

   SALARY_TABLE
   
   RELATIONSHIP   ->   CARE_OF_DEATILS
   
   JOB_ROLE
   
   JOB_HISTORY
   ;l;;;'
   

    
    
    



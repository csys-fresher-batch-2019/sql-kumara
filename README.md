# Employee Management system

*https://Pachak-emp-details-systems.in

## Features

*users should be able to view company_employee_details

### Features 1: Deatils_of_Employee_department

```sql


create table departments
( 
     d_id number ,                                       --primary key
     department_name varchar2(20) not null,
     manager_id varchar2(20) not null,
     department_location varchar2(20),
     constraint dept_pk primary key(d_id),
     constraint manager_id_uq unique (manager_id,department_name) 
);
insert into departments(d_id,department_name,manager_id,department_location) values (1,'pchh_it',1,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (2,'pchh_marketing',2,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (3,'pchh_salesforce',3,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (4,'pchh_product',1,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (5,'pchh_testing',4,'chennai');
insert into departments(d_id,department_name,manager_id,department_location) values (6,'pchh_services',2,'chennai');


select * from departments;
drop table departments;


| department_id | department_name | manager_id | department_location |
|:-------------:|-----------------|------------|---------------------|
|       1       | pchh_it         |      1     |       chennai       |
|       2       | pchh_marketing  |      2     |       chennai       |
|       3       | pchh_salesforce |      3     |       chennai       |
|       4       | pchh_product    |      4     |       chennai       |
|       5       | pchh_testing    |      5     |       chennai       |
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

insert into employee_details values(1,1,'anbuselvam','male',to_date('03-03-1997','dd-mm-yyyy'),to_date('03-01-2019','dd-mm-yyyy'),'234567891','','WA25728567','9585758494');
insert into employee_details values(2,2,'vinayak','male','22-OCT-98','03-NOV-19','142648797 ','453782827378','1347537WA8','9835353664');
insert into employee_details values(3,3,'vijaykumar','male','12-APR-1996','03-NOV-2019','124367898','242627227388','12145EA5368','9242525643');
insert into employee_details values(4,4,'ramya','female','11-MAR-1998','03-MAR-2019','145678930','353767388992','','8356342526');
insert into employee_details values(5,5,'velan','male','16-JAN-1998','04-NOV-2019','156372890','345362728299','574838393PS','8134556266');
insert into employee_details values(6,1,'alex','male','12-NOV-1997','04-NOV-2019','123456781','252627288899','46373738DW','9562727278');




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
### Feauture: queries


    
    select * from states s
    right join employee_addresses e
    on s.states_id=e.state_id
    right join countries c
    on c.country_id=s.country_id;
    
    select country_id,state_name,
    (select country_id from countries c where s.states_id=c.country_id)
    from states s;
	
    
    
    
    



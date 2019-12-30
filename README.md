# Employee Management system

*https://Pachak-emp-details-systems.in

## Features

*users should be able to view company_employee_details

### Features 1: Deatils_of_Employees

```sql


create table departments
( 
     d_id number ,              --PRIMARY KEY
     department_name varchar2(20) not null,
     manager_id varchar2(20) not null,
     department_location varchar2(20),
     constraint dept_pk primary key(d_id)
);

insert into departments values(1,'sec_it',1,'chennai');



create table employee_details
(
    e_id number ,	          --PRIMARY KEY 
    department_id number not null,	--FOREIGN KEY
    employee_name varchar2(55) not null,
    birth_date date,
    joining_date date ,
    pan_card varchar2(20) NOT NULL,     
    adhar_num  number,                  --UNIQUE KEY
    driving_license_num varchar2(20), 	--UNIQUE KEY
    employee_mobnum number,             --UNIQUE KEY
    constraint emp_dept_pk primary key(e_id),
    constraint emp_adhar unique(adhar_num),
    constraint emp_dl_uq unique(driving_license_num),
    constraint emp_mobno_uq unique(employee_mobnum),
    constraint emp_fk foreign key (department_id) references departments(d_id),
    constraint proof_chk check (adhar_num is not null or driving_license_num is not null) 
);

insert into employee_details values(1,1,'pachak','14/10/1997',sysdate,'123456789','879567584567','wa1234rt567','9807896780');
insert into employee_details values(2,1,'mochak','01/01/1997','26/11/2019','123456781','879567584556','','9807896894');
insert into employee_details values(3,1,'lochak','11/01/1997','26/11/2019','323456781','','A2345678964,'9807896123');

select * employee_details;

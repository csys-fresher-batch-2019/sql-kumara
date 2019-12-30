# Employee Management system

*https://TVS-emp-details-systems.in

## Features

*users should be able to view company departments

### Features 1: To create a company-Department table

```sql


create table departments
( 
     d_id number ,   --primary key
     department_name varchar2(20) not null,
     manager_id varchar2(20) not null,
     Department_location varchar2(20),
     constraint dept_pk primary key(d_id)
      --constraint manager_id_uq unique (manager_id)
);

insert into departments values(1,'sec_it',1,'chennai');


create table employee_details
(
    e_id number,	          --PRIMARY KEY 
    department_id number,	--FOREIGN KEY
    employee_name varchar2(55),
    birth_date date,
    joining_date date default sysdate,
    pan_card varchar2(20) NOT NULL,
    adhar_num  number,
    driving_license_num varchar2(20), 	--UNIQUE KEY
    employee_mobnum number,
    constraint emp_dept_pk primary key(e_id),
    constraint emp_adhar unique(adhar_num),
    constraint emp_dl_uq unique(driving_license_num),
    constraint emp_mobno_uq unique(employee_mobnum),
    constraint emp_fk foreign key (department_id) references departments(d_id),
    constraint proof_chk check (adhar_num is not null or driving_license_num is not null) 
);

insert into employee_details values(1,1,'pchh','14/10/1997',sysdate,'123456789','879567584567','wa1234rt567','9807896780');

# Employee Management system

*https://TVS-emp-details-systems.in

## Features

*users should be able to view company departments

### Features 1: To create a company-Department table

```sql




create table departments
( 
     id number ,
     department_name varchar2(20) not null,
     manager_id varchar2(20) not null,
     Department_location varchar2(20) default 'CHENNAI',
     constraint dept_pk primary key(id)
      --constraint manager_id_uq unique (manager_id)
);

create table employee_details
(
    id number,	--PRIMARY KEY 
    department_id number,	--FOREIGN KEY
    employee_name varchar2(55),
    birth_date date,
    joining_date date default current_date,
    pan_card varchar2(20) NOT NULL,
    adhar_num  number,
    driving_license_num varchar2(20), 	--UNIQUE KEY
    employee_mobnum number,
    constraint emp_dept_pk primary key(id),
    constraint emp_adhar unique (adhar_num),
    constraint emp_dl_uq unique (driving_license_num),
    constraint emp_mobno_uq unique (employee_mobnum),
    constraint proof_chk check (adhar_num is not null or driving_license is not null) 
);

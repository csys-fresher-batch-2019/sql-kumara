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


```
### Features 1: Deatils_of_Employees

```sql 
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



CREATE TABLE COUNTRIES(

	COUNTRY_ID number,  --PRIMARY KEY
	COUNTRY_NAME varchar2(20)  not null,
    constraint COUNTRY_ID_PK primary key(COUNTRY_ID),
	constraint COUNTRY_NAME_UK unique (COUNTRY_NAME)
		
);

INSERT INTO COUNTRIES(COUNTRY_ID,COUNTRY_NAME) VALUES (1,'INDIA');
INSERT INTO COUNTRIES(COUNTRY_ID,COUNTRY_NAME) VALUES (2,'AFKANISTAN');
INSERT INTO COUNTRIES(COUNTRY_ID,COUNTRY_NAME) VALUES (3,'SRILANKA');



CREATE TABLE STATES(
		COUNTRY_ID number,
		STATES_ID number not null ,
		STATE_NAME varchar2(40),
		CONSTRAINT STATE_ID_PK PRIMARY KEY(STATES_ID),
		CONSTRAINT STATE_NAME_UK UNIQUE(STATE_NAME),
		CONSTRAINT COUNTRY_ID_FK FOREIGN KEY(COUNTRY_ID) REFERENCES COUNTRIES(COUNTRY_ID)
);

INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,2,'TAMILNADU');
INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,3,'ANDRA');
INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,4,'UP');
INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,5,'BIHAR');
INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,6,'NEPAL');
INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,7,'MUMBAI');
INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,8,'KARNATAKA');
INSERT INTO STATES (COUNTRY_ID,STATES_ID,STATE_NAME) VALUES (1,9,'DEHLI');



CREATE TABLE EMPLOYEE_ADDRESSES(
		ADDRESS_ID number,
		EMP_ID number not null ,
		ADDRESS_TYPE varchar2(25),
		ADDRESS_LINE1 varchar2(25) not null,
		ADDRESS_LINE2 varchar(25),
		CITY_NAME varchar2(55) not null,
		PIN_CODE number not null,
		STATE_ID number not null,
		COUNTRY_ID number not null,
		CONSTRAINT ADDR_TYPE_CK CHECK (ADDRESS_TYPE IN ('PERMANANT','TEMPORARY','OFFICE','OTHERS')),
		CONSTRAINT STATES_CHK FOREIGN KEY(STATE_ID) REFERENCES STATES(STATES_ID), 
		CONSTRAINT ADDR_ID_PK PRIMARY KEY(ADDRESS_ID),
        CONSTRAINT EMP_k_FK FOREIGN KEY(EMP_ID) REFERENCES EMPLOYEE_DETAILS(e_id)

);

INSERT INTO EMPLOYEE_ADDRESSES(ADDRESS_ID,EMP_ID,ADDRESS_TYPE,ADDRESS_LINE1,ADDRESS_LINE2,CITY_NAME,PIN_CODE,STATE_ID,COUNTRY_ID)
	VALUES(1,1,'PERMANANT','#12,KN STREET','NULL','CHENNAI',600012,2,1);

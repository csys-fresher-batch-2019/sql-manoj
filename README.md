# eBUS
  ### * https://ebus.in

## Features
  
   
## Feature 1: User Registration
```sql
create table user_account(
user_name varchar2(30) not null,
user_id number,
user_password varchar2(30) not null,
gender varchar2(6) not null,
dob date not null,
contact_number number(10) not null,
email_id varchar2(40) not null unique,
constraint gender_check check (gender in('M','F','OTHERS')),
constraint user_id_primary_key primary key(user_id),
constraint mobile_number_check check(999999999<contact_number));

create sequence user_id start with 1000 increment by 1;

      insert into user_account values('manoj',user_id.nextval,'manojpass','M',to_date('23-08-1998'),9790291737,'manoj@gmail.com');
      insert into user_account values('ram',user_id.nextval,'rampass','M',to_date('22-08-1998'),9790291739,'ram@gmail.com');
      insert into user_account values('ravi',user_id.nextval,'ravipass','M',to_date('20-08-1998'),9790291730,'ravi@gmail.com');
      
  ```  
  ## User Registration:
| user_name | user_id | user_password | gender | dob        | contact_number | email_id        |
|-----------|---------|---------------|--------|------------|----------------|-----------------|
| manoj     | 1000    | manojpass     | M      | 23-08-1998 | 9790291737     | manoj@gmail.com |
| ram       | 1001    | rampass       | M      | 22-08-1998 | 9790291739     | ram@gmail.com   |
| ravi      | 1002    | ravipass      | M      | 20-08-1998 | 9790291730     | ravi@gmail.com  |


                            
                       
                      
 ## Feature 2:Bus Details  
 ```sql
create table bus_details(
bus_id number,
bus_name varchar2(20) not null,
from_location varchar2(20) not null,
to_location varchar2(20) not null,
journey_date date not null,
ticket_price number not null,
travelling_time varchar2(20) not null,
constraint b_primary primary key(bus_id),
constraint f_t_chech check(from_location <> to_location));
                            
                            
 insert into bus_details values(101,'YBM','tirupur','chennai',to_date('1-2-2020'),1000,'23:00 to 07:00');
insert into bus_details values(102,'ABC','tirupur','salem',to_date('21-2-2020'),1000,'01:00 to 08:00');
insert into bus_details values(103,'ABC','chennai','coimbatore',to_date('2-2-2020'),500,'10:00 to 18:00');
insert into bus_details values(104,'XYZ','theni','coimbatore',to_date('22-2-2020'),500,'10:00 to 18:00');
insert into bus_details values(105,'XYZ','theni','coimbatore',to_date('23-2-2020'),500,'10:00 to 18:00');

                          
 
 
                         select * bus_details;
```


## Bus_details
| bus_id | bus_name | from_location | to_location | journey_date | ticket_price | travelling_time  |
|--------|----------|---------------|-------------|--------------|--------------|------------------|
|  100   |   KPN    |  tirupur      |  chennai    | 1-2-2020     |   1000       |  23:00 to 07:00  |
|  101   |   ABC    |  tirupur      |  salem      | 21-2-2020    |   1000       |  01:00 to 08:00  |
|  102   |   ABC    |  chennai      | coimbatore  | 2-2-2020     |    500       |  10:00 to 18:00  |
|  103   |    XYZ   |  theni        | coimbatore  | 22-2-2020    |    500       |  10:00 to 18:00  |
|  104   |   XYZ    |  chennai      |  coimbatore | 23-2-2020    |    500       |  10:00 to 18:00  |  
                            
                            
                            
## Feature 3:Seat Availability                            
```sql
create table seat_availability(
bus_id number not null unique,
maximum_seats number not null,
available_seats number not null,
constraint check_available check(available_seats>=0),
constraint check_maximum check(maximum_seats>0));


insert into seat_availability values(101,60,60);
insert into seat_availability values(102,50,50);
insert into seat_availability values(103,40,40);
insert into seat_availability values(104,50,50);
insert into seat_availability values(105,60,60);
                        
                        
```
## Seat_availability
| bus_id | maximum_seats | available_seats |
|--------|---------------|-----------------|
| 100    | 60            | 60              |
| 101    | 50            | 49              |
| 102    | 40            | 39              |
| 103    | 50            | 50              |
| 104    | 60            | 60              |
   
 ## Feature 4:Passenger Details
   ``` sql
 create table passenger_details(
booking_id number ,
user_id number not null,
bus_id number not null,
passenger_name varchar2(30) not null,
age number not null,
gender varchar2(10),
mobile_number number not null ,
no_of_tickets number not null,
booking_status varchar2(15) default 'pending',
constraint age_chk check(age>=0),
constraint gender_chk check (gender in('M','F','OTHERS')),
constraint booking_status_check check(booking_status in('booked','cancelled','pending')),
constraint primary_booking primary key(booking_id),
constraint foreign_userid foreign key(user_id) references user_account (user_id),
constraint mobile_check check(mobile_number>999999999),
constraint no_tickets check(no_of_tickets>=0));


select*from passenger_details;


create sequence sequence_booking_id start with 30 increment by 1; 
  
   ```
   
   
 ## Passenger Details 
   
| booking_id | bus_id | user_id | passenegr_name | age | gender | mobile_number | no_of_tickets | booking_status |
|------------|--------|---------|----------------|-----|--------|---------------|---------------|----------------|
| 10         | 101    | 1000    | manoj          | 21  | M      | 9790291737    | 1             | booked         |
| 11         | 102    | 1001    | ram            | 21  | M      | 8989098789    | 1             | booked         |



   ## Feature 5:Payment Status
   ```sql
create table payment_status(
user_id number not null,
bus_id number not null,
booking_id number not null,
total_price number not null,
paid_status varchar(15) default 'pending',
transaction_id number,
constraint payment_status  check(paid_status in('success','pending','failure','returned','COD','cancelled')),
constraint check_price check(total_price>0),
constraint second_foreign_bid foreign key(bus_id) references bus_details(bus_id));

select*from payment_status;
                        
   ```
 ## Payment Status
   
| user_id | bus_id | booking_id | total_price | paid_status | transaction_id |
|---------|--------|------------|-------------|-------------|----------------|
| 1000    | 101    | 10         | 1000        | success     |                |
| 1001    | 102    | 11         | 1000        | success     |                |
   













 








                      
                         
                        
                         
                        
                      
   
   
   
   
   
   
   
   
   
   
   
   
   
   
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
                        

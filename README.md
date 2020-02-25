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
| 101    | 50            | 50              |
| 102    | 40            | 40              |
| 103    | 50            | 50              |
| 104    | 60            | 60              |
   
 ## Feature 4:Reservation Information
   ``` sql
       
   create table reservation_info(ticket_num number,
                                 p_id number not null,
                                 route_id number not null,
                                 bus_id number not null,
                                 no_of_tickets number not null,
                                 constraint check_no_tickets check(no_of_tickets>0),
                                 constraint primary_key_tic_num primary key(ticket_num),
                                 constraint foreign_key_p_id foreign key(p_id) references passenger_info(p_id),
                                 constraint foreign_key_b_id foreign key(bus_id) references bus_info(bus_id),
                                 constraint foreign_key_route_id foreign key(route_id) references route_info(route_id)
                                 );
                                 
                      
                      insert into reservation_info values(12345,1002,120,100,1);                     
                      insert into reservation_info values(12346,1001,121,101,1);                     
                      insert into reservation_info values(12347,1004,122,102,1);                     
                      insert into reservation_info values(12348,1003,123,103,1);
                      
                      
                      select * from reservation_info;
                      
   
   ```
   
   
 ## Reservation_Info 
   
| ticket_num | p_id | route_id | bus_id | no_of_tickets |
|------------|------|----------|--------|---------------|
| 12345      | 1002 | 120      | 100    | 1             |
| 12346      | 1001 | 121      | 101    | 1             |
| 12347      | 1004 | 122      | 102    | 1             |
| 12348      | 1003 | 123      | 102    | 1             |



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
   













 








                      
                         
                        
                         
                        
                      
   
   
   
   
   
   
   
   
   
   
   
   
   
   
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
                        

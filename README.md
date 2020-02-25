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
                            
                           

                            
                           



 

                            
                            
## Feature 3:Route Information                            
```sql
create table route_info(route_id number,
                        bus_id number not null,
                        fare number not null,
                        departure_date_time timestamp not null,
                        arrival_date_time timestamp not null,
                        constraint foreign_key_bud_id foreign key(bus_id) references bus_info(bus_id),
                        constraint primary_key_route_id primary key (route_id),
                        constraint check_fare check(fare>=0)
                        ); 
       
insert into bus_details values(101,'YBM','tirupur','chennai',to_date('1-2-2020'),1000,'23:00 to 07:00');
insert into bus_details values(102,'ABC','tirupur','salem',to_date('21-2-2020'),1000,'01:00 to 08:00');
insert into bus_details values(103,'ABC','chennai','coimbatore',to_date('2-2-2020'),500,'10:00 to 18:00');
insert into bus_details values(104,'XYZ','theni','coimbatore',to_date('22-2-2020'),500,'10:00 to 18:00');
insert into bus_details values(105,'XYZ','theni','coimbatore',to_date('23-2-2020'),500,'10:00 to 18:00');
insert into bus_details values(106,'ABC','theni','coimbatore',to_date('23-2-2020'),500,'11:00 to 19:00');
insert into bus_details values(107,'YBM','tirupur','banglore',to_date('23-2-2020'),500,'20:00 to 07:00');
insert into bus_details values(108,'qwerty','salem','trichy',to_date('03-03-2020'),300,'10:00 to 13:00');


           
                        select * from route_info;
                        
                        
```
## Route_info
| route_id | bus_id | fare | departure_date_time | arrival_date_time |
|----------|--------|------|---------------------|-------------------|
| 120      | 100    | 500  |  23-01-20 10:00PM   |  24-01-20 05:00AM |
| 121      | 101    | 600  |  05-01-20 11:00AM   |  05-01-20 05:00PM |
| 122      | 102    | 500  |  23-01-20 01:00PM   |  23-01-20 08:00PM |
| 123      | 103    | 800  |  20-01-20 10:00PM   |  21-01-20 05:00AM |
| 124      | 104    | 500  |  29-01-20 05:00AM   |  29-01-20 11:00AM |
   
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



   ## Feature 5:Seats Availability
   ```sql
         create table seat_availability(bus_id number not null,
                                        available_seats number not null,
                                        constraint foreign_k_bus_id foreign key(bus_id) references bus_info(bus_id),
                                        constraint check_no_of_seats check(available_seats>=0)
                                        );
                                        
                         insert into seat_availability values(100,49);
                         insert into seat_availability values(101,39); 
                         insert into seat_availability values(102,39);
                         insert into seat_availability values(103,44); 
                         insert into seat_availability values(104,50);
                         
                          select * from seat_availability;
                        
   ```
   ## seat_availability
   
   
   
| bus_id | available_seats |
|--------|-----------------|
| 100    | 49              |
| 101    | 39              |
| 102    | 39              |
| 103    | 44              |
| 104    | 50              |


To find seat availability:
```sql

CREATE OR REPLACE FUNCTION SEATS_AVAILABLE (i_bus_id IN number)
RETURN NUMBER AS 
remaining_seats number;
booked_seats number;
maximum_seats number;

BEGIN
select max_seats into maximum_seats from bus_info where bus_id=i_bus_id;
select sum(no_of_tickets) into booked_seats from reservation_info where bus_id=i_bus_id;
  remaining_seats := maximum_seats - booked_seats;
  RETURN remaining_seats;
END SEATS_AVAILABLE;

select SEATS_AVAILABLE(100) from dual;
```

To find route id of the bus:
```sql
CREATE OR REPLACE FUNCTION ROUTE_ID (i_bus_id number)
RETURN NUMBER AS 
r_id number;
rou_id number;

BEGIN
select route_id into r_id from route_info where bus_id=i_bus_id;
rou_id := r_id;
  RETURN rou_id;
END ROUTE_ID;

select ROUTE_ID(100) from dual;
```
To find fair of the bus:
```sql
select b.bus_name,b.from_location,b.to_location,r.fare from bus_info b,route_info r where b.bus_id=r.bus_id;

 

```
To find fair of the travel(left join):
```sql
 select p.p_id,p.bus_id,r.fare from reservation_info p left join route_info r on p.bus_id=r.bus_id;

```
To find maximum no of seats and available seats:
```sql
SELECT b.bus_id,b.max_seats,s.available_seats
FROM bus_info b
FULL OUTER JOIN seat_availability s ON b.bus_id=s.bus_id;

```
To find busses with AC:
```sql
select distinct b.bus_id,c.AC from bus_info b,bus_info c where b.AC=c.AC AND b.AC=1;
```
To display available buses:
```sql
select bus_name from bus_info;

```

To find passenger who has not submitted pan details:

```sql

select p_name from passenger_info where pan_num is null;


```
To find passenger who has not submitted aadhar details:
```sql
select p_name from passenger_info where pan_num is null;


```
To update bus fare:
```sql
UPDATE route_info
SET fare=600
WHERE bus_id= 100;
```
To find buses with seats above 40:
```sql
SELECT * 
   FROM bus_info 
   WHERE max_seats IN (SELECT max_seats 
         FROM bus_info
         WHERE max_seats>40) ;

```
To find bus information with available seats:
```sql
SELECT b.*,s.available_seats
FROM bus_info b
FULL OUTER JOIN seat_availability s ON b.bus_id=s.bus_id;
```         

















 








                      
                         
                        
                         
                        
                      
   
   
   
   
   
   
   
   
   
   
   
   
   
   
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
                        

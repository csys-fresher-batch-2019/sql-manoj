# eBUS
  ### * https://ebus.in

## Features
  
   
## Feature 1: Bus Information
```sql
      create table bus_info(s_no number not null,
                            bus_id number,
                            bus_name varchar2(20) not null,
                            max_seats number not null,
                            bus_type varchar2(20) not null,
                            ac varchar2(20) not null,
                            from_location varchar2(30) not null,
                            to_location varchar2(30) not null,
                            constraint bus_id_pk primary key (bus_id),
                            constraint bus_type_check check (bus_type in('seater','sleeper','semi-sleeper')),
                            constraint ac_check check (ac in('1','0')),
                            constraint from_to_check check (from_location <> to_location),
                            constraint max_seats_check check(max_seats>0)
                            );
                            create sequence s_no_sequence start with 1 increment by 1;
                            
                            insert into bus_info values(s_no_sequence.nextval,100,'KPN',50,'sleeper',1,'chennai','tirupur');
                            insert into bus_info values(s_no_sequence.nextval,101,'YBM',40,'seater',1,'chennai','salem');
                            insert into bus_info values(s_no_sequence.nextval,102,'YBM',40,'sleeper',1,'tirupur','banglore');
                            insert into bus_info values(s_no_sequence.nextval,103,'APPLE',45,'semi-sleeper',0,'coimbatore','chennai');
                            insert into bus_info values(s_no_sequence.nextval,104,'ABC',50,'seater',0,'chennai','salem');
                            
                            select * from bus_info;
  ```                          
# bus_info                            
| s_no | bus_id | bus_name | max_seats | bus_type       | AC | from_location | to_location |
|------|--------|----------|-----------|----------------|----|---------------|-------------|
|  1   |  100   |   KPN    |    50     |  seater        | 1  |  chennai      |  tirupur    |
|  2   |  101   |   YBM    |    40     |  sleeper       | 1  |  chennai      |  salem      |
|  3   |  102   |   YBM    |    40     |  seater        | 1  |  tirupur      |  banglore   |
|  4   |  103   |  APPLE   |    45     |  semi-sleeper  | 0  |  coimbatore   |  chennai    |
|  5   |  104   |   ABC    |    50     |  seater        | 0  |  chennai      |  salem      |
                            
                           


                            
                       
                      
 ## Feature 2:Passenger Information   
 ```sql
 create table passenger_info(p_id number,
                            p_name varchar2(30) not null,
                            mob_num number(10) not null,
                            age number not null,
                            aadhar_num number(12) unique,
                            pan_num varchar2(10) unique,
                            constraint p_id_pk primary key(p_id),
                            constraint mob_num_unique unique(mob_num),
                            constraint age_check check (age>=0),
                            constraint pan_or_aadhar_not_null check (length(aadhar_num||pan_num) is not null),
                            constraint mob_num_check check(mob_num>999999999),
                            constraint aadhar_num_check check(aadhar_num>99999999999)
                            );
                            
                            
                            
                          
 insert into passenger_info(p_id,p_name,mob_num,age,aadhar_num) values (1001,'aravinth',9876543210,22,123443211234);
 insert into passenger_info(p_id,p_name,mob_num,age,aadhar_num,pan_num) values (1002,'manoj',9234567895,21,123416341234,'ABCD1234E');
 insert into passenger_info(p_id,p_name,mob_num,age,aadhar_num,pan_num) values (1003,'manoj',9234567899,21,123416349999,'QWERT1234Y');
 insert into passenger_info(p_id,p_name,mob_num,age,pan_num) values (1004,'ram',9934567895,21,'ADFGH9999T');
 
 
                         select * from passenger_info;
```


## passenger_info
| p_id | p_name   | mob_num    | age | aadhar_num   | pan_num    |
|------|----------|------------|-----|--------------|------------|
| 1001 | aravinth | 9876543210 | 22  | 123443211234 |     -      |
| 1002 | manoj    | 9234567895 | 21  | 123416341234 | ABCD1234E  |
| 1003 | manoj    | 9234567899 | 21  | 123416349999 | QWERT1234Y |
| 1004 | ram      | 9934567895 | 21  |      -       | ADFGH9999T |
 
 
 

                            
                            
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
       
       insert into route_info values(120,100,500,to_date('23-01-2020 10:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
       to_date('24-01-2020 05:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
       insert into route_info values(121,101,600,to_date('05-01-2020 11:00:00AM','dd-mm-yyyy hh:mi:ssPM'),
       to_date('05-01-2020 05:00:00PM','dd-mm-yyyy hh:mi:ssPM'));
       insert into route_info values(122,102,500,to_date('23-01-2020 01:00:00PM','dd-mm-yyyy hh:mi:ssAM'),
       to_date('23-01-2020 08:00:00PM','dd-mm-yyyy hh:mi:ssPM'));
       insert into route_info values(123,103,800,to_date('20-01-2020 10:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
       to_date('21-01-2020 05:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
       insert into route_info values(124,104,500,to_date('29-01-2020 05:00:00AM','dd-mm-yyyy hh:mi:ssPM'),
       to_date('29-01-2020 11:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
       
           
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
To update bud fare:
```sql
UPDATE route_info
SET fare=600
WHERE bus_id= 100;
```
To find buses with seats above 40:
```
SELECT * 
   FROM bus_info 
   WHERE max_seats IN (SELECT max_seats 
         FROM bus_info
         WHERE max_seats>40) ;

```















 








                      
                         
                        
                         
                        
                      
   
   
   
   
   
   
   
   
   
   
   
   
   
   
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
                        

# eBUS
  ### * https://ebus.in

## Features
  
   
## Feature 1: List of Buses
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
                            
                            insert into bus_info values(s_no_seq.nextval,100,'KPN',50,'sleeper',1,'chennai','tirupur');
                            insert into bus_info values(s_no_seq.nextval,101,'YBM',40,'seater',1,'chennai','salem');
                            insert into bus_info values(s_no_seq.nextval,102,'YBM',40,'sleeper',1,'tirupur','banglore');
                            insert into bus_info values(s_no_seq.nextval,103,'APPLE',45,'semi-sleeper',0,'coimbatore','chennai');
                            insert into bus_info values(s_no_seq.nextval,104,'ABC'',50,'seater',0,'chennai','salem');
                            
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
                            constraint mob_num_check check(mob_num>999999999)
                            constraint aadhar_num_check check(aadhar_num>99999999999)
                            constraint pan_num_check check(pan_num like '[A-Z][A-Z][A-Z][A-Z][A-Z][0-9][0-9][0-9][0-9][A-Z]')
                            );
                            
                            
                          
 insert into passenger_info(p_id,p_name,mob_num,age,aadhar_num) values (1001,'aravinth',9876543210,22,123443211234);
 insert into passenger_info(p_id,p_name,mob_num,age,aadhar_num,pan_num) values (1002,'manoj',9234567895,21,123416341234,'ABCD1234E');
 insert into passenger_info(p_id,p_name,mob_num,age,aadhar_num,pan_num) values (1003,'manoj',9234567899,21,123416349999,'QWERT1234Y');
 insert into passenger_info(p_id,p_name,mob_num,age,pan_num) values (1004,'ram',9934567895,21,'ADFGH9999T');
 
 
                         select * from passenger_info;
```
# passenger_info
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
                        boarding_date_time datetime not null,
                        departure_date_time datetime not null,
                        constraint foreign_key_bud_id foreign key(bus_id) references bus_info(bus_id),
                        constraint primary_key_route_id primary key (route_id),
                        constraint check_fare check(fare>=0)
                        ); 
       
       insert into route_info values(120,100,500,'chennai','tirupur',to_date('23-01-2020 10:00:00','dd-mm-yyyy hh:mi:ssPM');
       insert into route_info values(121,101,600,'chennai','salem',to_date('05-01-2020 11:00:00','dd-mm-yyyy hh:mi:ssPM');
       insert into route_info values(122,102,500,'chennai','tirupur',to_date('23-01-2020 01:00:00','dd-mm-yyyy hh:mi:ssAM');
       insert into route_info values(123,103,800,'coimbatore','chennai',to_date('20-01-2020 10:00:00','dd-mm-yyyy hh:mi:ssPM');
       insert into route_info values(124,104,500,'chennai','salem',to_date('29-01-2020 05:00:00','dd-mm-yyyy hh:mi:ssPM');
           
                        select * from route_info;
                        
                        
   ```
   ## Feature 4:Reservation Information
   ``` sql
       
   create table reservation_info(ticket_num number,
                                 p_id number not null,
                                 route_id not null,
                                 constraint primary_key_tic_num primary key(ticket_num),
                                 constraint foreign_key_p_id foreign key(p_id) references passenger_info(p_id),
                                 constraint foreign_key_route_id foreign_key(route_id) references route_info(route_id)
                                 );
                                 
                      
                      insert into reservation_info values(12345,1002,120);                     
                      insert into reservation_info values(12346,1001,121);                     
                      insert into reservation_info values(12347,1004,122);                     
                      insert into reservation_info values(12348,1003,123);
                      
                      
                      select * from reservation_table;
                      
   
   ```
   
   
   
                      
| ticket_num | p_id | route_id |
|------------|------|----------|
| 12345      | 1002 | 120      |
| 12346      | 1001 | 121      |
| 12347      | 1004 | 122      |
| 12348      | 1003 | 123      |
   
   
   
   
                      
   
   
   
   
                      
                      
   
   
   
   
   
   
   
   
   
   
   
   
   
   
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
       
                        
                        
                        
                        

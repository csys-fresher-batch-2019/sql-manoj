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
                            pan_num varchar unique,
                            constraint p_id_pk primary key(p_id),
                            constraint mob_num_unique unique(mob_num),
                            constraint age_check check (age>=0),
                            constraint pan_or_aadhar_not_null check (coalesce(aadhar_num,pan_num) is not null),
                            constraint mob_num_check check(mob_num>999999999)
                            constraint 
                            );
                            
                            insert into passenger_info(p_id,p_name,mob_num,age,aadhar_num,
                            
                            
                            

# eBUS
   ###  * https://ebus.in

## Features
   ###  * users can able to view all buses.
   
## Feature 1: List of all Buses
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
                            constraint max_seats_check check(max_seats>0),
                            );
                            create sequence s_no_seq start with 1 increment by 1;
                            
                            insert into bus_info values(100,'KPN',50,'sleeper',1,'chennai','tirupur');
                            insert into bus_info values(101,'YBM',40,'seater',1,'chennai','salem');
                            insert into bus_info values(102,'YBM',40,'sleeper,1,'tirupur','banglore');
                            insert into bus_info values(103,'APPLE',45,'semi-sleeper,0,'coimbatore','chennai');
                            insert into bus_info values(104,'ABC'',50,'seater',0,'chennai','salem');
                            
 ## Feature 2:                         
                            
                            

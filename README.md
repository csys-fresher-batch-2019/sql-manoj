# eBUS
   ###  * https://ebus.in

## Features
   ###  * users can able to view all buses.
   
## Feature 1: List of all Buses
```sql
      create table bus_info(bus_id number,
                            bus_name varchar2(20) not null,
                            max_seats number not null,
                            bus_type varchar2(20) not null,
                            ac varchar2(20) not null,
                            from_location varchar2(30) not null,
                            to_location varchar2(30) not null,
                            constraint bus_id_pk primary key (bus_name),
                            constraint bus_type_check check (bus_type in('seater','sleeper','semi-sleeper'),
                            constraint ac_check check(ac in('1','0'),
                            constraint from_to_unique unique (from_location <> to_location)
                            );
                            
                            insert into bus_info('KPN',50,'sleeper',1,'chennai','tirupur');
                            insert into bus_info('YBM',40,'seater',1,'chennai','salem');
                            insert into bus_info('YBM',40,'sleeper,1,'tirupur','banglore');
                            insert into bus_info('APPLE',45,'semi-sleeper,0,'coimbatore','chennai');
                            insert into bus_info('ABC'',50,'seater',0,'chennai','salem');
                            
                            

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
                            constraint bus_name_pk primary key (bus_name),
                            constraint bus_type_check check (bus_type in('seater','sleeper','semi-sleeper'),
                            constraint ac_check check(ac in('yes','no'),
                            constraint from_to_unique unique (from_location,to_location)
                            );
                            
                            
                            

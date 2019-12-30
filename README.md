# eBUS
   ###  * https://ebus.in

## Features
   ###  * users can able to view all buses.
   
## Feature 1: List of all Buses
```sql
      create table Bus_Info(Bus_ID number,Bus_Name varchar2(20) not null,
                            Max_Seats number not null,
                            Bus_Type varchar2(10) not null,
                            AC varchar2(20) not null,
                            constraint Bus_Name_PK primary key (Bus_name),
                            constraint Bus_Type_check check (Bus_Type in('Seater','Sleeper','Semi-Sleeper'),
                            constraint  check( in('yes','no')
                            );
                            ```
                            
                            

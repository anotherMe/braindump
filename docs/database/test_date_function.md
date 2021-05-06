# Test date function

<file sql>
create or replace function datetest (text) returns integer as $$
begin
     if ($1 is null) then
         return 0;
     end if;
     perform $1::date;
     return 1;
exception when others then
     return 0;
end;
$$ language plpgsql;
</file>
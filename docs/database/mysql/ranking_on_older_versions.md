

Older versions of MySQL ( version < 8.0 ? ) do not support **rank** function, needless to say they don't support ranking with **partition by** as well.

In order to achieve similar functionality we need to use **variables** ( we're not forced to use *session variables* we can just define variables using **cross joins** ).

One example:

```sql
select 
	case 
		when @partition = concat(c.cod_prat, ' - ', c.num_cont) then  @rank := @rank + 1 
		else @rank := 1
	end as ranking, 
	@partition := concat(c.cod_prat, ' - ', c.num_cont) as partitioning,
	c.*
from contenitori c, (select @rank := 0 ) r, ( select @partition := '' ) p
order by c.cod_prat, c.num_cont, c.prog desc;
```



### References

[MySQLTUTORIAL](https://www.mysqltutorial.org/mysql-row_number/)
[StackOverflos](https://stackoverflow.com/questions/52352877/mysql-5-6-dense-rank-like-functionality-without-order-by)

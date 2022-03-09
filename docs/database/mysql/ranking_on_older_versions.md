

Older versions of MySQL do not support **rank** ( version < 8.0 ? ) function. In order to achieve similar functionality 
we need to use **variables** ( we're not forced to use *session variables* we can just define variables using **cross joins** ).


```sql

	select
		@rank := case 
			when @group = t0.sound then @rank
			else @rank := @rank + 1
		end as ranking,
		@changeColor := case 
			when @group = t0.sound then @changeColor
			else @changeColor := not @changeColor
		end as change_color,
		@group := t0.sound as gruppo,
		t0.*
	from (
		select
		    p.dec_mez,
		    p.d_eta,
		    p.terminal,
		    p.posiz,
		    p.cliente2,
		    p.import2,
		    p.rif_cli,
		    c.num_cont,
		    sp.posizionato_il,
		    sp.spett_rag,
		    case when ssc.identificativo is not null then 'S' else 'N' end as sdoganamento,
		    p.pos_chiusa,
		    concat( COALESCE(p.dec_mez, ''), COALESCE(p.d_eta, ''), COALESCE(p.sbarco_presso_rag, '') ) as sound
		from pratiche p
		inner join conten c 
		    on c.cod_prat=p.posiz		
		left join stp_posizionamento sp 
		    on sp.posiz = p.posiz
		left join stp_posizionamento_cont spc 
		    on spc.id_pos = sp.id
		    and spc.identificativo = c.num_cont
		left join stp_sdoganamento ss 
		    on ss.posiz = p.posiz 
		left join stp_sdoganamento_cont ssc 
		    on ssc.id_stp = ss.id
		    and ssc.identificativo = c.num_cont
		 where p.tipo='I'
		     and (length(c.num_cont) = 11)
		     and year(p.data_ar) < year(curdate())+2
		     and coalesce(p.dec_mez,'') != ''
		order by concat( COALESCE(p.dec_mez, ''), COALESCE(p.d_eta, ''), COALESCE(p.sbarco_presso_rag, '') )
	) as t0
	cross join (SELECT @rank := 0) r
	cross join (SELECT @changeColor := TRUE) c
	cross join (select @group := '') g;
	
```



### References

[MySQLTUTORIAL](https://www.mysqltutorial.org/mysql-row_number/)
[StackOverflos](https://stackoverflow.com/questions/52352877/mysql-5-6-dense-rank-like-functionality-without-order-by)

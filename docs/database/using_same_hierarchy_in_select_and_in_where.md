====== Using same hierarchy in SELECT and in WHERE ======

Long story short: you can't.

But, as stated in [[http://stackoverflow.com/questions/12964203/mdx-error-hierarchy-already-appears-in-the-axis0-axis|this article]], it's possible to modify the query.

So, instead of this MDX query:

<code>
select
	[X Comuni].[SedeCPI].members on 0
from
	[OML_DWH]
where
	(
		[Measures].[Conteggio di Assunzioni],
		[X Comuni].[SedeCPI].&[Campobasso]
	)
</code>

You could have written:

<code>
select
	[X Comuni].[SedeCPI].members on 0
from
(	
	select [X Comuni].[SedeCPI].&[Campobasso] on 0
	from [OML_DWH]
	where [Measures].[Conteggio di Assunzioni]
)
</code>

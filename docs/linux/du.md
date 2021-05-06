
====== du - estimate file space usage ======

===== Show only total for each directory =====

<code>du -cshx *</code>

<code>
-c, --total :: produce a grand total
-h, --human-readable :: human readable format
-s, --summarize :: display only a total for each argument
-x, --one-file-system :: skip directories on different file systems
</code>

===== Show results sorted by size =====

<code>du -S | sort -g</code>

== References: ==

[[http://linux.die.net/man/1/du|die.net]]
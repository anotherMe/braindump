====== cron ======

==== List cron jobs for current user ====

<code>crontab -l</code>


==== List cron jobs for all user ====

<code>
# for user in $(cut -f1 -d: /etc/passwd); do crontab -u $user -l; done
</code>

==== How to read the crontab ==== 

Each entry in a crontab file consists of six fields, specified in the following order

**minute hour day month weekday command**

The fields are separated by blank spaces or tabs.
 
^ Field        ^ Description ^
| minute       | 0 through 59 |
| hour         | 0 through 23 |
| day of month | 1 through 31 |
| month        | 1 through 12 |
| day of week  | 0 through 7 (0 or 7 is Sunday, 1 is Monday, etc., or use names) |
| command      | This is the complete sequence of commands to be executed for the job |

When an asterisk (*) is displayed, it means all possible values for the field. For example, an asterisk in the hour time field would be equivalent to “every hour”

==== Edit the crontab ==== 

  crontab -e

=== Useful resources ===

[[http://crontab.guru|crontab.guru]]
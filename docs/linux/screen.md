
====== screen Quick Reference ======

How to Navigate, copy & paste content?

within screen sessions:
Cntl a + [  : To start navigation using up/down arrow
Press Space bar: To select content starting position
Press Space bar again: To select a block of content
Cntl a + ] : To paste the selected content

===== Getting in =====

| start a new screen session with session name | ''screen -S //<name>//'' |
| list running sessions/screens | ''screen -ls'' |
| attach to a running session | ''screen -x'' |
| ... to session with name | ''screen -r //<name>//'' |
| the "ultimate attach" | ''screen -dRR'' (Attaches to a screen session.  If the session is attached elsewhere, detaches that other display.  If no session exists, creates one.  If multiple sessions exist, uses the first one.) |

| detach a running session | ''screen -d //<name>//'' |

===== Escape key =====

All screen commands are prefixed by an escape key, by default ''C-a''
(that's Control-a, sometimes written ''^a'').  To send a literal ''C-a''
to the programs in screen, use ''C-a a''. This is useful when working with screen within screen. For example ''C-a a n'' will move screen to a new window on the screen within screen.

===== Getting out =====

| detach | ''[[commands:detach|C-a d]]'' |
| detach and logout (quick exit) | ''[[commands:pow_detach|C-a D D]]'' |
| exit screen | ''[[commands:quit|C-a \]]'' Exit all of the programs in screen. (//not// recommended) | 
| force-exit screen | ''[[commands:quit|C-a C-\]]'' (//not// recommended) |
| getting out of the screen session | exit |

===== Help ====

| See help | ''[[commands:help|C-a ?]]'' (lists keybindings) |

The [[man:start|man page]] is the complete reference, but it's very long.

===== Window Management =====

| create new window | ''[[commands:screen|C-a c]]'' |
| change to last-visited active window | ''[[commands:other|C-a C-a]]'' (commonly used to flip-flop between two windows) |
| change to window by number | ''[[commands:select|C-a <number>]]'' (only for windows 0 to 9) |
| change to window by number or name | ''[[commands:select|C-a ' <number or title>]]'' |
| change to next window in list | ''[[commands:next|C-a n]]'' or ''[[commands:next|C-a <space>]]'' |
| change to previous window in list | ''[[commands:prev|C-a p]]'' or ''[[commands:prev|C-a <backspace>]]'' |
| see window list     | ''[[commands:windowlist|C-a "]]'' (allows you to select a window to change to) |
| show window bar       | ''[[commands:windows|C-a w]]'' (if you don't have window bar) |
| close current window  | Close all applications in the current window (including shell) |
| kill current window   | ''[[commands:kill|C-a k]]'' (not recommended) |
| kill all windows   | ''[[commands:kill|C-a \]]'' (not recommended) |
| rename current window | ''[[commands:title|C-a A]]'' |

===== Split screen =====

| split display horizontally  | ''[[commands:split|C-a S]]'' |
| split display vertically    | ''[[commands:split|C-a | or C-a V (for the vanilla vertical screen patch)]]'' |
| jump to next display region | ''[[commands:focus|C-a tab]]'' |
| remove current region       | ''[[commands:remove|C-a X]]'' |
| remove all regions but the current one | ''[[commands:only|C-a Q]]'' |

===== Scripting =====
# the screen name session has to be valid or else, message: No screen session found.
| send a command to a named session                | ''screen -S //<name>// -X //<command>//'' |
| create a new window and run //ping example.com// | ''screen -S //<name>// -X screen //ping example.com//'' |
| stuff characters into the input buffer\\ using bash to expand a newline character\\ ([[http://lists.gnu.org/archive/html/screen-users/2007-06/msg00012.html|from here]]) | <code bash>screen -S <name> [-p <page>] -X stuff $'quit\r'</code> |
| a full example | <code bash>
# run bash within screen
screen -AmdS bash_shell bash
# run top within that bash session
screen -S bash_shell -p 0 -X stuff $'top\r'

# ... some time later

# stuff 'q' to tell top to quit
screen -S bash_shell -X stuff 'q'
# stuff 'exit\n' to exit bash session
screen -S bash_shell -X stuff $'exit\r'
</code> |

===== Misc =====

| redraw window               | ''[[commands:redisplay|C-a C-l]]'' |
| enter copy mode | ''[[commands:copy|C-a []]'' or ''[[commands:copy|C-a <esc>]]'' (also used for viewing scrollback buffer) |
| paste                       | ''[[commands:paste|C-a ] ]]''  |
| monitor window for activity | ''[[commands:monitor|C-a M]]'' |
| monitor window for silence  | ''[[commands:silence|C-a _]]'' |
| enter digraph (for producing non-ASCII characters) | ''[[commands:digraph|C-a C-v]]'' |
| lock (password protect) display | ''[[commands:lockscreen|C-a x]]'' |
| enter screen command        | ''[[commands:colon|C-a :]]'' |
| enable logging in the screen session | C-a H |
| getting out of the screen session | exit |


===== Scrollback-buffer =====

In copy mode, one can navigate the scrollback buffer in various ways:

| half page up | C-u |
| half page down | C-d |
| cursor left/down/up/right | h/j/k/l |

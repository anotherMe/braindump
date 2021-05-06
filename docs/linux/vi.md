# vi #

## Find & replace ##

Replace every occurence in document:

  :%s/pattern/replace/


## Cut/Copy & Paste ##

  * Position the cursor where you want to begin cutting.
  * Press **v** to select characters (or uppercase **V** to select whole lines, or **Ctrl-v** to select rectangular blocks).
  * Move the cursor to the end of what you want to cut.
  * Press **d** to cut (or **y** to copy).
  * Move to where you would like to paste.
  * Press **P** to paste before the cursor, or **p** to paste after.


## Search

### Simple search

  /mysearchpattern

Press **n** to seek next forward and **N** for backward.


### Case insensitive search

You need to use the \c escape sequence:

  /\cmysearchpattern


## Colors ##

There are many color schemes which are usually distributed together with vim. You can see the available color schemes in vim's colors folder, for example in my case:

  $ ls /usr/share/vim/vimNN/colors/ # where vimNN is vim version

For example, to change color scheme to desert, enter //**:color desert**//. To have the color scheme by default every time you open vim, add :color desert into your ~/.vimrc.

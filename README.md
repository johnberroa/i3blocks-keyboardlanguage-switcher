# i3blocks-keyboardlanguage-switcher
Adds a minimal block to i3blocks that shows the current keyboard layout, and allows switching keyboard layouts with a mod key combination.

I created this altered block because solutions I found online (e.g. using ``xkblayout-state`` weren't working).  For instance, the keyboard layout name for *US English* and *US English International* were both *US*.  I wanted a more fine grained display.  It's most definitely not the most elegant, nor efficient, but it has the desired effect.

It's my first bash script!

## Installation
* Place the block from ``.i3blocks.conf`` wherever you want in your own ``.i3blocks.conf`` config file.
* Place the ``bindsym`` command from ``config`` into your own i3 ``config`` and take note of the mod key combination--it may override a current combination!
* Create (if not already existing) a directory called ``bin`` in your root, and place language and (optionally) language-printer in there.  Make them executable by running: ``chmod +x filename``
* Edit ``~.bashrc`` and add the following line: ``export PATH=$PATH:~/bin``
* Log out and in and all should work.

## Usage
``.i3blocks.conf``: There are two functions:
* ``command=setxkbmap -print | grep xkb_symbols | awk '{print $4}' | awk -F"+" '{print $2}'``
* ``command=language-printer``
The first prints the layout as ``setxkbmap`` outputs.  This is a bit ugly (in my opinion) because it outputs the layout name as, for example, *us* and *us(intl)*.  If this is fine, you can uncomment ``command=language-printer`` and uncomment the ``setxkbmap`` command.  If so, you don't need to place the ``language-printer`` script in your ``bin``.  Also, feel free to set the label for the block if you desire one.

``config``: Fairly straight forward command.  Take out the ``notify-send`` if you don't want a notification to appear when switching keyboards, change the mod key combination to whatever you desire (defaults is mod+space which overrides another default command), and change the signal if you already used 7.

``language``: A script that switches between keyboard layouts based on what layout is currently active.  Here you can add or take away layouts.  To get the proper name, switch in the terminal the layout with ``setxkbmap`` and print the output with ``setxkbmap -print | grep xkb_symbols | awk '{print $4}' | awk -F"+" '{print $2}'``.  Use this for the string equality in the if statements.

``language-printer``: Optional script that prints things nicer.  Essentially the same as ``language``, but will just output the name of the current keyboard layout however you desire.  This is what is displayed in the i3block.

## Development
Feel free to edit/make better/offer suggestions.  I'm open to learn!

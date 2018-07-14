# i3blocks-keyboardlanguage-switcher
Adds a minimal block to i3blocks that shows the current keyboard layout, and allows switching keyboard layouts with a mod key combination.

I created this altered block because solutions I found online (e.g. using ``xkblayout-state`` weren't working).  For instance, the keyboard layout name for *US English* and *US English International* were both *US*.  I wanted a more fine grained display.  It's most definitely not the most elegant, nor efficient, but it has the desired effect.

It's my first bash script!

## Installation
* Place the block from ``.i3blocks.conf`` wherever you want in your own ``.i3blocks.conf`` config file.
* Place the ``bindsym`` command from ``config`` into your own i3 ``config`` and take note of the mod key combination--it may override a current combination!
* Create (if not already existing) a directory called ``bin`` in your root, and place language and (optionally) language-printer in there.  Make them executable by running: ``sudo chmod +x filename``
* Edit ``~.bashrc`` and add the following line: ``export PATH=$PATH:~/bin``
* Log out and in and all should work.

## Usage
Press ``mod+space`` to switch between keyboard layouts.  A notification will appear saying the keyboard layout changed, and the icon on the i3blocks status bar will display the currently active keyboard.

## Files
``language``: A script that switches between keyboard layouts based on what layout is currently active.  Here you can add or take away layouts.  To get the proper name, in the terminal switch the layout with ``setxkbmap`` and print the output with ``setxkbmap -print | grep xkb_symbols | awk '{print $4}' | awk -F"+" '{print $2}'``.  Use this for the string equality in the if statements.

``language-printer``: Optional script that prints things nicer.  Essentially the same as ``language``, but will just output the name of the current keyboard layout however you desire.  This is what is displayed in the i3block.  A cool idea would be to use ``fontawesome`` and place flags instead of text!

``.i3blocks.conf``: There are two commands:
* ``command=setxkbmap -print | grep xkb_symbols | awk '{print $4}' | awk -F"+" '{print $2}'``
* ``command=language-printer``

The first command prints the layout the same way as ``setxkbmap`` outputs it.  This is a bit ugly (in my opinion) because it outputs the layout name as, for example, *us* and *us(intl)*.  If this is fine, you can delete ``command=language-printer`` and uncomment the ``setxkbmap`` command.  If this is done, you don't need to place the ``language-printer`` script in your ``bin``.  Otherwise, it will use the custom ``language-printer`` script.  Also, feel free to set the label for the block if you desire one.

``config``: Fairly straight forward ``bindsym`` command.  Take out the ``notify-send`` if you don't want a notification to appear when switching keyboards, change the mod key combination to whatever you desire (defaults is mod+space which overrides another default command), and change the signal if you already used 7.

## Development
Feel free to edit/make better/offer suggestions.  I'm open to learn!


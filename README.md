00-1 NEW README
mrxvt is a lightweight, tabbed terminal emulator based on rxvt.

The original authors and maintainers are:
> Terminator <jimmyzhou@users.sourceforge.net>
> Gautam Iyer <gi1242@users.sourceforge.net>
> Jehan <zemarmot@users.sourceforge.net>

Due to their lack of time I moved the project to a git repository (as in, here).
For now let us treat it as an unofficial fork. Below, the original README file.


Congratulations! You have purchased an extremely fine
    device that would give you thousands of years of trouble-free 
    service, except that you undoubtably will destroy it via some 
    typical bonehead consumer maneuver. Which is why we ask you
    to PLEASE FOR GOD'S SAKE READ THIS OWNER'S MANUAL CAREFULLY
    BEFORE YOU UNPACK THE DEVICE. YOU ALREADY UNPACKED IT, DIDN'T
    YOU? YOU UNPACKED IT AND PLUGGED IT IN AND TURNED IT ON AND 
    FIDDLED WITH THE KNOBS, AND NOW YOUR CHILD, THE SAME CHILD WHO
    ONCE SHOVED A POLISH SAUSAGE INTO YOUR VIDEOCASSETTE RECORDER
    AND SET IT ON "FAST FORWARD", THIS CHILD ALSO IS FIDDLING
    WITH THE KNOBS, RIGHT?  AND YOU'RE JUST NOW STARTING TO READ 
    THE INSTRUCTIONS, RIGHT???	WE MIGHT AS WELL JUST BREAK THESE 
    DEVICES RIGHT AT THE FACTORY BEFORE WE SHIP THEM OUT, YOU 
    KNOW THAT? 
		-- Dave	Barry, "Read This First!"



00   INTRODUCTION

Mrxvt is a multi-tabbed (like gnome-terminal/konsole) terminal emulator for the
X Window System. It targets to be light-weight, so the desktop environment,
like CDE, KDE or GTK is not required in order to run it. It achieves this
without losing the common useful features, like tab, image and
pseudo-transparent background, multi-style scrollbars, XIM and CJK support,
etc.



01   A BRIEF HISTORY

You can safely skip this section if you do not have time.

For years, a multi-tabbed rxvt has been requested by the users with no luck.
Now, things have changed! Mrxvt (previously named as materm) is a tabbed X
terminal emulator based on aterm/rxvt. It's small, fast, portable, feature rich
and only depends on X library.

An early version of mrxvt is based on multi-aterm v0.1 and named materm.
Multi-aterm was first developed by Alexis from 2002 based on aterm. But the
development seems to stop in 2004 without reaching a usable stable status. So I
took over the project, began to hack it and renamed it to materm. I have made
lots of changes to the code since I dislike the original code style. Hopefully,
I have not broken too many things. ;-)

Due to the limits of aterm, many features are not well implemented in materm,
such as XIM support. So after release 0.2, I decided to pick up the latest rxvt
as the base of new development branch. And the name of the project is changed
to mrxvt. This branch is completely new compared to the branch prior to 0.2. I
have found that rxvt coding style is much better than aterm (except the indent
is horrible ;-)), and it is enjoyable to work on it. I have also ported many
features from aterm and eterm to mrxvt, like tinting and text shadow. Be aware
that some features in the new branch are slightly different from release 0.2,
e.g., color background tinting is available for each individual terminal in
release 0.2, but is global from 0.3.0.

[quote="Gautam Iyer"]
In 2005, I decided to join Jimmy in his wonderful efforts on mrxvt. Mainly
because I had finished my thesis and had a few months to kill before
graduating. I started by fixing a bug with Xft (to get the ACS graphics
characters drawn under Xft), and gradually did major rewrites to the legacy rxvt
code.

Most of the code Jimmy wrote was great. But the old rxvt code sucked! The screen
refresh routines for instance were "flicker-rama". If you moved a tiny clock
over the mrxvt window, then the *whole* window would flicker. Of course, I was
running this on a AMD K6, 500 mHz, with Xft and anti aliasing, so the flicker
was *quite* prominent.

By around August 2006, significant portions of the legacy code has been
overhauled, and I think we have a rock solid code base. If all goes well, maybe
we'll come out with a 1.0 version in 2008.
[/quote]



02   BUG REPORT AND FAQ

Bug reports are very welcome! You can build mrxvt with debug support. So if you
have gdb in your system, you may run mrxvt in gdb with the source to track down
the bug, and report it to me.

To save both your time and my time, please write down detailed steps to
replicate the bug. If I cannot replicate it by myself, I will ignore it even if
it may destroy the universe.

Patches are extremely welcome since I am not familiar with many things, like
multi-languages and accent.

In addition, I may not have time to update the documents in time. Feel free to
help me and the users to improve them. Translations are also welcome. Of course,
not from C to C++ or something like that! You know my meaning of translations.

If you run into certain problems, please read the FAQ file and the man page
before trying to contact me! Your question may be answered by them already. I
most likely will dump your question to /dev/null if it is already answered
there.



03   BUILD AND INSTALL

To build and install from the source, please read INSTALL file!

A quick (lazy) choice is to configure mrxvt as the following. After you
--enable-everything, usually there is no need to enable other options
explicitly. I have found that many distributions, like gentoo, enable other
options with --enable-everything. This is NOT necessary in fact. The option is a
shortcut to avoid a long list of configuration options.

    $ ./configure --enable-everything --disable-debug



04   CONFIGURATION FILE

To run mrxvt with your own preferences, you can set X resources in ~/.mrxvtrc. A
sample mrxvtrc.sample is included in the share/ directory of the source code,
and you can start to hack your own ~/.mrxvtrc from it. You can also customize
mrxvt for all users via a system-wide configuration file, usually
/etc/mrxvt/mrxvtrc or /usr/local/etc/mrxvt/mrxvtrc.

Since 0.5.0, configuration via file ~/.Xdefaults and ~/.Xresources is not
supported any longer. Most options in the config file can be replace by a
(short) command line option if you like command line options.



05   HOTKEY BINDINGS

NOTE: As of 0.5.0, the "hotkey" feature was renamed to "macros".

Several hot key combinations are available for keyboard users. Mrxvt is designed
to be as flexible as possible. It can be surprising to see that many features
can be altered during runtime using hotkeys or escape sequences. Please read the
manual for a list of them. Be aware that they may be changed in the near future
because the shortage of combinations for all features. ;-)

If you do not like the default hot key combinations, you can define the
combinations by yourself. Please read the manual page to find out how to define
them.



06   CJK DISPLAY AND INPUT

To display and input Chinese (Korea/Japanese), you can do the following:

    . Configure mrxvt with "--enable-cjk --enable-xim" options, and build it.

    . Install the correct CJK fonts. Mrxvt will try to look for some default CJK
      fonts if you do not specify them  using the -fm option or mfont X resource
      name. The default CJK fonts are listed in the src/encoding.h file. Notice
      that they are -fm and mfont, NOT -fn and font!!! If you use freetype font,
      use -xftfm option to specify the CJK font family. Notice that -fm and
      -xftfm options use different formats of font names. For details about the
      difference, read the FAQ file.

    . Set environment variable LC_CTYPE to zh_CN (or zh_CN.GBK, zh_CN.GB2312,
      zh_CN.EUC based on your system). Make sure to unset environment variable
      LC_ALL, otherwise LC_CTYPE is overrided. Notice that this setting is
      global for all the following commands you will type in the same shell
      session. You can supply the environment variable to mrxvt at runtime
      instead of setting it globally here. Keep reading the following for
      details.

    . Set X resources in ~/.mrxvtrc. Notice that the value of inputMethod is
      case sensitive.

	Mrxvt.mfont:		  hanzigb16st
	Mrxvt.xftmfont:		  simsun
	Mrxvt.xftSize:		  14
	Mrxvt.multichar_encoding: GB
	Mrxvt.inputMethod:	  SCIM

    . Start the SCIM X input server as usual. For example:

	$ # for ksh/bash users
	$ LC_ALL=zh_CN LANG=zh_CN scim -d
	$ # for csh/tcsh users
	$ env LC_ALL=zh_CN LANG=zh_CN scim -d

    . Execute mrxvt. You can supply the environment variable LC_CTYPE and
      XMODIFIERS to mrxvt at runtime instead of setting them globally as above.
      All you need to do is to run mrxvt as following:

	# the following command is for bash/ksh
	LC_CTYPE=zh_CN XMODIFIERS=@im=SCIM mrxvt &
	# the following command is for csh/tcsh
	env LC_CTYPE=zh_CN XMODIFIERS=@im=SCIM mrxvt &

    . Focus on the mrxvt window, click Ctrl_Space to invoke SCIM

    . For Linux and Mac OS X, setting environment variable LC_ALL (for scim) and
      LC_CTYPE (for mrxvt) to zh_CN or zh_CN.GBK are both good for SCIM/fcitx
      input. For FreeBSD, they must be zh_CN.eucCN for fcitx input. For OpenBSD,
      they can be zh_CN.EUC or zh_CN.GBK for fcitx input.

Mrxvt is tested to work with SCIM, fcitx and gcin on Linux, FreeBSD, OpenBSD and
Mac OS X. It should work fine with other X Input methods, like xcin, Chinput and
miniChinput. It is reported to work with French ascent as well.



07   FEATURES

Major features (* are new features compared with rxvt, + are enhanced
features compared with rxvt):

    * multi-tab support
    * runtime changedable tab title and tab order
    * simple command support (session) for each tab terminal
    * profiles for different tabs
    * macros to define shortcut key combinations
    * input broadcasting to all tab terminals
    * freetype font (Xft) support
    * built-in true translucent window support
    * user configurable keyboard shortcuts
    . pseudo-transparent terminal background
    * pseudo-transparent tabbar background
    * pseudo-transparent scrollbar background
    * pseudo-transparent menubar background
    + user supplied background image per terminal
    * user supplied background image for tabbar
    * user supplied background image for scrollbar
    * user supplied background image for menubar
    + xpm/jpeg/png background image
    * background color tinting
    * runtime changedable tinting color and shading
    * color text shadow and different shadow mode
    * background fading and off-focus fading
    + NeXT/Rxvt/Xterm/SGI/Plain style scrollbar
    + XIM and multi-languages (Chinese/Japanese/Korean) suppport
    . multiple platforms
    . utmp/wtmp/lastlog logging
    . only depends on X, no GTK, no Qt
    . small and fast

For a complete list of all features, please read README.configure file.



08   PORTABILITY

Here are tested platforms that mrxvt is known to work with:

    Slackware Linux 8.1/10.0/10.1/10.2, -current
    Slackintosh 10.1, 10.2 (PPC)
    RedHat Linux 9.0, Enterprise 3, Fedora Core 2/3
    Debian Linux
    Gentoo Linux
    SuSE Linux 8.2, 9.0, 9.1, 9.2
    SUN Solaris (SPARC) 7/8/9/10
    FreeBSD 4.8/5.2.1/5.3
    OpenBSD 3.5/3.6/3.8/3.9
    NetBSD 2.0
    IRIX 6.5
    HP-UX
    Tru64/OSF 5.1
    Mac OS X 10.3 (Panther), 10.4 (Tiger)
    Cygwin

If you cannot find mrxvt in your favorite system (especially open source systems
like Linux and BSD), you may try to contact the system developers and request
them to add it into the system. :-)



09   KNOWN ISSUES

Here are several known issues of mrxvt:

    . UTF-8 is not supported yet.

    . Some users report that they have problem to envoke the SCIM Chinese input
      method under Gentoo 2004.3 and Debian Sarge. I have no idea why this is
      the case because it always works for me. The solution? Dump Gentoo/Debian
      and turn to Slackware, or trace the program and send me patch. ;-)

    . To build mrxvt on HP-UX, you need to disable logging features.

    . Background image support requires libxpm, libpng or libjpeg be installed.
      The images are only tiled on the background of the terminal window. They
      cannot be scaled to fit the window size.

    . XFT support requires freetype, xft and fontconfig libraries be installed.
      Multichar support under XFT requires GNU iconv library be installed, which
      is usually included in GLIBC for Linux systems.

    . If swap screen option is disabled, screen scrolling may behave randomly.
      ;-)  So the safe choice is to always enable it.

    . Tinting and pseudo-transparent are global since 0.3.0. Well, we could
      implement tinting and pseudo-transparent for each individual terminal (not
      a technical difficulty), but it will significantly increase the X
      resources usage since each terminal needs at least one pixmap.

    . Certain characters, e.g., characters with accent in European languages may
      not be correctly displayed under XFT.



10   SECURITY ISSUES

Here are several security issues of mrxvt:

    Before 0.3.10, by default, mrxvt binary is installed as setuid root.
    Although we have tried hard to avoid security problems raised by setuid root
    permission, we do not guarantee 100% safety. You have been warned!!!
    
    From 0.3.10, mrxvt binary will be installed without setuid root due to
    security concerns. Thus, if mrxvt is not compiled with utempter library
    support, you will lose the logging features.

    From 0.3.5, mrxvt supports utempter library, which means if you have
    installed the utempter library, you can remove the setuid root permission
    from mrxvt binary without losing the logging feature. But doing so may cause
    trouble to chown the tty on some systems.

    From 0.4.x, numerous escape sequences were introduced to manipulate tabs.
    This are potential security risks.

    From 0.5.x the above escape sequences are disabled by default, and more
    secure alternates have been provided (macros + popup menus).



11  COPYRIGHT

Mrxvt is licensed under GNU General Public License (GPL). You are free to copy,
modify and redistribute the source and binary of mrxvt under GPL. But there is a
issue with SCO Corp.:

    According to section 4 of the GPL, SCO Corporation of Lindon, Utah (formerly
    Caldera) has no rights to redistribute any versions of Mrxvt and/or Materm
    in any of their products, including (without limitation) OpenLinux,
    Skunkware, OpenServer, and UNIXWare.

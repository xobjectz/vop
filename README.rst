NAME

::

    VOP - objects library


SYNOPSIS

::

    vop <cmd> [key=val] [key==val]
    vop [-a] [-c] [-d] [-h] [-v] [-w]

    options are:

    -a     load all modules
    -c     start console
    -d     start daemon
    -h     display help
    -v     use verbose


DESCRIPTION

::

    VOP contains all the python3 code to program objects in a functional
    way. It provides a base Object class that has only dunder methods, all
    methods are factored out into functions with the objects as the first
    argument. It is called Object Programming (OP), OOP without the
    oriented.

    VOP allows for easy json save//load to/from disk of objects. It
    provides an "clean namespace" Object class that only has dunder
    methods, so the namespace is not cluttered with method names. This
    makes storing and reading to/from json possible.

    VOP has all you need to program a unix cli program, such as disk
    perisistence for configuration files, event handler to handle the
    client/server connection, code to introspect modules for
    commands, deferred exception handling to not crash on an error, a
    parser to parse commandline options and values, etc.

    VOP has a demo bot, it can connect to IRC, fetch and display RSS
    feeds, take todo notes, keep a shopping list and log text. You can
    also copy/paste the service file and run it under systemd for 24/7
    presence in a IRC channel.

    VOP is Public Domain.

USAGE

::

    without any argument the program does nothing

    $ vop
    $

    see list of commands

    $ vop cmd
    cmd,err,mod,req,thr,ver

    list of modules

    $ vop mod
    cmd,err,fnd,irc,log,mod,req,rss,tdo,thr

    use -c to start a console

    $ vop -c

    use mod=<name1,name2> to load additional modules

    $ vop -c mod=irc,rss
    >

    use -v for verbose

    $ vop -cv mod=irc
    VOP started CV started Sat Dec 2 17:53:24 2023
    >


CONFIGURATION

::

    $ vop cfg 
    channel=#objx commands=True nick=objx port=6667 server=localhost

    irc

    $ vop cfg server=<server>
    $ vop cfg channel=<channel>
    $ vop cfg nick=<nick>

    sasl

    $ vop pwd <nsvnick> <nspass>
    $ vop cfg password=<frompwd>

    rss

    $ vop rss <url>
    $ vop dpl <url> <item1,item2>
    $ vop rem <url>
    $ vop nme <url> <name>

COMMANDS

::

    cmd - commands
    cfg - irc configuration
    dlt - remove a user
    dpl - sets display items
    fnd - find objects 
    log - log some text
    met - add a user
    mre - displays cached output
    pwd - sasl nickserv name/pass
    rem - removes a rss feed
    rss - add a feed
    thr - show the running threads

SYSTEMD

::

    save the following it in /etc/systems/system/vop.service and
    replace "<user>" with the user running pipx

    [Unit]
    Description=objects library
    Requires=network-online.target
    After=network-online.target

    [Service]
    Type=simple
    User=<user>
    Group=<user>
    WorkingDirectory=/home/<user>/.vop
    ExecStart=/home/<user>/.local/pipx/venvs/objx/bin/vop -d
    RemainAfterExit=yes

    [Install]
    WantedBy=default.target

    then run this

    $ mkdir ~/.vop
    $ sudo systemctl enable vop --now

    default channel/server is #vop on localhost

FILES

::

    ~/.vop
    ~/.local/bin/vop
    ~/.local/pipx/venvs/vop/

AUTHOR

::

    Bart Thate <bthate@dds.nl>

COPYRIGHT

::

    VOP is Public Domain.

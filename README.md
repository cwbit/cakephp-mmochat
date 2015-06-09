# cakephp-mmochat
World Of Warcraft / MMO inspired chat plugin for CakePHP 3 with channels, tabs, permissions and more using Socket.io and Node.js


# NOTE : this is still a WIP - nothing actually works yet.

##### Configuring Commands and Prefixes

The following, modifiable, configuration settings determine how users can access the available commands

* `/` default prefix for all commands
*  `msg` send a direct message
*  `[a-Z]+` send a message to a channel
*  `join` join a channel
*  `leave` leave a channel
*  `global` send a message globally (to `everyone`)

##### Talking in a Channel

Talk in different channels with slash prefixes

```
/g this is guild chat
/s this is local chat
/trade this is trade channel chat
```

Talk in the last used channel by just typing

```
    > /g hi there
    > i'm still here
```

##### Talking to another user

If enabled, direct chat user-to-user is accomplished by messaging the user directly

By default the identifier for this command is `msg`

```
	/msg some_user Hello!
```

#### Sending Global Messages

.. note: sending a message globally requires certain permissions

Global messages are sent to all currently connected clients. It is the functional equivalent of sending a message to `everyone` and is typically used for things like broadcasting a server shutdown/reboot warning

```
/global message
```

##### Configuring the chat display

Channel prefix displayed as either short or full channel name

```
[g] some_dude >  what's up, peeps?
[guild] some_dude > what's up, peeps?
```

Patterns for the channel display are customizable

```
 [:c] :u > :msg        [g] a_user > hello, world
 [:cc] :u > :msg       [guild] a_user > hello, world
 :t [:cc] :u > :msg    14:35 [guild] a_user > hello, world
```

Valid options for the channel display are

* `:t` time (regional format)
* `:c` channel abbreviation
* `:cc` channel full name
* `:u` user name
* `:msg` the message

##### Understanding channels

Channels are implemented at two levels

* the channel you actually communicate in
* the underlying node.js room the channel is mapped to

Put differently, each channel is both a concept (i.e. I'm in local chat in this zone) as well as an actual unique channel (i.e. local chat in this zone maps to `:zone-local`). This allows us to have multiple `local` channels - ie. a local chat channel in each zone that are not shared between zones.

This is accomplished by mapping each channel to a unique Node.js room.

##### Joining a Channel

To join a channel you may need a password

```
/join foo
[warning] this channel requires a password
/join foo pa$$w0rd
```

##### Leaving a Channel

```
/leave foo
```

##### Creating a channel

.. note: creating a channel requires the appropriate permissions

.. note: channels must be mapped to a node channel pattern

```
channel_pattern
	name
	alias
	password
```
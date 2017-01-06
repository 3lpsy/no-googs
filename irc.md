# IRC

## General

```
$ /join #channelname 

$ /me 'waves hello'
 username waves hello
```

## Register (Freenode)

```
$ /msg NickServ REGISTER password email@example.com
```

## Login (Freenode)
```
$ /connect chat.freenode.net 6667 username:password

$ /nick foo
$ /msg NickServ IDENTIFY foo password

```

# [Weechat](https://weechat.org/files/doc/devel/weechat_quickstart.en.html)

```
$ /set config.section.option value
```

## Add an IRC server

```
$ /server add freenode chat.freenode.net
```

## Set Common IRC Server Options

```
$ /set irc.server.freenode.nicks "mynick,mynick2,mynick3,mynick4,mynick5"
$ /set irc.server.freenode.username "My user name"
$ /set irc.server.freenode.realname "My real name"
$ /set irc.server.freenode.autoconnect on
$ /set irc.server.freenode.addresses "chat.freenode.net/7000"
$ /set irc.server.freenode.command "/msg nickserv identify xxxxxxx"
$ /set irc.server.freenode.autojoin "#channel1,#channel2"
$ /set irc.server.freenode.nicks null/se
```

## Security

May require setting "irc.server.freenode.username" to "" or null

```
$ /set irc.server.freenode.ssl on
$ /set irc.server.freenode.sasl_username "mynick"
$ /set irc.server.freenode.sasl_password "xxxxxxx"

$ /secure passphrase this is my secret passphrase
$ /secure set freenode_password xxxxxxx
$ /set irc.server.freenode.sasl_password "${sec.data.freenode_password}"

```



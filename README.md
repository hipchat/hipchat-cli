hipchat-cli
===========

Some command line scripts for performing [HipChat][hc] API calls.

./hipchat\_room\_message
-----
Used to send a message to a room.

```bash
$ cat message.txt | ./hipchat_room_message -t <token> -r 1234 -f "System"
```

[hc]: http://www.hipchat.com

Configuration
-----

hipchat-cli can be configured with one of the following options in a combination of those.

* Command-line options
* Environment variables
* Configuration file

### Command-line options

Command-line options are passed into hipchat-cli. A list of options is available by executing ```hipchat_room_message -h```.
```
$ hipchat_room_message -h
Usage: hipchat_room_message -t <token> -r <room id> -f <from name>

This script will read from stdin and send the contents to the given room as
a system message.

OPTIONS:
   -h             Show this message
   -t <token>     API token
   -r <room id>   Room ID
   -f <from name> From name
   -c <color>     Message color (yellow, red, green, purple or random - default: yellow)
   -m <format>    Message format (html or text - default: html)
   -n             Trigger notification for people in the room (default: 0)
   -o             API host (api.hipchat.com)
```

### Environment variables

All options available as command-line options can be passed in as environment variables.

Environment variable | Description
-------------------- | -----------
HIPCHAT_TOKEN        | API token
HIPCHAT_ROOM_ID      | Room ID
HIPCHAT_FROM         | From name
HIPCHAT_COLOR        | Message color (yellow, red, green, purple or random - default: yellow)
HIPCHAT_FORMAT       | Message format (html or text - default: html)
HIPCHAT_NOTIFY       | Trigger notification for people in the room (default: 0)
HIPCHAT_HOST         | API host (api.hipchat.com)

#### Usage example:
```bash
$ cat message.txt | HIPCHAT_TOKEN=<token> HIPCHAT_ROOM_ID=1234 ./hipchat_room_message -f "System"
```

### Configuration file

All environment variables can be specified in a configuration file. The configuration file is ```/etc/hipchat```.

#### Usage example:

Configuration in ```/etc/hipchat```:
```bash
HIPCHAT_TOKEN=<token>
HIPCHAT_ROOM_ID=1234
```

Command-line:
```bash
$ cat message.txt | HIPCHAT_FROM="System" ./hipchat_room_message -c green
```

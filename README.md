hipchat-cli
===========

Some command line scripts for performing [HipChat][hc] API calls.

./hipchat\_room\_message
-----
Used to send a message to a room.

    cat message.txt | ./hipchat_room_message -t <token> -r 1234 -f "System"

[hc]: http://www.hipchat.com

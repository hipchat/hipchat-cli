#!/bin/bash

###############################################################################
#
# ./hipchat_room_message
#
# A script for sending a system message to a room.
#
# Docs: http://github.com/hipchat/hipchat-cli
#
# Usage:
#   cat message.txt | ./hipchat_room_message -t <token> -r 1234 -f "System"
#   echo -e "New\nline" | ./hipchat_room_message -t <token> -r 1234 -f "System"
#
###############################################################################

# exit on failure
set -e

usage() {
  cat << EOF
Usage: $0 -t <token> -r <room id> -f <from name>

This script will read from stdin and send the contents to the given room as
a system message.

OPTIONS:
   -h             Show this message
   -t <token>     API token
   -r <room id>   Room ID
   -f <from name> From name
   -c <color>     Message color (yellow, red, green, purple or random - default: yellow)
   -n             Trigger notification for people in the room
   -o             API host (api.hipchat.com)
EOF
}

TOKEN=
ROOM_ID=
FROM=
COLOR=
MESSAGE=
NOTIFY=0
HOST='api.hipchat.com'
while getopts “ht:r:f:c:o:n” OPTION; do
  case $OPTION in
    h) usage; exit 1;;
    t) TOKEN=$OPTARG;;
    r) ROOM_ID=$OPTARG;;
    f) FROM=$OPTARG;;
    c) COLOR=$OPTARG;;
    n) NOTIFY=1;;
    o) HOST=$OPTARG;;
    [?]) usage; exit;;
  esac
done

# check for required args
if [[ -z $TOKEN ]] || [[ -z $ROOM_ID ]] || [[ -z $FROM ]]; then
  usage
  exit 1
fi

# read stdin
INPUT=$(cat)

# replace newlines with XHTML <br>
INPUT=$(echo -n "${INPUT}" | sed "s/$/\<br\>/")

# replace bare URLs with real hyperlinks
INPUT=$(echo -n "${INPUT}" | perl -p -e "s/(?<!href=\")((?:https?|ftp|mailto)\:\/\/[^ \n]*)/\<a href=\"\1\"\>\1\<\/a>/g")

# urlencode with perl
INPUT=$(echo -n "${INPUT}" | perl -p -e 's/([^A-Za-z0-9])/sprintf("%%%02X", ord($1))/seg')

# do the curl
curl -sS \
  -d "auth_token=$TOKEN&room_id=$ROOM_ID&from=$FROM&color=$COLOR&message=$INPUT&notify=$NOTIFY" \
  https://$HOST/v1/rooms/message

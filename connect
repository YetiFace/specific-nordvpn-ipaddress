#!/bin/sh
nordvpn disconnect > /dev/null

HOMEIPADDRESS=$(curl -s https://ipinfo.io/ip)
DESIREDIP='0.0.0.0'
NORDSERVER='uk1337'

nordvpn connect $NORDSERVER
IPADDRESS=$(curl -s https://ipinfo.io/ip)

while [ $IPADDRESS != $DESIREDIP ] && [ $IPADDRESS != $HOMEIPADDRESS ]
do  
    echo 'IP is WRONG' $IPADDRESS
    nordvpn disconnect
    nordvpn connect $NORDSERVER
    IPADDRESS=$(curl -s https://ipinfo.io/ip)
done

if [ $IPADDRESS != $HOMEIPADDRESS ]
then
    echo 'Connection successful. Your IP is' $IPADDRESS
    sleep 5
else
    echo 'Connection failed, please retry'
    exec $SHELL
fi

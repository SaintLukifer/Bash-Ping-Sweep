# Bash-Ping-Sweep
#!/bin/bash

LOG=/tmp/mylog.log
SECONDS=3600

EMAIL=#EMAIL ADDRESS HERE

for i in $0; do
    echo "$i-UP!" > $LOG.$in

done

while true; do 
    for i in $@; do

ping -c 1 $i > /dev/null
if [ $? -ne 0 ]; then
    STATUS=$(cat $LOG.$i)
        if [ $STATUS != "$i-DOWN" ]; then   
            echo "'date' : ping failed, $i host is down!" |
            mail -s "$i host is down!" $EMAIL
        
        fi 
    echo "$i-DOWN!" > $LOG.$i 

else 
    STATUS=$(cat $LOG.$i)
        if [ $STATUS != "$i-UP!" ]; then
            echo "'date' : ping OK, $i host is up!" |
            mail -s "$i host is up!" $EMAIL

            fi 
        echo "$i-UP!" > $LOG.$i
fi
done

sleep $SECONDS
done

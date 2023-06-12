# Linux-Notes
For finding the IP of the system ---> ifconfig | grep "inet " | grep -Fv 127.0.0.1 | awk '{print $2}'

# Linux-Notes
For finding the IP of the system ---> ifconfig | grep "inet " | grep -Fv 127.0.0.1 | awk '{print $2}'
|Command| Description|
|--------|------------|
|type "linux command"| It is used for finding whether the command is shell built in or residing as the binary in some directory|
|help "linux command"| It is find the info associated with the command, though it works for only shell built in|
|man "linux command"| It is to get info associated with the commands which are not shell built in|
|'$WORD' & "$WORD"|Single quote picks the variable directly by giving no room for expansion and double quote picks the corresponding reference variabe and expand itself on the basis of value corresponding to key. Double and single quote has considerable difference as the first one will print the $WORD directly and second one will look for correspoding value of $WORD.|
|Echo ${WORD}ing|Here due to the introduction of braces, now we can append the other letters as well. Output will scripting as $WORD is pointing to Script.|
|||

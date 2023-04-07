# Low level Design Patterns

## Adapter design Pattern
public class SocketClassAdapterImpl extends Socket implements SocketAdapter
This can be understood in the way that SocketAdapter has all the method which is desirable in the output. 
java.util.Arrays#asList() is the better example. 
https://www.digitalocean.com/community/tutorials/adapter-design-pattern-java

## Facade Design pattern
It is one of the Structural design patterns. Facade design pattern is more like a helper for client applications. its purpose is to provide a single interface rather than multiple interfaces that does the similar kind of jobs. 
Facade design pattern provide a wrapper interface on top of the existing interface to help client application.

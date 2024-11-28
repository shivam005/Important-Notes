# Low level Design Patterns

| Design Pattern | Description |Notes|
| --- | ----------- |-----|
|-----|  CREATIONAL|----|
|  Singleton | The singleton pattern restricts the initialization of a class to ensure that only one instance of the class can be created. |Herein, we create a static instance and we check, If the instance is null then assign it with a newly created object and If it is not null then return it right away.|
|Prototype|Creating a new object instance from another similar instance and then modify according to our requirements (Cloning from prototype)|Herein instead of making object using new keyword, we clone it because calling constructor is a heavy operation. Clone method by default do shallow copy.|
|Factory|The factory pattern takes out the responsibility of instantiating a object from the class to a Factory class.| need to create objects based on some input criteria (At Runtime) or logic without exposing the instantiation logic to the client|
|Abstract Factory|Allows us to create a Factory for factory classes.|In simple term, It is factory of factory. |
|Builder|Creating an object step by step and a method to finally get the object instance.|When some optional paremeters are not to be used at the time of object creation.|
|------|Structural|-------|
|Adapter|Provides an interface between two unrelated entities so that they can work together.||
|Composite|Used when we have to implement a part-whole hierarchy. For example, a diagram made of other pieces such as circle, square, triangle, etc.||
|Proxy|Provide a surrogate or placeholder for another object to control access to it.||
|Flyweight|Caching and reusing object instances, used with immutable objects. For example, string pool.||
|Facade|Creating a wrapper interfaces on top of existing interfaces to help client applications.||
|Bridge|The bridge design pattern is used to decouple the interfaces from implementation and hiding the implementation details from the client program.||
|Decorator|The decorator design pattern is used to modify the functionality of an object at runtime.||
|------------|Behavioral|-----------|
|Strategy|Strategy pattern is used when we have multiple algorithm for a specific task and client decides the actual implementation to be used at runtime.||
|State|State design pattern is used when an Object change it’s behavior based on it’s internal state.||
|Observer|useful when you are interested in the state of an object and want to get notified whenever there is any change.||
|Template Method|used to create a template method stub and defer some of the steps of implementation to the subclasses.||
|Mediator|used to provide a centralized communication medium between different objects in a system.||
|Chain of Responsibility|used to achieve loose coupling in software design where a request from the client is passed to a chain of objects to process them.||
|Command|Command Pattern is used to implement lose coupling in a request-response model.||
|Visitor|Visitor pattern is used when we have to perform an operation on a group of similar kind of Objects.||
|Interpreter|defines a grammatical representation for a language and provides an interpreter to deal with this grammar.||
|Iterator|used to provide a standard way to traverse through a group of Objects.||
|Memento|The memento design pattern is used when we want to save the state of an object so that we can restore later on.||

## Abstract Factory Pattern
It is used to create factorries of factory. Simply, in factory pattern we have got to create multiple classes which implements the method in that interface but here in we create a seperate interface for different factories which is used ultimately. 

## Factory Design Pattern 
It is to be used when the type object which needs to be created, is determined at the runtime on the basis of the paremeter passed. Lets assume that you have a interface which has many implementing class which class needs to be instantiated, would be determined on the basis of the parameter passed. Whatever parameter will be passed, we will return the object of the class by reintantiating it. It is beneficial, when we are need to use different implementation on the basis of the incoming parameter then we can pass it through the factory and can instantiate object on the basis of the parameter.  

```
// Product interface
interface Shape {
    void draw();
}

// Concrete Products
class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Square implements Shape {
    public void draw() {
        System.out.println("Drawing Square");
    }
}

// Factory
class ShapeFactory {
    public Shape getShape(String shapeType) {
        if (shapeType == null) {
            return null;
        }
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("SQUARE")) {
            return new Square();
        }
        return null;
    }
}

// Client
public class FactoryPatternDemo {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        // Get an object of Circle and call its draw method.
        Shape shape1 = shapeFactory.getShape("CIRCLE");
        shape1.draw();

        // Get an object of Square and call its draw method.
        Shape shape2 = shapeFactory.getShape("SQUARE");
        shape2.draw();
    }
}
```

## Builder Design Pattern
Builder Pattern is perfect for constructing complex objects with many optional parameters and ensuring that the object is immutable and consistent after construction.
It allows method chaining and ensures that the fields of the Builder instance are properly set before creating the target object.
Usually, in order to prevent the optional parameter, we have got to create multiple parametrized constructor but this problem can be resolved here by creating a single constructor which would take same instance as parameter and would populate the values initialized.
```
public class BuilderDesignPattern {

    String name;
    String someThingOptional;
    Integer age;

    @Override
    public String toString() {
        return "BuilderDesignPattern{" +
                "name='" + name + '\'' +
                ", someThingOptional='" + someThingOptional + '\'' +
                ", age=" + age +
                '}';
    }

    public BuilderDesignPattern(BuilderDesignPattern builder){
        this.name=builder.name;
        this.age= builder.age;
        this.someThingOptional= builder.someThingOptional;
    }
    public BuilderDesignPattern(){

    }

    public BuilderDesignPattern setname(String name){
        this.name = name;
        return this;
    }

    public BuilderDesignPattern setsomeThingOptional(String someThingOptional){
        this.someThingOptional = someThingOptional;
        return this;
    }

    public BuilderDesignPattern setage(Integer age){
        this.age = age;
        return this;
    }

    public BuilderDesignPattern build(){
        return new BuilderDesignPattern(this);
    }

    public static void main(String[] args) {
        System.out.println( new BuilderDesignPattern().setage(11).setname("name").setsomeThingOptional("optional").build());
        System.out.println( new BuilderDesignPattern().setage(11).setname("name").build());
    }
}

```

## State Design Pattern
Which method(from which class) needs to be invoked would be deciced on the basis of the state of the object. Firstly, we will fix the state of any object to something and each time, method would be invoked on the current state only. Each state would have same number of methods but will have different implementation. Once a method is invoked on a particular state, we will make sure to change the state as well because the consecutive method needs to be invoked on the upcoming state only. 
Example: 
1. Traffic Light System:: RedState, YellowState, GreenState
2. Vending Machine:: NoCoinState, HasCoinState, DispensingState
3. DocumentMaker:: DraftState, ReviewState, ApprovedState, PublishedState
4. Media Player:: PlayingState, PausedState, StoppedState
5. Bank Account:: ActiveState, OverdrawnState, ClosedState
6. Phone Call:: RingingState, ConnectedState, OnHoldState, DisconnectedState
7. Order Processing:: NewOrderState, ProcessingState, ShippedState, DeliveredState, CancelledState
8. ATM Machine:: NoCardState, HasCardState, PinEnteredState, DispensingCashState
9. Printing Machine:: ReadyState, PrintingState, OutOfPaperState, ErrorState
10. Video Game Characte:: IdleState, RunningState, JumpingState, AttackingState
```
public class VendingMachine {
    private VendingMachineState noCoinState;
    private VendingMachineState hasCoinState;
    private VendingMachineState dispensingState;

    private VendingMachineState currentState;

    public VendingMachine() {
        noCoinState = new NoCoinState(this);
        hasCoinState = new HasCoinState(this);
        dispensingState = new DispensingState(this);

        currentState = noCoinState; // initial state
    }

    public void setState(VendingMachineState state) {
        this.currentState = state;
    }

    public void insertCoin() {
        currentState.insertCoin();
    }

    public void ejectCoin() {
        currentState.ejectCoin();
    }

    public void selectProduct() {
        currentState.selectProduct();
    }
}

public interface VendingMachineState {
    void insertCoin();
    void ejectCoin();
    void selectProduct();
    void dispenseProduct();
}
public class NoCoinState implements VendingMachineState {
    private VendingMachine vendingMachine;

    public NoCoinState(VendingMachine vendingMachine) {
        this.vendingMachine = vendingMachine;
    }

    @Override
    public void insertCoin() {
        System.out.println("Coin inserted.");
        vendingMachine.setState(vendingMachine.getHasCoinState());
    }

    @Override
    public void ejectCoin() {
        System.out.println("No coin to eject.");
    }

    @Override
    public void selectProduct() {
        System.out.println("Insert coin first.");
    }

    @Override
    public void dispenseProduct() {
        System.out.println("Insert coin first.");
    }
}

```
## Strategy Design Pattern
We use this design pattern when we realise that the child has duplicate code which should have been present in the parent class but because of design flaw, we are bound to write it into different child. 
Using this design pattern, we create a instance of any strategy (Interface) and selection of implementing class would be done by constructor injection. 
Herein, we create an interface as strategy which would have different implement class as their actual strategy. At the time of use which actual strategy should be used, would be determined by the object created of a particular class and this would be done using constructor injection sort of design. 
Example;
1. Name->PaymentService :: Strategy-> CreditCardPayment, PayPalPayment, BitcoinPayment
2. Sorter:: BubbleSort, QuickSort, MergeSort
3. FileCompressor:: ZipCompression, RarCompression, TarCompression
```
   public interface CompressionStrategy {
    void compress(String file);
}

public class ZipCompression implements CompressionStrategy {
    public void compress(String file) {
        System.out.println("Compressing using ZIP.");
    }
}

public class RarCompression implements CompressionStrategy {
    public void compress(String file) {
        System.out.println("Compressing using RAR.");
    }
}

public class FileCompressor {
    private CompressionStrategy strategy;
    
    public void setCompressionStrategy(CompressionStrategy strategy) {
        this.strategy = strategy;
    }
    
    public void compressFile(String file) {
        strategy.compress(file);
    }
}
public class StrategyPatternDemo {
    public static void main(String[] args) {
        FileCompressor compressor = new FileCompressor();
        // Using ZipCompression strategy
        CompressionStrategy zipCompression = new ZipCompression();
        compressor.setCompressionStrategy(zipCompression);
        compressor.compressFile("file.txt");

        // Changing to RarCompression strategy
        CompressionStrategy rarCompression = new RarCompression();
        compressor.setCompressionStrategy(rarCompression);
        compressor.compressFile("file.txt");
    }
}

```
4. Authenticator :: OAuthAuthentication, LDAPAuthentication, SAMLAuthentication
5. TaxCalculator::
6. RouteCalculator::CarRoute ,BikeRoute, WalkingRoute
7. FileParser :: CSVParser, JSONParser, XMLParser
8. ImageFilter :: BlackAndWhiteFilter, SepiaFilter, BlurFilter
9. NotificationService :: EmailNotification, SMSNotification, PushNotification
10. DiscountService :: PercentageDiscount, BuyOneGetOneFree, FixedDiscount

## Observer Design Pattern
There are two entities in this design pattern: 1. Observable (Has State) 2. Observer. We manage the list of observer (Which could have any number of implementation) and whenever any observer subscribe, we add it to the list. Whenever, we find any difference or change in the observable state. We iterate the list and notify all the observers.  This notification would be triggered from the method(update()) of implementing class of the observer.  

Example;
1. Context-> NewsPublisher :: Observers -> Subscribers (EmailSubscriber, SMSSubscriber, AppSubscriber)
2. Stock :: Brokers, Investors (Brokers and investors get notified when stock prices change)
3. WeatherStation :: DisplayDevices (PhoneDisplay, WindowDisplay)
4. UserAccount :: Followers (Followers get notified when the user posts new content)
5. Button :: EventListeners (ClickListener, HoverListener)
6. ChatRoom :: Users (Users get notified when a new message is posted in the chat room)
7. TrafficLight :: Cars (Cars get notified when the traffic light changes its state (e.g., from red to green))
8. BuildSystem :: (Build agents get notified when there is a new build task to perform)
```
public interface WeatherObserver {
    void update(float temperature, float humidity);
}

public class PhoneDisplay implements WeatherObserver {
    public void update(float temperature, float humidity) {
        System.out.println("Phone display updated: Temp = " + temperature + ", Humidity = " + humidity);
    }
}

public class WeatherStation {
    private List<WeatherObserver> observers = new ArrayList<>();
    private float temperature;
    private float humidity;
    
    public void addObserver(WeatherObserver observer) {
        observers.add(observer);
    }
    
    public void removeObserver(WeatherObserver observer) {
        observers.remove(observer);
    }
    
    public void setMeasurements(float temperature, float humidity) {
        this.temperature = temperature;
        this.humidity = humidity;
        notifyObservers();
    }
    
    private void notifyObservers() {
        for (WeatherObserver observer : observers) {
            observer.update(temperature, humidity);
        }
    }
}
public class Main {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();
        WeatherObserver phoneDisplay = new PhoneDisplay();
        
        weatherStation.addObserver(phoneDisplay);
        weatherStation.setMeasurements(23.5f, 65.0f);
    }
}
```
```
public interface Observer {
    void update(String news);
}

public class EmailSubscriber implements Observer {
    public void update(String news) {
        System.out.println("Email Subscriber: " + news);
    }
}

public class NewsPublisher {
    private List<Observer> subscribers = new ArrayList<>();
    
    public void subscribe(Observer observer) {
        subscribers.add(observer);
    }
    
    public void unsubscribe(Observer observer) {
        subscribers.remove(observer);
    }
    
    public void notifySubscribers(String news) {
        for (Observer subscriber : subscribers) {
            subscriber.update(news);
        }
    }
}
public class Main {
    public static void main(String[] args) {
        NewsPublisher newsPublisher = new NewsPublisher();
        Observer emailSubscriber = new EmailSubscriber();
        
        newsPublisher.subscribe(emailSubscriber);
        newsPublisher.notifySubscribers("Breaking News: Observer pattern in Java!");
    }
}
```
## Chain of Responsibility Design Pattern
1. Technical Support System (Handling support tickets based on severity) :: Level 1 Support, Level 2 Support, Level 3 Support
2. ATM Withdrawal (Dispensing money based on denominations) :: 100-dollar dispenser, 50-dollar dispenser, 20-dollar dispenser
3. Email Filtering :: SpamFilter, FanMailFilter, BusinessMailFilter
4. Request Handling in Web Server ::  AuthenticationHandler, AuthorizationHandler, DataValidationHandler
```
abstract class Logger {
    protected Logger nextLogger;
    
    public void setNextLogger(Logger nextLogger) {
        this.nextLogger = nextLogger;
    }
    
    public abstract void logMessage(String message, int level);
}

class InfoLogger extends Logger {
    public void logMessage(String message, int level) {
        if (level == 1) {
            System.out.println("Info: " + message);
        } else if (nextLogger != null) {
            nextLogger.logMessage(message, level);
        }
    }
}

class DebugLogger extends Logger {
    public void logMessage(String message, int level) {
        if (level == 2) {
            System.out.println("Debug: " + message);
        } else if (nextLogger != null) {
            nextLogger.logMessage(message, level);
        }
    }
}

class ErrorLogger extends Logger {
    public void logMessage(String message, int level) {
        if (level == 3) {
            System.out.println("Error: " + message);
        } else if (nextLogger != null) {
            nextLogger.logMessage(message, level);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Logger infoLogger = new InfoLogger();
        Logger debugLogger = new DebugLogger();
        Logger errorLogger = new ErrorLogger();
        
        infoLogger.setNextLogger(debugLogger);
        debugLogger.setNextLogger(errorLogger);
        
        infoLogger.logMessage("This is a debug message.", 2);
    }
}

```
## Adapter design Pattern
public class SocketClassAdapterImpl extends Socket implements SocketAdapter
This can be understood in the way that SocketAdapter has all the method which is desirable in the output. 
java.util.Arrays#asList() is the better example. 
https://www.digitalocean.com/community/tutorials/adapter-design-pattern-java

## Facade Design pattern
It is one of the Structural design patterns. Facade design pattern is more like a helper for client applications. its purpose is to provide a single interface rather than multiple interfaces that does the similar kind of jobs. 
Facade design pattern provide a wrapper interface on top of the existing interface to help client application.

# SOLID Principles
### Single Responsibility Principle (SRP)
Definition: A class should have only one reason to change, meaning it should have only one responsibility.
Why it matters:
Improves code readability and maintainability.
Avoids coupling unrelated functionality.
```
class Report {
    public void generateReport() {
        // Code to generate report
    }
}

class ReportSaver {
    public void saveToFile(Report report) {
        // Code to save report to a file
    }
}
// Now, each class has a single responsibility.
```
### Open/Closed Principle (OCP)
Definition: Software entities (classes, methods, etc.) should be open for extension but closed for modification.
Why it matters:
Enhances code extensibility.
Reduces the risk of introducing bugs when modifying existing code.
```
abstract class Discount {
    public abstract double calculate(double price);
}

class NewYearDiscount extends Discount {
    public double calculate(double price) {
        return price * 0.10;
    }
}

class BlackFridayDiscount extends Discount {
    public double calculate(double price) {
        return price * 0.20;
    }
}
// Now, you can extend the Discount class without modifying existing code.
```
###  Liskov Substitution Principle (LSP)
Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
```
However, the additional methods in a subclass that aren't part of the parent class's interface can seem like a violation of LSP because:
1. When you treat an object as an instance of its parent class, you will only have access to methods defined in the parent class.
2. Any methods unique to the subclass will not be visible unless you cast the object back to the subclass type.
Technically, it doesn't break the Liskov Substitution Principle because LSP doesn't demand that all features of a subclass are visible when treated as an instance of the parent class. LSP is primarily concerned with ensuring that subclass behavior does not contradict or invalidate the behavior expected from the parent class.
```
### Interface Segregation Principle (ISP)
Definition: A class should not be forced to implement interfaces it does not use.
Why it matters:
Prevents bloated interfaces.
Keeps implementations focused and clear.
```
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Human implements Workable, Eatable {
    public void work() {
        // Human works
    }

    public void eat() {
        // Human eats
    }
}

class Robot implements Workable {
    public void work() {
        // Robot works
    }
}
```
###  Dependency Inversion Principle (DIP)
Definition: High-level modules should not depend on low-level modules. Both should depend on abstractions.
Abstractions should not depend on details. Details should depend on abstractions.
Why it matters:
Reduces tight coupling.
Makes code easier to test and maintain.
```
interface InputDevice {
    void input();
}

class Keyboard implements InputDevice {
    public void input() {
        // Keyboard implementation
    }
}

class Computer {
    private InputDevice inputDevice;

    public Computer(InputDevice inputDevice) {
        this.inputDevice = inputDevice; // Loosely coupled
    }
}
// Here, Computer depends on the InputDevice abstraction, not the Keyboard implementation.
```

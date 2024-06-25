# Low level Design Patterns

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

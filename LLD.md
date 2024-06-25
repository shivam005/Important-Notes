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


## Adapter design Pattern
public class SocketClassAdapterImpl extends Socket implements SocketAdapter
This can be understood in the way that SocketAdapter has all the method which is desirable in the output. 
java.util.Arrays#asList() is the better example. 
https://www.digitalocean.com/community/tutorials/adapter-design-pattern-java

## Facade Design pattern
It is one of the Structural design patterns. Facade design pattern is more like a helper for client applications. its purpose is to provide a single interface rather than multiple interfaces that does the similar kind of jobs. 
Facade design pattern provide a wrapper interface on top of the existing interface to help client application.

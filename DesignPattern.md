# Creational : Object creation
### Factory Method
```
public interface Shape {
    void draw();
}
```
```
public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}

public class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Square");
    }
}
```
```
public class ShapeFactory {

    // Use getShape method to get an object of type Shape
    public Shape getShape(String shapeType) {
        if (shapeType == null) {
            return null;
        }
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("RECTANGLE")) {
            return new Rectangle();
        } else if (shapeType.equalsIgnoreCase("SQUARE")) {
            return new Square();
        }
        return null;
    }
}
```
```
public class FactoryPatternDemo {

    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        // Get an object of Circle and call its draw method.
        Shape shape1 = shapeFactory.getShape("CIRCLE");
        shape1.draw(); // Output: Drawing a Circle

        // Get an object of Rectangle and call its draw method.
        Shape shape2 = shapeFactory.getShape("RECTANGLE");
        shape2.draw(); // Output: Drawing a Rectangle

        // Get an object of Square and call its draw method.
        Shape shape3 = shapeFactory.getShape("SQUARE");
        shape3.draw(); // Output: Drawing a Square
    }
}
```
Purpose: It is used when a class cannot anticipate the class of objects it needs to create, or when a class wants its subclasses to specify the objects it creates.
### Abstract Factory
Purpose: It is used when there is a need to create a suite of related products that should be used together, and when the system needs to be independent of how these objects are created and composed.
```
public interface Shape {
    void draw();
}
```
```
// Normal shape implementations
public class NormalCircle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a normal Circle");
    }
}

public class NormalRectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a normal Rectangle");
    }
}

public class NormalSquare implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a normal Square");
    }
}

// Rounded shape implementations
public class RoundedCircle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rounded Circle");
    }
}

public class RoundedRectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rounded Rectangle");
    }
}

public class RoundedSquare implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rounded Square");
    }
}
```
```
public interface ShapeFactory {
    Shape createCircle();
    Shape createRectangle();
    Shape createSquare();
}
```
```
// Factory for normal shapes
public class NormalShapeFactory implements ShapeFactory {
    @Override
    public Shape createCircle() {
        return new NormalCircle();
    }

    @Override
    public Shape createRectangle() {
        return new NormalRectangle();
    }

    @Override
    public Shape createSquare() {
        return new NormalSquare();
    }
}

// Factory for rounded shapes
public class RoundedShapeFactory implements ShapeFactory {
    @Override
    public Shape createCircle() {
        return new RoundedCircle();
    }

    @Override
    public Shape createRectangle() {
        return new RoundedRectangle();
    }

    @Override
    public Shape createSquare() {
        return new RoundedSquare();
    }
}
```
```
public class AbstractFactoryDemo {

    public static void main(String[] args) {
        // Get shape factory for normal shapes
        ShapeFactory normalFactory = new NormalShapeFactory();
        Shape normalCircle = normalFactory.createCircle();
        Shape normalRectangle = normalFactory.createRectangle();
        Shape normalSquare = normalFactory.createSquare();

        // Draw normal shapes
        normalCircle.draw(); // Output: Drawing a normal Circle
        normalRectangle.draw(); // Output: Drawing a normal Rectangle
        normalSquare.draw(); // Output: Drawing a normal Square

        // Get shape factory for rounded shapes
        ShapeFactory roundedFactory = new RoundedShapeFactory();
        Shape roundedCircle = roundedFactory.createCircle();
        Shape roundedRectangle = roundedFactory.createRectangle();
        Shape roundedSquare = roundedFactory.createSquare();

        // Draw rounded shapes
        roundedCircle.draw(); // Output: Drawing a rounded Circle
        roundedRectangle.draw(); // Output: Drawing a rounded Rectangle
        roundedSquare.draw(); // Output: Drawing a rounded Square
    }
}

```
### Builder 
```
public interface Shape {
    void draw();
}
```
```
public class Circle implements Shape {
    private String color;
    private int borderThickness;

    private Circle(CircleBuilder builder) {
        this.color = builder.color;
        this.borderThickness = builder.borderThickness;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a Circle with color: " + color + " and border thickness: " + borderThickness);
    }

    // Builder for Circle
    public static class CircleBuilder {
        private String color;
        private int borderThickness;

        public CircleBuilder setColor(String color) {
            this.color = color;
            return this;
        }

        public CircleBuilder setBorderThickness(int borderThickness) {
            this.borderThickness = borderThickness;
            return this;
        }

        public Circle build() {
            return new Circle(this);
        }
    }
}

public class Rectangle implements Shape {
    private String color;
    private int borderThickness;

    private Rectangle(RectangleBuilder builder) {
        this.color = builder.color;
        this.borderThickness = builder.borderThickness;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle with color: " + color + " and border thickness: " + borderThickness);
    }

    // Builder for Rectangle
    public static class RectangleBuilder {
        private String color;
        private int borderThickness;

        public RectangleBuilder setColor(String color) {
            this.color = color;
            return this;
        }

        public RectangleBuilder setBorderThickness(int borderThickness) {
            this.borderThickness = borderThickness;
            return this;
        }

        public Rectangle build() {
            return new Rectangle(this);
        }
    }
}
```
```
public class ShapeFactory {
    public Circle.CircleBuilder getCircleBuilder() {
        return new Circle.CircleBuilder();
    }

    public Rectangle.RectangleBuilder getRectangleBuilder() {
        return new Rectangle.RectangleBuilder();
    }
}
```
```
public class BuilderFactoryDemo {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        // Create a Circle using Builder
        Circle circle = shapeFactory.getCircleBuilder()
                .setColor("Red")
                .setBorderThickness(2)
                .build();
        circle.draw(); // Output: Drawing a Circle with color: Red and border thickness: 2

        // Create a Rectangle using Builder
        Rectangle rectangle = shapeFactory.getRectangleBuilder()
                .setColor("Blue")
                .setBorderThickness(3)
                .build();
        rectangle.draw(); // Output: Drawing a Rectangle with color: Blue and border thickness: 3
    }
}
```
### Prototype
When you use super.clone(), it creates a copy of the current object, but the specific class that is instantiated depends on the actual class of the object on which clone() is called. Here’s how it works:

Cloning in Java: When you call super.clone(), it uses the clone() method from the Object class, which creates a shallow copy of the object. The actual class type of the object determines which implementing class is used for the cloning process.

Implementation: If your class overrides the clone() method, you typically call super.clone() within that method. The object returned by super.clone() is of the same type as the object that called the method. This means that if you have a subclass that overrides clone(), it will create an instance of that subclass.
```
public interface Shape extends Cloneable {
    Shape clone();
    void draw();
}
```
```
public class Circle implements Shape {
    private String color;
    private int radius;

    public Circle(String color, int radius) {
        this.color = color;
        this.radius = radius;
    }

    @Override
    public Circle clone() {
        return new Circle(this.color, this.radius);
    }

    @Override
    public void draw() {
        System.out.println("Drawing a Circle with color: " + color + " and radius: " + radius);
    }

    // Getters and setters for color and radius can be added if needed
}

public class Rectangle implements Shape {
    private String color;
    private int width;
    private int height;

    public Rectangle(String color, int width, int height) {
        this.color = color;
        this.width = width;
        this.height = height;
    }

    @Override
    public Rectangle clone() {
        return new Rectangle(this.color, this.width, this.height);
    }

    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle with color: " + color + " and dimensions: " + width + "x" + height);
    }

    // Getters and setters for color, width, and height can be added if needed
}
```
```
public class PrototypeDemo {
    public static void main(String[] args) {
        // Create original objects
        Circle originalCircle = new Circle("Red", 10);
        Rectangle originalRectangle = new Rectangle("Blue", 20, 30);

        // Clone the objects
        Circle clonedCircle = originalCircle.clone();
        Rectangle clonedRectangle = originalRectangle.clone();

        // Draw the original and cloned objects
        originalCircle.draw();    // Output: Drawing a Circle with color: Red and radius: 10
        clonedCircle.draw();      // Output: Drawing a Circle with color: Red and radius: 10

        originalRectangle.draw(); // Output: Drawing a Rectangle with color: Blue and dimensions: 20x30
        clonedRectangle.draw();   // Output: Drawing a Rectangle with color: Blue and dimensions: 20x30
    }
}
```
### Singleton
```
public interface Shape {
    void draw();
}
```
```
public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}
```
```
public class ShapeManager {
    // The single instance of the class
    private static ShapeManager instance;

    // Private constructor to prevent instantiation
    private ShapeManager() {}

    // Method to get the single instance of the class
    public static synchronized  ShapeManager getInstance() {
        if (instance == null) {
            instance = new ShapeManager();
        }
        return instance;
    }

    // Example methods to manage shapes
    public void drawShape(Shape shape) {
        shape.draw();
    }
}
```
```
public class SingletonDemo {
    public static void main(String[] args) {
        // Get the single instance of ShapeManager
        ShapeManager shapeManager = ShapeManager.getInstance();

        // Create shapes
        Shape circle = new Circle();
        Shape rectangle = new Rectangle();

        // Use ShapeManager to draw shapes
        shapeManager.drawShape(circle);    // Output: Drawing a Circle
        shapeManager.drawShape(rectangle); // Output: Drawing a Rectangle
    }
}
```

# Structural : Assembling objects and classes into larger structures
### Adapter
```
public interface Shape {
    void draw();
}
```
```
public class LegacyRectangle {
    public void drawRectangle() {
        System.out.println("Drawing a Rectangle");
    }
}
```
```
public class RectangleAdapter implements Shape {
    private LegacyRectangle legacyRectangle;

    public RectangleAdapter(LegacyRectangle legacyRectangle) {
        this.legacyRectangle = legacyRectangle;
    }

    @Override
    public void draw() {
        legacyRectangle.drawRectangle();
    }
}
```
```
public class AdapterPatternDemo {
    public static void main(String[] args) {
        // Create an instance of LegacyRectangle
        LegacyRectangle legacyRectangle = new LegacyRectangle();

        // Create an adapter for the LegacyRectangle
        Shape rectangleAdapter = new RectangleAdapter(legacyRectangle);

        // Use the adapter to draw the rectangle
        rectangleAdapter.draw(); // Output: Drawing a Rectangle
    }
}
```
### Bridge
```
public interface DrawAPI {
    void drawCircle(int radius, int x, int y);
    void drawRectangle(int width, int height, int x, int y);
}
```
```
public class RedDrawAPI implements DrawAPI {
    @Override
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Drawing Circle[ color: red, radius: " + radius + ", x: " + x + ", y: " + y + " ]");
    }

    @Override
    public void drawRectangle(int width, int height, int x, int y) {
        System.out.println("Drawing Rectangle[ color: red, width: " + width + ", height: " + height + ", x: " + x + ", y: " + y + " ]");
    }
}

public class GreenDrawAPI implements DrawAPI {
    @Override
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Drawing Circle[ color: green, radius: " + radius + ", x: " + x + ", y: " + y + " ]");
    }

    @Override
    public void drawRectangle(int width, int height, int x, int y) {
        System.out.println("Drawing Rectangle[ color: green, width: " + width + ", height: " + height + ", x: " + x + ", y: " + y + " ]");
    }
}
```
```
public abstract class Shape {
    protected DrawAPI drawAPI;

    protected Shape(DrawAPI drawAPI) {
        this.drawAPI = drawAPI;
    }

    public abstract void draw();
}
```
```
public class Circle extends Shape {
    private int x, y, radius;

    public Circle(int x, int y, int radius, DrawAPI drawAPI) {
        super(drawAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    @Override
    public void draw() {
        drawAPI.drawCircle(radius, x, y);
    }
}

public class Rectangle extends Shape {
    private int x, y, width, height;

    public Rectangle(int x, int y, int width, int height, DrawAPI drawAPI) {
        super(drawAPI);
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }

    @Override
    public void draw() {
        drawAPI.drawRectangle(width, height, x, y);
    }
}
```
```
public class BridgePatternDemo {
    public static void main(String[] args) {
        Shape redCircle = new Circle(100, 100, 10, new RedDrawAPI());
        Shape greenCircle = new Circle(100, 100, 10, new GreenDrawAPI());
        Shape redRectangle = new Rectangle(200, 200, 20, 30, new RedDrawAPI());
        Shape greenRectangle = new Rectangle(200, 200, 20, 30, new GreenDrawAPI());

        redCircle.draw();        // Output: Drawing Circle[ color: red, radius: 10, x: 100, y: 100 ]
        greenCircle.draw();      // Output: Drawing Circle[ color: green, radius: 10, x: 100, y: 100 ]
        redRectangle.draw();     // Output: Drawing Rectangle[ color: red, width: 20, height: 30, x: 200, y: 200 ]
        greenRectangle.draw();   // Output: Drawing Rectangle[ color: green, width: 20, height: 30, x: 200, y: 200 ]
    }
}
```
### Composite
### Facade
### Decorator
### Flyweight
### Proxy

# Behavioral : Assignment of responsibilities between objects.
### Chain of Responsibility
### Command
### Iterator
### Mediator
### Memento
### Observer
### State
### Strategy
### Template Method
### Visitor

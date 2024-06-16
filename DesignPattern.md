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
### Prototype
### Singleton

# Structural : Assembling objects and classes into larger structures
### Adapter
### Bridge
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

# test-php-number-1
 test-php-number-1

# Dependency Injection (DI) in PHP

**Dependency Injection (DI)** is a design pattern that deals with how objects or classes obtain their dependencies. Instead of a class creating its own dependencies, they are "injected" from an external source. This promotes loose coupling and makes the code more modular, flexible, and easier to maintain.

## How Dependency Injection Improves Code Architecture:

1. **Loose Coupling**: DI reduces direct dependencies between objects. Instead of a class instantiating its own dependencies, they are provided (injected) by an external source, making the class independent of how those dependencies are created or managed.
   
2. **Testability**: With DI, it's easier to swap real dependencies with mock objects or stubs for unit testing. This is essential for unit tests since classes can be isolated with mock dependencies instead of real ones.

3. **Maintainability**: When dependencies are injected, classes become simpler, with a clear separation of concerns. Changes to a dependency won't require changes in the dependent class, as long as the interface remains the same.

4. **Flexibility**: Different implementations of the same dependency can be injected at runtime, providing greater flexibility in how objects interact.

## How Dependency Injection Works:

In DI, a class does not directly create or manage its dependencies. Instead, these dependencies are provided (injected) into the class via the constructor, setter methods, or an interface. There are three main types of Dependency Injection:
- **Constructor Injection**: Dependencies are injected through the constructor.
- **Setter Injection**: Dependencies are injected via setter methods.
- **Interface Injection**: The class provides an injection method that other objects can call to inject dependencies.

## Example: Implementing Dependency Injection in PHP Without a Framework

Here’s a simple example where the `Car` class depends on the `Engine` class.

### Defining the Classes and Injecting Dependencies

```php
// Engine class (dependency)
class Engine {
    public function start() {
        return "Engine started!";
    }
}

// Car class (depends on Engine)
class Car {
    private $engine;

    // Constructor Injection
    public function __construct(Engine $engine) {
        $this->engine = $engine;
    }

    public function startCar() {
        return $this->engine->start() . " The car is now running.";
    }
}

// Create the Engine object
$engine = new Engine();

// Inject the Engine dependency into the Car object
$car = new Car($engine);

// Call the method
echo $car->startCar();

```

### Benefits of This Approach
1. ***Loose Coupling***: The Car class no longer knows how to create the Engine object. It only knows it needs an Engine to function.
2. ***Testability***: If we want to test the Car class, we can mock the Engine class to isolate the test
```php
class MockEngine extends Engine {
    public function start() {
        return "Mock Engine started!";
    }
}

$mockEngine = new MockEngine();
$car = new Car($mockEngine);

echo $car->startCar();  // "Mock Engine started! The car is now running."

```

3. ***Flexibility***: We can easily swap out the Engine with any other class that implements the same methods. For example, we could inject a TurboEngine or ElectricEngine class without modifying the Car class.

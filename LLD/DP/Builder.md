 - [Definition](#Definition)
 - [# Why Use the Builder Pattern?](#%20Why%20Use%20the%20Builder%20Pattern?)
 - [## Key Principles of the Builder Pattern](##%20Key%20Principles%20of%20the%20Builder%20Pattern)
 - [## Structure of the Builder Pattern](##%20Structure%20of%20the%20Builder%20Pattern)
 - [## Example Implementation in Java](##%20Example%20Implementation%20in%20Java)
 - [## When Should You Use the Builder Pattern?](##%20When%20Should%20You%20Use%20the%20Builder%20Pattern?)


<a name="Definition"></a>
# Definition
	

> The Builder Design Pattern is a creational pattern that provides a
> flexible way to construct complex objects step by step. Instead of
> creating an object in one go using a constructor, the Builder pattern
> allows controlled and customizable object creation.

# Why Use the Builder Pattern?
	

> When an object has a large number of optional parameters or complex
> construction logic, using constructors or setter methods can make the
> code difficult to manage. The Builder pattern simplifies object
> creation by providing a dedicated builder class.

		

## Key Principles of the Builder Pattern

 - Encapsulation of Object Construction- The object construction logic is separated from its representation, making it easy to modify or extend.
 - Step-by-Step Object Creation- The Builder pattern allows constructing objects in a controlled, step-by-step manner.
 - Immutability- Once built, the object remains immutable (i.e., cannot be changed), ensuring thread safety and reliability.

## Structure of the Builder Pattern

	

> It involves the following components:

 - Product (Main Object to be built)- The complex object whose creation is controlled by the builder.
 - Builder (Abstract Interface or Base Builder Class)- Defines the steps required for building the object.
 - Concrete Builder- Implements the builder interface and defines the actual construction process.
 - Director (Optional)- Controls the construction process and defines the order in which the object is built.

## Example Implementation in Java

	Here’s a basic example using the Builder pattern:
		
    // Product class
    		class Car {
    			private String engine;
    			private int wheels;
    			private String color;
    
    			// Private constructor to enforce object creation via Builder
    			private Car(CarBuilder builder) {
    				this.engine = builder.engine;
    				this.wheels = builder.wheels;
    				this.color = builder.color;
    			}
    
    			@Override
    			public String toString() {
    				return "Car [Engine=" + engine + ", Wheels=" + wheels + ", Color=" + color + "]";
    			}
    
    			// Builder Class
    			static class CarBuilder {
    				private String engine;
    				private int wheels;
    				private String color;
    
    				public CarBuilder setEngine(String engine) {
    					this.engine = engine;
    					return this;
    				}
    
    				public CarBuilder setWheels(int wheels) {
    					this.wheels = wheels;
    					return this;
    				}
    
    				public CarBuilder setColor(String color) {
    					this.color = color;
    					return this;
    				}
    
    				public Car build() {
    					return new Car(this);
    				}
    			}
    		}
    
    		// Usage
    		public class BuilderPatternExample {
    			public static void main(String[] args) {
    				Car car = new Car.CarBuilder()
    								.setEngine("V8")
    								.setWheels(4)
    								.setColor("Red")
    								.build();
    
    				System.out.println(car);
    			}
    		}

## When Should You Use the Builder Pattern?

 - When a class has many optional parameters.
 -  When object construction requires multiple steps or validations.
 - When you want to enforce immutable objects.

> 	The Builder pattern is widely used in real-world applications,
> including frameworks like Lombok in Java, where annotation-based
> builders simplify object creation.

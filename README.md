

# The whole overview of SOLID principles

SOLID principles are some set of rules and best practices for designing any solution in the developmental sector in Object-Oriented programming. These principles were first introduced by Robert C. martin in one his reearch paper and the acronym "SOLID" was first mentioned by Michael Feathers.

## Why need SOLID?
 - To write maintainable codes.
 - Easier to understand for any developers.
 - Increses flexibility and reduce complexities.
 - To maintain less complex architecture of solution.

## SOLID definition
The term SOLID holds for 5 different design principles:
- **S**ingle Responsibility principle.
- **O**pen-Closed principle.
- **L**iscov Substitution principle.
- **I**nterface Segregation principle.
- **D**ependency Inversion principle.

Lets discuss about these one by one:
## Single Responsibility Principle (*SRP*)
This principle states that one class should have only one reason to change. It means we should consider a class should have only one responsibility. To state this principle more precisely:
- **Testing capabilities:** If a class has only one type of activities, then it is much more easier for any developer to perform some unit testing regarding to fix some that particular type of bugs. Like: to fix some database connection or user authentication related issues, we only need to focus on *DatabaseConnector* or *UserAuthenticationManager* classes.
- **Loose Coupling:** By separating the functional components of each class, we can maintain the loose coupling between the classes.
- **Structural Design:** By following the SRP principle, the overall structure of a class remains small and much readable.

Example: Assume, we have a class named *Connector*. The responsibilities of this class is to connect any type of connection according to our need. It can connect *Database*, *Laptop* and *Mobile*. 


![Untitled Diagram (9)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/fd7372f6-ae00-4225-aa58-788747880d22)



 ```java
 class Connector {
	String connectorName;
	void connectDatabase(String connectionType) {
		System.out.println(connectionType + " connected!");
	}
	void connectMobile(String connectionType) {
		System.out.println(connectionType + " connected!");
	}
	void connectLaptop(String connectionType) {
		System.out.println(connectionType + " connected!");
	}
}
public  class SRP {
	public  static  void main(String args[]) {
		Connector connector = new Connector();
		
		connector.connectDatabase("MongoDB");
		connector.connectLaptop("Laptop");
		connector.connectMobile("Mobile");
	}
}
 ```
 ```
 MongoDB connected!
Laptop connected!
Mobile connected!
 ```
 Here we can see the *Connector* class have 3 different type of responsibilities. And it violates the *Single responsibility Principle*. So how can we fix this ?
We can have a base *Connector* class to setup any kind of connections. And this *Connector* class can have 3 different child classes to perform the above 3 different activities. Consider the following code:

![Untitled Diagram (10)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/5a826faa-e2f0-4836-861c-daade1d7811c)


```java
abstract  class Connector {
	String connectorType;
	abstract  void connect();
}
class DatabaseConnector extends Connector {
	DatabaseConnector(String type) {
		this.connectorType = type;
	}
	@Override
	void connect() {
		System.out.println(connectorType + " connected!");
	}
}
class LaptopConnector extends Connector {
	LaptopConnector(String type) {
	this.connectorType = type;
}
	@Override
	void connect() {
		System.out.println(connectorType + " connected!");
	}
}
class MobileConnector extends Connector {
	MobileConnector(String type) {
		this.connectorType = type;
	}
	@Override
	void connect() {
		System.out.println(connectorType + " connected!");
	}
}
public  class SRP {
	public  static  void main(String args[]) {
		Connector db_connector = new DatabaseConnector("MongoDB");
		Connector laptop_Connector = new DatabaseConnector("Laptop");
		Connector mobile_Connector = new DatabaseConnector("Mobile");

		db_connector.connect();
		laptop_Connector.connect();
		mobile_Connector.connect();
	}
}
```
 ```
 MongoDB connected!
Laptop connected!
Mobile connected!
 ```

## Open-Closed Principle (*OCP*)

This principle states that *Classes should be open for extension and closed for modification*. basically, what does this principle actually mean? <br/>
It means we should be able to add new functionality without touching the existing code for the class. Because whenever we modify the existing code, we are at the risk of having bugs. So we should avoid touching the tested and reliable (mostly) production code if possible.
We can apply such technique by using abstract classes and interfaces. The previous example that I've explained for maintaining SRP principle, it also maintains OCP principle. If we need to add a different type of *Connector*, for example: **WiFiConnector**,  then we can just simply extend the parent **Connector** class and provide the own implementation for *connect()* method for the newly created connector. 

![Untitled Diagram (22)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/3b640eab-8813-4a18-b0b2-dbb48c4cb43f)


Let's discuss about another example about different types of shapes. We have implementations for shapes like: *Line*, *Ractangle*, *Circle* classes. If we need another new *Random* type shape, we just have to implement the *Shape* interface and provide all implementations for this random shape. By following the OCP principle, we do not need to modify our existing classes. <br/>

#### OCP violation:

![Untitled Diagram (40)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/1878bcf3-dcd3-4586-9c64-dffb884b6dae)


We know that every shapre has its own area to measure. So the *area* is a common property for every shape. If we need to add this property to our concrete ```Shape``` interface, then it will be strictly violate our open-close principle, as we are modifing our existing base code.  


## Liskov Substitution Principle (*LSP*)
Liskov substitution principle states that *parent classes should be easily substituted with their child classes*. It means that, given that class Y is a subclass of class X, we should be able to pass an object of class Y to any method that expects an object of class X and the method should not give any weird output in that case. <br/>
Suppose, we have a *Guiter* class as a parent class which has some basic properties & functionalities that all types of guiter have. Now we three different types of guiter that have the same properties but with different implementation of their own. 

![Untitled Diagram (11)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/f93536e4-dabe-49a0-a938-b395f90ca436)


```java
class Guiter {
	String type;
	void cableConnection() {
		System.out.println("Normal cable connection for all guiter.");
	}
}
class BassGuiter extends Guiter {
	BassGuiter(String type) {
		this.type = type;
	}
	void sound() {
		System.out.println(type + " has Metalic sound.");
	}
}
class AcousticGuiter extends Guiter {
	AcousticGuiter(String type) {
		this.type = type;
	}
	void cableConnection() {
		System.out.println(type + " has special cable connection.");
	}
}
public  class LSP {
	public  static  void main(String args[]) {
		Guiter bassGuiter = new BassGuiter("BassGuiter");
		Guiter acoustic = new AcousticGuiter("Acoustic Guiter");

		bassGuiter.sound();
		acoustic.cableConnection();
	}
}
```
Our above example can violate LSP in one particular scenerio. Let's discuss about it: <br/>

![Untitled Diagram (19)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/680cdf71-c028-4911-9d30-b93fbd8af143)


We all know about Ukulele, which is also a special type of guiter. Though we have defined all guiter will have a cable connection, but in ukulele, there is no cable connecting port to connect. By inheriting the Guiter class, Ukulele will inherit the cableConnection() method forcedfully, which is irrelevant for this class. Thus this situation violates the Liskov substitution principle. So, we can redesign our Guiter class like this:

![Untitled Diagram (21)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/8919e355-e93a-4e1d-9193-dfe87a2faa72)


## Interface Segregation Principle (*ISP*)
Segregation means to separate a particular thing, hence interface segregation is about separating the interfaces. This principle simply states that an interface should not be forced to have such properties that are irrelevant to it.
Let's see an example:

![Untitled Diagram (41)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/4caccda9-4723-46c2-a8b6-1e1e80fbad84)


```java
public interface ParkingArea {
	void parkCar();		// Decrease empty spot count by 1
	void getCapacity();	// Returns car capacity to park
	double calculateCost(Car car); // Calculates cost for a CAR object 
}
```
If we have another type of *FreeParkingArea* which implements the *ParkingArea* interface, 
```java
class FreeParkingArea implements ParkingArea{
	void parkCar();	// Decrease empty spot count by 1
	void getCapacity();	// Returns car capacity to park
	double calculateCost(Car car); return 0;	 
}
```
Here we can see from the name that *FreeParkingArea* class is totally free for any types of vehicles to park. But it is forced to implement the *calculateCost()* method, which is irrelevant for this type of parking. So we can separate this interface and redesign our code as follows:

![Untitled Diagram (12)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/d5a91f6e-a768-4495-a32b-32d46029ee09)


```java
interface ParkingArea{
	void parkCar();
	void getCapacity();
}
interface PaidParkingArea extends ParkingArea{
	void parkCar();
	void getCapacity();
	double calculateCost(Car car);
}
interface FreeParkingArea extends ParkingArea{
	void parkCar();
	void getCapacity();
}
```
As we have separated our parking area, now any type of paid area class can implement the *PainparkingArea* interface and any free parking type class can implement the *FreeParkingArea* interface.


## Dependency Inversion Principle (*DIP*)
Sometimes people get confused about this principle. But following this principle is pretty much smart choice. However, the statement for this principle is: *Higher level module should not depend on lower level module, but they should depend on abstractions.*

![Dependency-Inverstion](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/8123015f-8e26-4299-b900-b2769f17437b)

> *[image source](http://www.aspbucket.com/2018/11/dependency-inversion-principle.html)*

Lets describe this confusion with a proper example:
Suppose we want to setup a database connection for our system and the system is heavily dependent on only one type of connection setup. Let's say, we have a setup for *MySQL* database connection for our system. What if we need to change all the connection setup regarding to this database connection! <br/>
As a solution for this type of scenery, we can use an abstract layer or interface where we can define all types of database connections and can use it based on our needs. Thus adding an abstract layer can save our system from disaster. 


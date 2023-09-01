
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


## Open-Closed Principle (*OCP*)

This principle states that **Classes should be open for extension and closed for modification**. basically, what does this principle actually mean? <br/>
It means we should be able to add new functionality without touching the existing code for the class. Because whenever we modify the existing code, we are at the risk of having bugs. So we should avoid touching the tested and reliable (mostly) production code if possible.
We can apply such technique by using abstract classes and interfaces. The previous example that I've explained for maintaining SRP principle, it also maintains OCP principle. If we need to add a different type of *Connector*, for example: **WiFiConnector**,  then we can just simply extend the parent **Connector** class and provide the own implementation for *connect()* method for the newly created connector. 

![Untitled Diagram (22)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/3b640eab-8813-4a18-b0b2-dbb48c4cb43f)


Let's discuss about another example about different types of shapes. We have implementations for shapes like: *Line*, *Ractangle*, *Circle* classes. If we need another new *Random* type shape, we just have to implement the *Shape* interface and provide all implementations for this random shape. By following the OCP principle, we do not need to modify our existing classes. <br/>

#### OCP violation:

![Untitled Diagram (40)](https://github.com/Asibul-40/SOLID-principle-overview/assets/77221075/1878bcf3-dcd3-4586-9c64-dffb884b6dae)


We know that every shapre has its own area to measure. So the *area* is a common property for every shape. If we need to add this property to our concrete ```Shape``` interface, then it will be strictly violate our open-close principle, as we are modifing our existing base code.  

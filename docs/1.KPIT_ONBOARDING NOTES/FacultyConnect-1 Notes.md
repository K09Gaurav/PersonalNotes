---
tags:
  - kpit
---
-
Focus areas
----------------

1) Object Oriented Programming
        -> Understanding Java programming fundamentals
        -> Compiling, debugging, utilizing extensions for Java in VS Code
        -> Pillars of OOP
                -> Encapsulation
                -> Abstraction
                -> Inheritance
                -> Polymorphism
        -> Understanding how 2 types can be related to each other
            -> Generalization & Specialization
                "EvCar is a type of Car"

	IS A relationship: inheritance
            
	-> Association: 2 classes are related to each other in terms of accessing each others operations/resources

	e.g: operations class is associated with Vehicle (unidirectional association)

            
	-> Composition: 2 classes (A,B)are related such that
			a) A class object controls the life of B class object. When A is destroyed. B is also destroyed.
			b) B class object cannot exist on its own.

			1               1
	Savings Account: ---> Debit Card


	-> Aggregation : 2 classes (A,B)are related such that

	a) A class will not control life of class B instance.
		b) B class instance can exist independently of A class instance. We should also be able to destroy A class instance without necessarily deleting class B instance

	Organization and its employees



-> Understanding static & non-static methods, constructor chaining, toString for representation



Misconception

a) An object oriented programming language should have the concept of class & object

Reality: 3 things that make a language object oriented
                i) There should be a way to make a blueprint/template/format for data
                ii) Instantiate/create units of data based on the specified format
                iii) Mechanism of message passing between instances/units of data


                obj1    ---------------> obj2 

                a functionality called display can be invoked on obj2 by obj1


b)  Misconception: All Pillars of OOP: Abstraction, Polymorphism, Encapsulation, Inheritance are mandatory
Reality: Pillars are just guidelines for writing better code, not a mandate
example: Go programming does not have Inheritance mechanism

c) Misconception: Encapsulation and Data binding are the same

reality: Data binding is one of the requirement in Encapsulation. 

Encapsulation is actually hiding implementation details from the users by exposing only required methods for the object and not requiring users to understand backgroun details on how objects are created


d) Misconception: One can only learn a single language effectively. Learning multiple is not possible

Reality: Most projects are built by incorporating features from multiple libraries/frameworks/languages

#kpit
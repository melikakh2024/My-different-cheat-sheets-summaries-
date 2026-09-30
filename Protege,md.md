# Protege 
The goal in this tutorial is to make learning Protégé and OWL easier and faster. 
###  Note:
Try to avoid thinking in terms of databases or SQL.
Semantic Web is a different way of modeling knowledge.
### This world is mainly built on:
- Classes (concepts like Pizza, Person)
- Properties (relationships like hasTopping, enrolledIn)
- Individuals (real examples like Pizza1, Ali)
- Restrictions (rules that define class membership)
### Note:    
Machines do not understand meaning like humans do.  
What is obvious for humans must be explicitly defined for machines.  
If you want the machine to reason correctly, you must describe everything clearly using classes, properties,and restrictions.  


-------------------------------------------------------------------
## Building an OWL ontology:
My goal is to understand ontology concepts through several examples , which is a familiar example for everyone. I will provide  explanation before each example, such as the goal and the components used.
### Example1:
Running Protégé for the first time usually shows available plugins. If you choose “Not now”, you can install or manage them later through File > Check Plugins.
### IRI:  
Every ontology must have an IRI (Internationalized Resource Identifier), which acts as its unique identifier.
This is similar to a primary key in a database.
In Protégé, the system automatically generates IRIs for other components based on the ontology IRI.

-------------------------------------------------------------------------------------------------------------------------------------------------
### Create classes: Pizza, PizzaTopping, and PizzaBase:
 I.e:class is main concept in Ontology , indeed, Classes are the main groups in a scenario that contain several individuals.They help the machine classify and organize information.
#### Make Pizza, PizzaTopping, and PizzaBase disjoint from each other 
 I.e:avoid redundancy in individuals.By default, classes in OWL can overlap, which may lead to empty or inconsistent intersections.
###  Create Class Hierarchy
 I.e:it is alternative way of creating class , so faster and easier instead of choosing several SubClasses
Tools > Create New Hierarchy 

------------------------------------------------------------------------------------------------------------------------------------------------
### Create some properties:
#### OWL Properties

I.e: defining how individuals are connected and described. there are 3 kinds of property (Object Properties, Data properties ,Annotation Properties)
Note : differences between them ::
#### Object Property:
It defines a relation between individuals.
Although we describe domain and range using classes, the actual relationship happens between individuals of those classes.
Domain and range:
#### Domain: the class of the subject (left side)
#### Range: the class of the object (right side)
They help the reasoner check consistency and detect errors, but they are not mandatory.


--------------------------------------------------------------------------------------------------------------------------------
#### Data Property:
It defines a relation between an individual and a literal value (such as number or text).
Example:
Pizza1 hasCalories 300
Left side: individual  
Right side: value (datatype)
#### Annotation Property:
Annotation properties are used for metadata (labels, comments, descriptions).
They can be applied to classes, properties, or individuals.
They are not used in reasoning and do not affect inference.
They only help humans understand the ontology better.
##### For those familiar with the Entity-Relationship model, OWL object properties are similar to relations and data properties are similar to attributes

#### Create some inverse properties
Making an inverse property is not mandatory, but if you define it, it is better to follow a naming convention in OWL such as hasX and isXOf.
For example: Michael hasPet Garfield, and Garfield isPetOf Michael.
#### Click on the Add icon (+) next to Inverse Of in the Description view

#### OWL Object Property Characteristics
###### Functional Properties
If we define a property as functional, it means one individual can have at most one value for that property.
###### E.g, if hasIngredient is functional and we define:
pizza1 hasIngredient tuna
pizza1 hasIngredient beef
the reasoner may infer that tuna and beef are the same individual, unless they are explicitly defined as different individuals.
A functional property is equivalent to a property with a cardinality restriction that says it has a maximum of 1 value
###### inverse Functional Properties
Inverse functional means that the inverse of a property is functional.
First, you should define your properties and explicitly declare their inverse. Then the system can infer that the inverse property can have at most one value for each individual
###### Transitive Properties
###### Symmetric and Asymmetric Properties
symmetric property is its own inverse.
An Asymmetric property is a property that can never have symmetric values.
#### Reflexive and Irreflexive Properties  

######  Property characteristics make ontology easier by letting the system infer information automatically and reducing manual work.
#### Domain & Range in OWL
Domain and Range are optional in OWL properties
But defining them is highly recommended
##### Why define them?
They help detect modeling mistakes early
They prevent errors at runtime
They improve data consistency
##### Meaning
Domain = the class that uses the property
Range = the class or datatype that the property points to
##### Types of properties
Object Property → connects Class to Class
Data Property → connects Class to Data value (e.g. xsd:integer)
OWL object property = a set of ordered pairs (binary relation) , set of (subject, object),, ٍE.g: hasTopping(Pizza1, Cheese) ,hasTopping(Pizza2, Tomato),

 You can define more than one class as the domain or range of a property. However, the result is the intersection of those classes, not the union.  

the main goal of domain and range is to infer better.

---------------------------------------------------------------------------------------------------------------
###### Describing and Defining Classes(It is the core of OWL) .
This part is one of the most important concepts in ontology modeling.  
#### we have 3 kinds of class : primitive class and defined class and Anonymous classes.
After defining properties, we can use them to define classes.
First, it is important to understand restrictions and class conditions. You can imagine each class as a “box”, where members must satisfy specific criteria.
In Protégé, class conditions are mainly defined using two tabs:
Equivalent To uses for making defined class 
SubClass Of uses for making primitive class 
### Difference between Equivalent To and SubClass Of
#### Equivalent To 
Used when the definition is necessary and sufficient
It creates a two-way meaning
Allows automatic classification by reasoner
#### Use it when:
The class definition is complete and exact
You want the reasoner to infer class membership
The class is logically defined (deterministic)
#### SubClass Of
Used when conditions are only necessary (not sufficient)
It defines constraints, not full definition
Classification is more open
#### Use it when:
The class is not fully defined
You only want to restrict members
You do not want automatic full classification
##### Simple idea:
Equivalent To = full definition (A ⇔ B)
SubClass Of = partial rule (A ⇒ B)
##### Key intuition:
Equivalent To is used when the class can be automatically inferred by the reasoner.  
SubClass Of is used when you only define constraints, not full identity.  
#### Note: We understand that each class contains members (individuals). The criteria for class membership are defined using property restrictions.  
At first, this concept may seem confusing, but it becomes clear that individuals are defined through restrictions on relationships (properties).  
In Protégé, restrictions can be added using the “+” button in either the SubClass Of or Equivalent To tabs. This opens a window that includes different tabs such as:  
Data Property Restrictions  
Object Property Restrictions  
Class Expression Editor  
These tools are essential at this stage of modeling. In fact, they all represent the same underlying logical result.  
Object Property and Data Property panels provide a graphical UI for defining restrictions, while the Class Expression Editor allows users to define restrictions explicitly using OWL expressions.  
#### E.g:
The class of individuals with at least one hasChild relation.  
· The class of individuals with 2 or more hasChild relations.  
· The class of individuals that have at least one hasTopping relationship to individuals that are members of MozzarellaTopping.   
– i.e. the class of things that have at least a mozzarella topping.   
· The class of individuals that are Pizzas and only have hasTopping relations to instances of the
class VegetableTopping (i.e., VegetarianPizza).

##### Goal of restrictions:
we have 3 kinds of restrictions : quantifier(existential , universal)  and cardinality and hasvalue 
Goal of restrictions:  
The goal of restrictions is to define the members of a class based on relationships between individuals.  
Existential restriction (some)
##### Individuals belong to a class if they have at least one relationship with an instance of a given class.  
👉 This means:  
There exists at least one related individual.  
Example:  
hasTopping some VegetableTopping  
✔ Interpretation:  
An individual is in the class if it has at least one vegetable topping.  
🧠 Important note:  
This is a class-level definition, but in runtime it refers to relationships between individuals.  
🧠 Universal restriction (only)  
Individuals belong to a class if all their relationships via a property are only with instances of a given class.  
Example:  
hasTopping only VegetableTopping  
✔ Interpretation:  
If the individual has toppings, all of them must be vegetable toppings.  
🚨 Common mistake (important)  
❌ “only means the class does not exist without that restriction”  
✔ This is wrong.  
👉 Correct idea:  
only does NOT require existence  
it only restricts possible values if they exist  
🍕 Example clarification:  
A pizza with no toppings at all still satisfies:  
hasTopping only VegetableTopping  
### Add a restriction to Pizza that specifies a Pizza must have a PizzaBase  
Select the Object restriction creator. This tab has the Restricted property on the left and the Restriction filler on the right.  
Expand the property hierarchy on the left and select hasBase as the property to restrict. Then in the
Restriction filler on the right select the class PizzaBase. Finally, the Restriction type at the bottom should be set to Some (existential)  

note :: Annotation properties are mainly used for metadata and documentation. They are not intended for reasoning or logical inference  by the reasoner.    


####  Create AmericanaPizza by Cloning MargheritaPizza and Adding Additional Restrictions  

if you need to create  one class similar to other class with extra property , it is better to use Edit>Duplicate selected class     
Reasoner detects logically impossible classes and maps them to owl:Nothing.  
Important note: With primitive classes, we only define constraints, not a complete definition of the class.  
“SubClass Of” expresses a necessary condition, but it is neither sufficient nor a two-way definition.  

----------------------------------
### Simple Rule:  
If a concept has one dimension → use subClass  
If a concept has two or more dimensions → use separate classes + properties  
If a concept is just a raw value with no attributes and no relationships → Data Property   
If a concept has its own attributes or relationships → Class   
#### questions for detection class and subclass :  

✅"Does it have its own attributes?"  
✅"Does it have relationships with other concepts?"  
✅"Can it exist independently  
Quick Test :  
Ask yourself:  
✅"Can one Room be BOTH Deluxe AND Single at the same time?"  
If YES → two dimensions → separate classes + properties   
✅"Can one animal be BOTH Mammal  AND Reptile"  
If NO → one dimension → subClass 

--------------------------------------
#### questions for detection Data Property: 

✅"Is it a raw value like number, text, date, time?"  
✅"Does it have NO relationships with other concepts?"  
✅"Does it have NO attributes of its own?"  
Yes → Data Property   

--------------------------------------------------


Ask: "Does this concept have its own attributes?"  
Example  
ContactAddress has a street, city, postal code → it has its own attributes → it is a Class, not just a data property  
Compare  
hasName just holds a string value → it is a Data Property 

-----------------------------------
🎯 Step 2 — Object Property Characteristics  
Functional — each subject can have at most one value for this property.  
Diagnostic question: "Can one X have more than one Y?"  
Yes →  NOT Functional.    
Hotel offers SwimmingPool and Hotel offers Golf — one hotel, many activities.  
No → Functional. Room hasCategory Deluxe — a room belongs to exactly one category.  

-------------------------

All questions applied to one property, step by step:  
| Question | Answer | Result |
|----------|--------|---------|
| Q1 | Can one Room have more than one Category? No | Functional |
| Q2 | Can two different Rooms share the same Category? Yes | NOT Inverse Functional |
| Q3 | If Room_101 hasCategory Deluxe, does Deluxe hasCategory Room_101? No | NOT Symmetric |
| Q4 | Can Deluxe hasCategory Room_101 ever be valid? No | Asymmetric |
| Q5 | If Room hasCategory Deluxe, and Deluxe hasCategory ??? Chain breaks | NOT Transitive |
| Q6 | Can a Room be its own Category? No | Irreflexive |
| Q7 | Does the reverse direction make sense? Yes | isCategoryOf |
| Q8 | Is hasCategory a specific version of a broader property? Yes | subPropertyOf hasFeature |
| Q9 | What is always on the left? On the right? | Room → RoomCategory |


| Characteristic | Diagnostic Question | NO Means |
|---------------|---------------------|----------|
| Functional | Can one subject have more than one value? | Functional |
| Inverse Functional | Can two subjects share the same value? | Inverse Functional |
| Symmetric | If A→B, does B→A hold? | Asymmetric |
| Transitive | Does A→B→C imply A→C? | NOT Transitive |
| Reflexive | Can X relate to itself? | Irreflexive  




#### The simple rule for Symmetric  
Symmetric only makes sense when both sides are the same kind of thing.  
TRUE:  
Hotel isNearTo Sight — both are locations, so the reverse also makes sense: Sight isNearTo Hotel  
False:  
Event hasContactAddress Address — an Address cannot "have contact address" an Event. They are fundamentally different kinds of things.  
Quick test: read the property backwards. If it still makes sense in the real world, it might be symmetric. If it sounds absurd, it is NOT symmetric.  

----------------------------------------------------
#### The simple rule for Inverseof:  
Question to ask: "Does this property have a meaningful reverse direction?"  

If A → B via property P, then B → A via the inverse property Q. Both directions must be meaningful in the domain.  
Hotel --offers--> Activity  
Activity --isOfferedBy--> Hotel  

Another  
hasCategory and isCategoryOf — "Deluxe isCategoryOf Room_101" is perfectly meaningful, so we create the inverse.  
Always write both sides when you declare inverseOf:  

hasCategory inverseOf: isCategoryOf  
isCategoryOf inverseOf: hasCategory  

-------------------------------------------------
#### The simple rule for equivalentProperty  
Question to ask: "Is there another property with exactly the same meaning?"  

Example  
offers ≡ provides — two properties that mean the exact same thing. Every triple using one also holds for the other.  
Warning  
This is rarely needed in a single ontology. You mainly use it when merging two ontologies from different sources that happen to model the same relationship with different names. 

----------------------------------------------------------------------------
#### The simple rule for subPropertyOf  
Question to ask: "Is this property a more specific version of a broader property?"  

Analogy  
Just like subClassOf for classes — if A subPropertyOf B, then every triple using A is also a triple using B.  
hasCategory subPropertyOf hasFeature  
hasSize subPropertyOf hasFeature  
Meaning  
If Room_101 hasCategory Deluxe, then the reasoner can automatically infer Room_101 hasFeature Deluxe — because category is a type of feature. 

-------------------------------------------------------------
#### domain  
Question to ask: "What class is always on the LEFT side of this property?"  
Example  
hasCategory domain: Room — anything that uses hasCategory must be a Room. The reasoner will infer it is a Room even if you never stated it explicitly.  
Caution   
Domain is a logical constraint, not just documentation. If you accidentally write Hotel hasCategory Deluxe, OWL will infer Hotel is a Room — probably not what you intended.  

----------------------------------------------------------------------------
#### range  
Question to ask: "What class or datatype is always on the RIGHT side?"  

Object  
hasCategory range: RoomCategory — the value must be an individual of class RoomCategory  
Datatype  
hasOpeningTime range: xsd:time — the value must be an XML time literal like "08:00:00"^^xsd:time  
Domain = left side (subject). Range = right side (object). Think of a triple as: [domain] --property--> [range]  

-------------------------------------------------------------------
#### disjointWith (property)  
Question to ask: "Can these two properties ever share the same subject AND object simultaneously?"  

Example  
hasOpeningTime disjointWith hasClosingTime — a specific time value cannot be both the opening time and closing time of the same entity. The two properties can never hold with the same pair.  
Another  
isParentOf disjointWith isChildOf — if A is the parent of B, then A cannot simultaneously be the child of B.  

----------------------------------------------------------------------------
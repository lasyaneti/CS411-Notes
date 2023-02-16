# Conceptual Database Design (ER/UML)

## Symbols in Entity-Relationship Diagrams
- ENTITY SET represented by rectangle
- RELATIONSHIP SET represented by diamond 
- ATTRIBUTE NAME represented by circe 

## Definitions 
- **Entity**: real world objects with set of attributes 
- **Entity set**: collection of similar entities 
- **Relationship**: association between 2 or more entities 
- **Relationship set**: collection of similar relationships 
- NOTE: set and individual are usually used interchangably in this class 

## Relationships 
- Subset of product of A and B 
```
A = {1, 2, 3} and B = {a, b, c, d}
R = {(1, a), (1, c), (3, b)}
```
- Relationships can also be tables that connect attributes of seperate tables 

### Multiciplicity 
![[Screenshot 2023-02-16 at 1.48.49 PM.png]]
 
## UML IS CLEANER THAN ER!! 

## More on UML
- Relationship sets can have role names in additional to the name of the set
- Entity can have a relationship with itself (BECAUSE IT IS AN ENTITY SET!!!)

## Modeling Constraints 
- **UNDERLINE** Primary Keys in E/R Diagrams
- **ARROW** is at most 1, **SEMICIRCLE** is exactly 1 for referential integrity constrains in E/R Diagrams
    - Arrow in ER is equivalant **EMPTY DIAMOND** in UML Diagrams 
    - Semicircle in ER is equivalant **FILLED DIAMOND** in UML Diagrams 

## Weak Entity Sets 
![[Screenshot 2023-02-16 at 2.01.26 PM.png]]
- "CS 411 Database Systems" is a class at UIUC, but it might also be a class at UW, and MIT, and any other college... 
- This is a weak entity set because we HAVE to go to the universty to really find out what class we are looking at
- There is no way to tell what unique course it is by only looking at the course entity
---
layout: project
type: project
image: img/projects/Animal-Farm/Title.png
title: "Animal-Farm"
date: 2022
published: true
labels:
  - C/C++
summary: "Introduce good Software Engineering practices"
---

<div class="text-center p-4">
  <img width="500px" src="../img/projects/Animal-Farm/1.jpg" class="img-thumbnail" >
</div>

In this project, my main aim was to deepen my knowledge of class hierarchy in C++ and to automate the creation of documentation using Doxygen. The project encompasses a variety of object models, such as Animal, Mammal, and Cat. Currently, the animal farm has an array-based database of cats, where each attribute is stored in an array. Additionally, there's another array-based database where each cat's attributes are encapsulated in a struct. Furthermore, there's a procedural singly linked-list database of cats, where each cat is treated as an object. Lastly, there's a collection class that implements a singly linked database of Animal objects.

Some example of the object in Animal Farm :

```cpp
 class classCat : public classMammal {
  
     protected:
     ///// Protected Attributes /////
         string name       ;
         bool   isCatFixed = false ;
     ///// Protected Attributes /////
  
     public:
     ///// Static Public Attributes /////
         static const string                SPECIES_NAME ;
         static const classWeight::t_weight MAX_WEIGHT   ;
     ///// Static Public Attributes /////
  
     public:
     ///// Constructor /////
         classCat( const string                &NewName    ) ;
         classCat( const string                &NewName,
                   const Color                 newColor,
                   const bool                  newIsFixed,
                   const Gender                newGender,
                   const classWeight::t_weight newWeight   ) ;
     ///// Constructor /////
  
  
     public:
     ///// Getters /////
         string getName() const noexcept ;
         bool   isFixed() const noexcept ;
     ///// Getters /////
  
     ///// Setters /////
         void setName ( const string &NewName )          ;
         void fixCat  ()                        noexcept ;
     ///// Setters /////
  
     public:
     ///// Static Public Member Function /////
         static bool validateName( const string &NewName ) ;
     ///// Static Public Member Function /////
  
     public:
     ///// Validation & Print /////
         string speak    () const noexcept override ;
         void   print    () const noexcept override ;
         bool   validate () const noexcept override ;
     ///// Validation & Print /////
  
     public:
     ///// Debug Print /////
         void debugPrint() const noexcept override ;
     ///// Debug Print /////
  
 };
```

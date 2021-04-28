# Access, Encapsulation, & Scope
## The `public` Keyword
The `public` and `private` keywords are very important within Java.  These keywords are defining what parts of our code have *access* to other parts of our code.  

We can define the access of many different parts of our code including instance variables, methods, constructors, and even a class itself.  If we choose to declare these as `public` this means that any part of our code can interact with them - even if that code is in a different class!  

The way we declare something to be `public` is to use the `public` keyword in the declaration statement.  In the code block belowm, we have a public class, constructor, instance variables, and method.  Notice the five different uses of `public`:  
```java linenums="1"
public class Dog{
    public String name;
    public int age;

    public Dog(String input_name, int input_age){
        name = input_name;
        age = input_age;
    }

    public void speak(){
        System.out.println("Arf! Arf! My name is " + name + " and I am a good dog!");
    }
}
```
Since everything about a `Dog` is public, any other class can access anything about a `Dog`.  For example, let's say there was a `DogSchool` class.  Any method of the `DogSchool` class could make a new `Dog` using the `public` `Dog` constructor, directly access that `Dog`'s instance variables, and directly use that `Dog`'s methods:  
```java linenums="1"
public class DogSchool{
    public void makeADog(){
        Dog cujo = new Dog("Cujo", 7);
        System.out.println(cujo.age);
        cujo.speak();
    }
}
```
Notice that the `DogSchool` class and the `#!java makeADog()` method are also public.  This means that if some other class created a `DogSchool`, they would have access to these methods as well!  We have public methods calling public methods!  

One final thing to note is that for the purposes of this lesson, we'll almost always make our classes and constructors `public`.  While you can set them to `private`, it's fairly uncommon to do so.  Instead, we'll focus on why you might make your instance variables and methods `private`.

## The `private` Keyword and Encapsulation  
When a Class' instance variable or method is marked as `private`, that means that you can only access those structures from elsewhere inside that same class.  Let's look back at our `DogSchool` example:  
```java linenums="1"
public class DogSchool{
 
  public void makeADog(){
    Dog cujo = new Dog("Cujo", 7);
    System.out.println(cujo.age);
    cujo.speak();
  }
}
```  
`makeADog` is trying to directly access `Dog`'s `.age` variable.  It's also trying to use the `.speak()` method.  If those are marked as `private` in the `Dog` class, the `DogSchool` class won't be able to do that.  Other methods within the `Dog` class would be able to us `.age` or `.speak()` (for example, we could use `cujo.age` within the `Dog` class), but other classes won't have access.  


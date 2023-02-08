# Printing Object State

## Learning Goals

- Use IntelliJ to generate a `toString()` method
- Update a program to print object state

## Introduction

Every Java class inherits a method named `toString()` that
returns a string representation of an object. 
The `toString()` method is inherited from a superclass named `Object`, which is a topic
we will cover in a later lesson.

By default, the `toString()` method returns the memory address of the object.
In this lesson, we will see how to override the `toString()` method
to return a descriptive string containing the values of the instance variables.
This allows us to print object state at various points of the program execution.


## Printing An Object Reference

Let's continue with the `Dog` class and add two print statements at the end of the `main` method
as shown:

```java
public class Dog {

    String name;
    String breed;
    int age;
    boolean waggingTail;

    public static void main(String[] args) {

        // create 2 Dog instances
        Dog bigDog = new Dog();
        Dog smallDog = new Dog();

        // assign new values to the fields of the first dog
        bigDog.name = "Bruno";
        bigDog.breed = "Great Dane";
        bigDog.age = 8;

        // assign new values to the fields of the second dog
        smallDog.name = "Penny";
        smallDog.breed = "Pug";
        smallDog.age = 5;
        smallDog.waggingTail = true;

        //print the state of each Dog instance
        System.out.println(bigDog);
        System.out.println(smallDog);

    }
}
```

When we run the `main()` method, we see something like this (memory addresses may differ):

```text
Dog@4617c264
Dog@36baf30c
```

- Behind the scenes, the compiler converts `System.out.println(bigDog);`
  to `System.out.println(bigDog.toString());`.
  - The `toString()` method is called to get a string representation of the object for printing.
- By default, `toString()` returns a string containing the name of the class, followed by "@", followed by a
  hexadecimal value corresponding to the object's memory location on the heap.

It is not particularly useful to see the memory location as the output.  Instead, we would like
to see each dog's name, breed, and so on.

## Using IntelliJ To Generate A `toString()` Implementation

Let's update the `Dog` class to change the implementation of the `toString()` method
to print the values stored in the instance variables.

We can implement `toString()` in any manner we wish; however, the easiest thing is to just have
IntelliJ generate it for us.  The `toString()` method can be placed anywhere in the class,
but we will place it directly before the `main()` method.

Position the cursor after the fields and before the `main()` method.
Right-click and select "Generate" from the menu.

![toString step 1 and 2](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/tostring_1.png)

Select "toString()" from the menu.

![toString step 3](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/tostring_2.png)    

Select all fields and then press "OK".

![toString step 4](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/tostring_3.png)

Confirm the new method named `toString()` has been added to the class above the `main` method:

```java
@Override
public String toString() {
    return "Dog{" +
        "name='" + name + '\'' +
        ", breed='" + breed + '\'' +
        ", age=" + age +
        ", waggingTail=" + waggingTail +
        '}';
}
```

Unlike the `main` method, the `toString()`
method signature does not include the keyword `static`. We will cover instance methods, which
are non-static and must be invoked with an object reference, in
detail in a later lesson. We'll also cover what `@Override` means
in a later lesson on inheritance.
But for now we can use the `toString()` method to print
the state of each dog as a descriptive string.

The `Dog` class should appear as shown below.

```java
public class Dog {

    String name;
    String breed;
    int age;
    boolean waggingTail;


    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", breed='" + breed + '\'' +
                ", age=" + age +
                ", waggingTail=" + waggingTail +
                '}';
    }

    public static void main(String[] args) {

        // create 2 Dog instances
        Dog bigDog = new Dog();
        Dog smallDog = new Dog();

        // assign new values to the fields of the first dog
        bigDog.name = "Bruno";
        bigDog.breed = "Great Dane";
        bigDog.age = 8;

        // assign new values to the fields of the second dog
        smallDog.name = "Penny";
        smallDog.breed = "Pug";
        smallDog.age = 5;
        smallDog.waggingTail = true;

        //print the state of each Dog instance
        System.out.println(bigDog);
        System.out.println(smallDog);

    }
}
```

Running the `main` method now produces the output shown below.

```text
Dog{name='Bruno', breed='Great Dane', age=8, waggingTail=false}
Dog{name='Penny', breed='Pug', age=5, waggingTail=true}
```

## Comprehension Check

### Challenge #1

Assume the following `ProgrammingLanguage` class:

```java

public class ProgrammingLanguage {

    String name;
    int yearReleased;

    @Override
    public String toString() {
        return "ProgrammingLanguage{" +
                "name='" + name + '\'' +
                ", yearReleased=" + yearReleased +
                '}';
    }

    public static void main(String[] args) {
        ProgrammingLanguage language1 = new ProgrammingLanguage();
        ProgrammingLanguage language2 = new ProgrammingLanguage();

        language1.name = "Java";
        language1.yearReleased = 1995;

        language2.name = "Go";
        language2.yearReleased = 2007;

        System.out.println(language1);
    }
}
```


<details>
    <summary>What is printed when the the <code>main</code> method executes?</summary>

  <p>Answer: <br><br>
  <code>ProgrammingLanguage{name='Java', yearReleased=1995}</code>
  </p>

</details>

<br>

### Challenge #2


Assume the following `Bike` class:

```java
public class Bike {
    String color;
    int height;
    int wheels = 2;

    public static void main(String[] args) {
        Bike mountainBike = new Bike();
        System.out.println(mountainBike);
    }
}
```


<details>
    <summary>What is printed when the the <code>main</code> method executes?</summary>

  <p>Answer: <br><br>
  Since the <code>Bike</code> class does not redefine the <code>toString()</code> method, the default implementation
  will print the memory address of the object, which looks something like this: <br> <br>
  <code>Bike@4617c264</code>
  </p>

</details>

<br>




## Conclusion

Every Java class has a method named `toString()` that
returns a string representation of an object.  The default
implementation returns the memory address of the object. IntelliJ
can generate a different implementation that returns a string
containing the values stored in the instance variables.


## Resources

- [Java 17 Object class](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

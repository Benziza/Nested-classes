# Nested-classes

## 1- The concept of nested classes

Java allows you to define as many variables and functions as you want within a class, and it also allows you to define a class within the same class.

```
class A {

    int x;

    public void print() {
        System.out.println("class A");
    }

    class B {

    }

}
```

You can put as many nested classes as you want inside each other.

```
class A {

    class B {

    }

    class C {
        class D {
        }
    }

}
```

## 2- Benefits of Nested Classes

### 2-1- Encapsulation

Nested classes can access private members of their enclosing class, which promotes encapsulation. This allows you to group related classes together and restrict access to their internals. By encapsulating related classes, you can hide implementation details and provide a clean and logical API for interacting with them.

```
public class OuterClass {
    private int outerData;

    public void outerMethod() {
        InnerClass inner = new InnerClass();
        inner.innerMethod();
    }

    private class InnerClass {
        private void innerMethod() {
            outerData = 10;  // Accessing private member
        }
    }
}
```

### 2-2- Organization and Readability

Placing related classes together improves code organization and makes it more readable. When a class is tightly related to another class and is used only by it, it makes sense to nest it within the outer class. This way, it's easier to understand the relationship between the classes.

```
class ShoppingCart {
    // Outer class code

    class Item {
        // Inner class code
    }
}
```

## 3- Types of Nested Classes

The Nested Classes are divided into two basic types:
![alt text](https://harmash.com/tutorials/java/nested-classes/098e334e-0fab-444d-8bd5-8ec7ba105c6b_nested-classes-type-in-java.PNG)

## 4- Technical terms

- A class that contains one or more classes is called an **outer class**.
- A class inside another class is called a **Nested Class** if its type is static.
- A class inside another class that is not defined as static is called the **Inner Class**.

## 5- Dealing with Static Nested Classes

Static Nested Class or Nested Class is a class that can be accessed directly from the Outer Class without the need to create an object of it.

- Exemple 1 :

```
public class A {

    static class B {

        public int x;
        public static int y;

        public void printX() {
            System.out.println("x contain: " + x);
        }

        public static void printY() {
            System.out.println("y contain: " + y);
        }

    }

}
```

Use :

```
public class Main {

    public static void main(String[] args) {

        A.B obj = new A.B();

        obj.x = 10;
        obj.printX();

        obj.y = 20; // Run But No
        obj.printY(); // Run But No

        A.B.y = 30; // Yes
        A.B.printY(); // Yes

    }

}
```

- Exemple 2 :

```
public class A {

    static class B {

        public int x;
        public static int y;

        public void printX() {
            System.out.println("x contain: " + x);
        }

        public static void printY() {
            System.out.println("y contain: " + y);
        }

    }

}
```

Use :

```
import A.B;

public class Main {

    public static void main(String[] args) {

        B obj = new B();

        obj.x = 10;
        obj.printX();

        obj.y = 20;// Run But No
        obj.printY();// Run But No

        A.B.y = 30;
        A.B.printY();

    }

}
```

## 6- Dealing with Non Static Nested Classes in Java

Non Static Nested Class or Inner Class is a class whose contents can only be accessed by an object.
Types of Inner Classes

### 6-1- Inner Classes

- An inner class is a class defined inside a class.
- The inner class can be defined as public, private, protected, or package private.

Example 1 : Public Inner Class

```
public class A {

    public class B {

        public void print() {
            System.out.println("B is a public inner class");
        }

    }

}
```

Use :

```
public class Main {

    public static void main(String[] args) {

        A.B obj = new A().new B();
        obj.print();

    }

}
```

Example 2 : Private Inner Class

```
public class A {

    private class B {

        public void print() {
            System.out.println("B is a private inner class");
        }

    }

    public void callPrintB() {
        B b = new B();
        b.print();
    }

}
```

Use :

```
public class Main {

    public static void main(String[] args) {

        A obj = new A();

        obj.callPrintB();

    }

}
```

### 6-2- Method Local Inner Classes

In Java, you can define a new class inside a function, and then that class is considered a local class in it. In the sense that it can only be accessed through it, as an object of this class can only be created inside it.

```
public class A {

    public void displayInnerClass() {

        class B {
            void print() {
                System.out.println("B is a Local Inner Class");
            }
        }

        B b = new B();
        b.print();
    }

}
```

Use :

```
public class Main {

    public static void main(String[] args) {

        A a = new A();
        a.displayInnerClass();

    }

}
```

### 6-3- Anonymous Inner Classes

If you want to use Interface without creating a class and having it execute it, or if you want to use an abstract class without creating a class that inherits from it, you can take advantage of the Anonymous Inner Class.

- 1

```
public abstract class Anonymous {
    public abstract void print();
}
```

The Anonymous Class we define starts from the word **new** to the last line.

```
Anonymous obj = new Anonymous() {

    @Override
    public void print() {
        System.out.println("Anonymous Inner Class is called");
    }

};
```

Whenever we want to use the print() function, we write the following.

```
obj.print();
```

- 2

Here we create an Anonymous Class and call the function we override in it directly when defining it.

```
new Anonymous() {

    @Override
    public void print() {
        System.out.println("Anonymous Inner Class is called");
    }

}.print();
```

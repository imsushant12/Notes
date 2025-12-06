
## Call by value and call by reference in Java
In case of primitive type variables (like int, char, etc.), Java creates a copy of the variable being passed in the method and then do the manipulations just like C/C++.

**Java only supports call by value**.

Java does not support the call by reference because in the call by reference we need to pass the address and the address is stored in pointers and java does not support pointers (because pointers break the security). When we pass an object or something, java creates a copy reference (not a copy of the object) so both the ``original reference`` and the ``copy reference`` points to the same location of the object.

### Ways to achieve pass by reference in Java.
1. Use a single element array.
2. Use a public member variable in a class. 
    Example: 
    ```java
        class Number {
            public int x = 1;
        }

        public class Test {
            public static void update(Number obj) {
                obj.x++;
            }

            public static void main(String[] arguments) {
                Number object = new Number();

                System.out.println("x = " + object.x);  // 1
                update(object);
                System.out.println("x = " + object.x);  // 2
            }
        }
    ```
3. Return the value of the updating function to the original variable only.
    Example: 
    ```java
        int change(int n) {
            n = 50;
        }

        int n = 5;
        System.out.println("n = " + n);     // 5
        n = change(n);
        System.out.println("n = " + n);     // 50
    ```
---

## Dynamic method dispatch
Dynamic method dispatch is the mechanism in which a call to an overridden method is resolved at run time instead of compile time. (Run time polymorphism).

```java
    Phone {                         // Super Class
        method_1();
        method_2();
    }
    SmartPhone extends Phone {      // Sub Class
        method_2();                 // overridden method
        method_3();
    }

    public static void main() {
        // Allowed:
        Phone object = new SmartPhone();
        // Not allowed:
        SmartPhone object = new Phone();

        // Allowed:
        object.method_1();
        object.method_2();
        // Not allowed:
        object.method_3();
    }
```

---

##
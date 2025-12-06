<p align="center">C++</p>

## Braced Initialization v/s Functional Initialization:
- **{ }** can be used to initialize variables. Empty braces or {} will initialize the variable with 0.
- **( )** can also be used for the same. Empty brackets or () will initialize the variable with 1.
  ```C++
    // Braced Initialization
    int x {20};
    int y {};
    
    // Functional Initialization
    int a (15);
    int b ();

    cout << x;             // 20
    cout << y;             // 0
    cout << a;             // 15
    cout << b;             // 1
  ```

- #### NOTE:
  - **( )** does narrowing conversion. Hence, it is less safe.
    ```C++
      int x (2.9);
      cout << x;         // 2
    ```
  - { } throws error because we are trying to convert double value (2.9) to an integer. 
    ```C++
      int x {2.9};
      cout << x;         // 2
    ```


---
### Different Number systems:
  ```C++
    int decimal = 15;           // 15
    int octal = 017;            // 15
    int binary = 0b00001111;    // 15
    int hexadecimal = 0x0f;     // 15
  ```

---
#### NOTE:
  - `break` terminates the single loop as well as the nested loops.

--- 
## Lambda Functions
- Syntax: **`[](data-type x){return logic;} (calling);`**;
- Example
   ```C++
    cout << [](int x) {return x+5;}(2);  // 7

    // OR
    auto sum = [](int x, int y) {return x + y;};
    cout << sum(2, 3);                   // 5
   ```
- **`all_of()`** function, return true if all of the value satisfies the provided lambda function.
    ```C++
    vector<int> v = {2, -1, 5};

    cout << all_of(v.begin(), v.end(), 
            [] (int x) {return x > 0;});    // 0
    ```
- Similarly, we can **`any_of()`**, return true if any one of the value satisfies the provided lambda function.
-  Similarly, we can **`none_of()`**, return true if none of the value satisfies the provided lambda function.

---
---
## STL:

1. **Ordered maps (maps)**:
   - **`map<int, int> m;`**
   - Uses tress (self balancing) for the implementation.
   - Unique keys.
   - Non-continuous in nature.
   - Keys are arranged in sorted order.
   - Access the values using `map.first` and `map.second`.
   - Can use map[] or map.find().
   - Operations take **`O(log n)`** time (if keys are not string).
   - Use **`find(key)`** to search for an element.
     - If the element is found, an iterator to the element is returned.
     - Else, an iterator is returned which points to map.end().
   - Important functions:
     - erase(value or iterator)
     - clear()
     - size()


2. **Unordered maps (unordered_map)**:
   - **`unordered_map<int, int> m;`**
   - Unique keys.
   - Uses hash tables for implementation.
   - Keys are not arranged in sorted order.
   - Operations take **`O(1)`** time (due to hashing).
   - Operations are similar to maps (ordered maps).
   - We cannot use complex data types other than **`strings`** as keys. Because complex data types does not have in built hash function definition. 

 
3. **Multimap (multimap)**:
   - **`multimap<int, int> m;`**
   - **Non** unique keys (duplicate keys).
   - **O(log n)**.


4. **Ordered sets (sets)**:
   - **`set<int> s;`**
   - sets are basically maps without values :**O(log n)**.
   - sorted order, unique keys.


5. **Unordered sets (unordered_sets)**:
   - **`unordered_set<int> s;`**
   - basically unordered maps without values :**O(1)**).


6. **Multi sets (multisets)**
   - **`multiset<int, int> m;`**
   - If we pass a value to `.erase()` function, then all the appearance of the value will be deleted. On the other hand, if we pass an iterator to `.erase()` function, only the first appearance of the value will be deleted.
   - **O(log n)**.

7. **Priority Queue**
- Max Heap: **`priority_queue <data-type> pq;`**
- Min Heap: **`priority_queue <type, vector<type>, greater<type>> pq;`**
   - Example:
      ```C++
       priority_queue <int, vector<int>, greater<int>> pq;
      ```

---
### `sort()` method:
- Syntax: `sort(begin-address, end-address);`
- Example: 
   - array: `sort(a, a+5);`
   - vector: `sort(a.begin(), a.end());`
- One of the most optimized sorting algorithm.
- Use three sorting depending upon the situation:
   - Starts with **Quick sort** and if the recursion depth goes more than a particular limit it switches to **Heap sort** to avoid Quicksort’s worse case O(N^2) time complexity.
   - Uses insertion sort when the number of elements to sort is quite less.

---
### lower bound and upper bound:
- Returns location of the searched element.
- If sorted array, then takes **O(log n)**.
- If un-sorted array, then takes **O(1)**.
- **lower bound**
   - if element is present, it returns the first occurrence. Else, it returns the next greater element of the searched element.
   - Syntax: `lower_bound(start, end+1);`
- **upper bound**
   - if element is present or not, it returns the first occurrence
   - Syntax: `upper_bound(start, end+1);`
- Example:
  ```C++
  #include <bits/stdc++.h>
  using namespace std;

  int main()
  {
      int n = 6;
      int a[] = {4, 5, 6, 3, 9};

      sort(a, a + n);

      // PRESENT
      cout << *(lower_bound(a, a + n, 5)) << endl;   // 5
      cout << *(upper_bound(a, a + n, 3)) << endl;   // 4

      // NOT PRESENT
      cout << *(lower_bound(a, a + n, 7)) << endl;   // 9
      cout << *(upper_bound(a, a + n, 7)) << endl;   // 9
  }
  ```

- In case of **sets** and **maps**, if we use the above syntax, it will take **O(n)**. So, we should use O(log n) syntax: 
  ```C++
    map.lower_bound(number);
    map.upper_bound(number);

    set.lower_bound(number);
    set.upper_bound(number);
  ```

- uses binary search in arrays and vectors.
- Uses binary tree traversal in case of sets and maps.

---
### Important Algorithms: 
1. **`min_element(start, end);`** - returns location.
2. **`max_element(start, end);`** - returns location.
3. **`accumulate(start, end, initial_value);`** - returns sum.
   - Example: 
     ```C++
     accumulate(v.begin(), v.end(), 0);
     ```
4. **`count(start, end, number);`** - returns count.
5. **`find(start, end, number);`** - returns location.
6. **`reverse(start, end);`** - returns nothing.


---
---
---
<p align="center">POINTER IN C/C++</p>

**Pointers** stores the address of other variables.

---
## Basics:

- Pointers have data-types as well.
- Since, a pointer can be used to **de-reference** a variable, a pointer stores the address of a variable of its own data type only. We can use typecasting on pointers.
- Example:
  ```C++
    int a = 10;
    int *p = &a;

    char c = "x";
    p = &c;             //ERROR

    char *p2;
    p2 = (char *)p;     //Typecast into pointer-to-char
  ```
- We can perform arithmetic operations on pointers. By adding a number (let's say 1) to a integer-pointer, we will get the address of next integer-variable.
- Example:
  ```C++
    int a = 10;
    int *p = &a;         // address: 2000
    cout << *(p + 1);    //address: 2004
  ```
  Since an integer takes 4 bytes, the next address came out as 2004.
---

### Void pointers:
- It is a generic pointer type. 
- It cannot be used for de-referencing and arithmetic operations.
- Example:
  ```C++
    int a = 10;
    int *p = &a;

    void *vP;

    // both the statements means the same.
    vP = &a;
    vP = p;

    cout << *vP;           // ERROR
    cout << (vP + 1);      // ERROR
  ```
---

### Call by Reference:
- It is used to send the address of an argument to the function.
- Call by Reference saves memory as we do not need new addresses to store functional-arguments.
- Any modifications on the formal argument inside the function will make effect on the actual argument.
- Example:
  ```C++
  void func(int *formal_argument)
  {
      *formal_argument += 2;
  }

  int main()
  {
      int actual_argument = 10;
      cout<<actual_argument;    // 10

      func(actual_argument);

      cout<<actual_argument;    // 12
  }
  ```
  **Note:**
  ```CSS
   address(formal_argument) = address(actual_argument).
  ```
- In case of arrays, there is always call by reference. Compiler implicitly converts the array-argument into a pointer-to-array argument.
- This implicit conversion is done to avoid copying the entire array again for the function. 
- Example:
  ```C++
  // void func(int *A)
  void func(int A[])
  {
      cout << sizeof(A);      // 8
  }

  int main()
  {
      int A[5];
      cout << sizeof(A);      // 20
  }
  ```

  **Note:**
  `A[i] is same as *(A + i)`
---

### Pointer to Array:
- There are a number of ways for defining pointer to an array.
- Example:
  ```C++
    int a[5];

    int *p1 = a;
    int *p2 = &a[0];
    int *p3 = a + 0;

    cout << p1;           // 0x61fdf0
    cout << p2;           // 0x61fdf0
    cout << p3;           // 0x61fdf0
  ```

---
### Dynamic Memory Allocation:
- Dynamic memory is allocated from the **heap** using some standard library functions.
- Heap area is used to store data that are created in the middle of the program execution.
- One of the main advantage is that the memory can be increased while executing program.


  ### C Language

  #### **`1. malloc()`** - memory allocation
  - allocates single block of requested memory.
  - it returns a **void pointer**, that gives address of the first allocated memory block. We typecast it into a data type so that de-referencing can be done.
  - returns **NULL** if memory is not sufficient.
  - doesn't initialize memory at execution time, it has **garbage value** initially.
  - Syntax:
    ```C++
      pointer = (data type*) malloc(byte-size);
    ```
  - Example:
    ```C++
      int *p = (int *) malloc(sizeof(int));      // variable
      int *p = (int *) malloc(10 * sizeof(int)); // array
    ```

  #### **`2. calloc()`** - continuous allocation
  - allocates multiple block of requested memory.
  - returns same as the `malloc()`.
  - initially initialize all bytes to zero.
  - Syntax:
    ```C++
      pointer = (data type*) calloc(number, byte-size);
    ```
  - here, **number** denotes the number of elements to be allocated.
  - Example:
    ```C++
      int *p = (int *) calloc(10, sizeof(int));
    ```

  #### **`3. realloc()`** - re allocation
  - reallocates the memory occupied by malloc() or calloc() functions.
  - if memory is not sufficient for malloc() or calloc(), realloc() is used to reallocate the memory. 
  - it changes the memory size.
  - it has **garbage value** initially.
  - Syntax:
    ```C++
      pointer = realloc(pointer, new_size);
    ```
  - Example:
    ```C++
      p = realloc(p, 10 * sizeof(int));
    ```

  #### **`4. free()`**
  - frees the dynamically allocated memory.
  - Syntax:
    ```C++
      free(pointer);
    ```


  ### C++
  #### How to check if memory is available or not?
  - if there is no space in the heap memory, the new request results in a failure throwing an exception (`std::bad_alloc`).
  - Example:
    ```C++
      int *p = new(nonthrow) int;  
      if(!p) // check if memory is available   
      {  
          cout << "No memory allocated!";  
      }
    ```

  #### **`1. new`**
  - allocates memory and the address of that space is returned to a pointer variable.
  - Syntax:
    ```C++
      pointer = new data_type;
    ```
  - Example:
    ```C++
      int *p = new int;
      int *p2 = new int[10];
    ```

  #### **`2. delete`**
  - delete is an operator that works same as free.
  - Syntax:
    ```C++
      delete p;
    ```

---

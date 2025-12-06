## YAML

- YAML stands for **Yet Another Markup Language**. YAML is also known as **YAML ain't Markup Language**.
- It is a data format that is used to store, represent, and exchange data. It can also be used to store information related to configuration, logs, etc. We cannot use it to store commands. 
- It is similar to JSON, and XML. These are used to serialize our data so that it can be used as various applications.
- Benefits:
    - Easy human readable
    - Indentation is there.
    - Easily convertible to JSON, XML.
    - More powerful in representing complex data.
    - Various tools or parser of YAML are available making easy parsing.
- Extension: ``.yaml`` or ``.yml``
- YAML is basically collection of documents, separated using ``---``. We end the final document with ``...`` symbol. Example:
  ```yaml
  # document-1 (key-value) pair
  "apple": "it is a fruit"
  1: "it is a number"
  ---

  # document-2 (list-type)
  - apple
  - mango
  - banana
  - guava
  ---

  # document-3 (block-type, indentation is important here)
  cities:
   - Delhi
   - Chennai
   - Mumbai
  ---

  # document-4 (flow type)
  cities: [Delhi, Mumbai, Chennai]
  ...  
  ```
- There is no multi-line comments in YAML.
---

### Data types in YAML.
- We specify the type of data using ``!!`` and then name of the data type for example ``!!str`` for string.
    ```yaml
    # String Variables
    myself: Me
    fruit: "apple"
    company: 'PwC'
    ---

    bio: | 
    hey my name is kunal kushwaha.
    i am a very nice dude.
    ---

    # write a single line in multiple lines
    message: >
    This will 
    all be 
    in one single line.

    # the above data will be same as
    message: This will all be in one single line
    ---

    # YAML can automatically detect the datatype.
    number: 5473                # integer
    marks: 98.76                # float
    booleanValue: !!bool No 
    # We can also write No as: n, N, false, False, FALSE
    # We can also write Yes as: y, Y, true, True, TRUE
    ---

    # we can also specify the data type explicitly
    zero: !!int 0
    posNum: !!int 45
    negNum: !!int -45
    binNum: !!int 0b11001
    octNum: !!int 06574
    hexNum: !!int 0x45
    commaValue: !!int +540_000          # same as: 540,000
    exponential numbers: 6.023E56       # same as: 
    marks: !!float 56.89
    infinite: !!float .inf
    not-a-Number: .nan
    boolValue: !!bool False
    string: !!str "Hello World"
    ---

    # Null or None
    surname: !!null Null 
    # We can also write No as: null NULL ~
    ~: this is a null key
    ---

    # Date and Time
    today: 2023-05-26
    date: !!timestamp 2002-12-14       # treated as UTC time.
    # separate date and time using T
    # For india using GMT value i.e. (+5:30) 
    IndiaTime: 2001-12-15T02:59:43.10 +5:30   
    NoTimeZone: 2001-12-15T02:59:43.10
    ...
    ```
- Some advance data types:
  1. Sequence - basically a list.
  2. Sparse Sequence - a sequence whose key can be empty.
  3. Nested sequence - list of lists.
  4. Maps - they are key value pairs. We can specify as: ``? key : value``.
  5. Pairs - Key having duplicate values. They are treated as array of hash tables.
  6. Set - Can contain only unique values in it. (Opposite of pairs).
  7. Dictionary - Explicitly written ``!!omap``
- Example:
    ```yaml
    # Sequence
    sequence: !!seq
    - marks
    - name
    - rollNo
    # It is same as:
    sequence: [marks, name, rollNo]
    ---

    sparse seq:
    - hey
    - how
    - 
    - Null
    - you
    ---

    # nested sequence
    - 
        - mango
        - apple
        - banana
    -
        - marks
        - rollNo
        - date
    ---
    # Map
    person:
        name: John
        age: 30
        address:
            street: 123  Street
            state: Chicago
            country: USA
    # Explicitly, we can write as:
    person: !!map
        ? name
        : John 
        ? age
        : 30
        ? address
        : !!map
            ? street
            : 123 Street
            ? state
            : Chicago
            ? country
            : USA
    
    # same as:
    person {name: John, age: 30, address: {street: 123 Street, state: Chicago, country: USA}}
    ---

    # Pairs
    pair example: !!pairs
        - job: student
        - job: developer
    # same as:
    pair example: !!pairs [job: student, job: developer]
    ---

    # Set 
    names: !!set
        ? A
        ? C
        ? B
    ---

    # dictionary
    people: !!omap
        - A:
            name: A
            age: 78
            height: 678
        - B:
            name: B
            age: 50
            height: 456
    ---

    # 

    ```

- **Note**:
    ```yaml
    The term "sequence" is a more generic term that refers to an ordered collection, while "list" typically implies that the collection is unordered and may allow duplicate items. However, in YAML, the distinction between a list and a sequence is not strict, and they are often used interchangeably.
    ```
- Reusing component using anchors. Anchors are written as: ``&anchor-name``. They can be used as: ``<< *anchor-name``. We can override the anchors.
- Example:
    ```yaml
    # reusing some properties
    likings: &likes
    like: mango
    dislike: grapes

    person1:
    name: A
    like: mango
    dislike: grapes

    person2:
    name: B
    like: mango
    dislike: grapes

    person3:
    name: C
    like: mango
    dislike: grapes

    person4:
    name: D
    like: mango
    dislike: orange
    ...
    ```
- Reusing the saved anchors. Example:
    ```yaml
    # reusing some properties using anchors
    likings: &likes
    like: mango
    dislike: grapes

    person1:
    name: A
    <<: *likes

    person2:
    name: B
    <<: *likes

    person3:
    name: C
    <<: *likes

    # overriding
    person4: 
    name: D
    <<: *likes
    dislike: orange
    ...
    ```




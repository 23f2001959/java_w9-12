# 1. Optional Types in Java

## What is Optional?

`Optional` is a **container object** introduced in **Java 8** that may or may not contain a value.
It helps **avoid NullPointerException**.

Instead of returning `null`, methods return an `Optional`.

---

## Why Optional?

Problem with `null`:

```java
String name = null;
System.out.println(name.length()); // NullPointerException
```

Solution using Optional:

```java
Optional<String> name = Optional.ofNullable(null);
System.out.println(name.orElse("Default Name"));
```

---

## Creating Optional Objects

```java
Optional<String> opt1 = Optional.of("Java");        // value must not be null
Optional<String> opt2 = Optional.ofNullable(null);  // value may be null
Optional<String> opt3 = Optional.empty();           // empty optional
```

---

## Common Optional Methods

| Method          | Purpose                       |
| --------------- | ----------------------------- |
| `isPresent()`   | Checks if value exists        |
| `get()`         | Gets value (unsafe if empty)  |
| `orElse()`      | Returns default value         |
| `orElseGet()`   | Returns value from Supplier   |
| `orElseThrow()` | Throws exception if empty     |
| `ifPresent()`   | Executes code if value exists |

Example:

```java
Optional<String> city = Optional.of("Delhi");

city.ifPresent(c -> System.out.println(c));
```

---

## Interview Point

* Optional **should not be used for fields**, only for return types.
* Avoid using `get()` directly.

---

# 2. Collecting Results from Streams

## What is Stream?

A **Stream** is a sequence of elements supporting **functional-style operations**.

Streams are used for:

* Filtering
* Mapping
* Sorting
* Collecting results

---

## What is Collecting?

`collect()` is a **terminal operation** used to **convert stream data into a collection or value**.

---

## Common Collectors

### 1. Collect to List

```java
List<String> names = List.of("Ram", "Shyam", "Mohan");

List<String> result = names.stream()
                           .filter(n -> n.startsWith("M"))
                           .collect(Collectors.toList());
```

---

### 2. Collect to Set

```java
Set<Integer> numbers = list.stream()
                           .collect(Collectors.toSet());
```

---

### 3. Collect to Map

```java
Map<Integer, String> map =
    names.stream()
         .collect(Collectors.toMap(
             String::length,
             name -> name
         ));
```

---

### 4. Joining Strings

```java
String result = names.stream()
                     .collect(Collectors.joining(", "));
```

---

### 5. Grouping

```java
Map<Integer, List<String>> grouped =
    names.stream()
         .collect(Collectors.groupingBy(String::length));
```

---

### 6. Counting

```java
long count = names.stream()
                  .collect(Collectors.counting());
```

---

## Interview Point

* `collect()` **ends the stream**
* Streams **cannot be reused**
* Intermediate operations are lazy

---

# 3. Input Output Streams in Java

## What are I/O Streams?

I/O Streams are used to **read data from a source** and **write data to a destination**.

Sources:

* File
* Keyboard
* Network

---

## Types of Streams

### 1. Byte Streams

Used for **binary data** (images, audio).

Classes:

* `InputStream`
* `OutputStream`

Example:

```java
FileInputStream fis = new FileInputStream("input.txt");
int data;
while ((data = fis.read()) != -1) {
    System.out.print((char) data);
}
fis.close();
```

---

### 2. Character Streams

Used for **text data**.

Classes:

* `Reader`
* `Writer`

Example:

```java
FileReader fr = new FileReader("input.txt");
int ch;
while ((ch = fr.read()) != -1) {
    System.out.print((char) ch);
}
fr.close();
```

---

### 3. Buffered Streams

Improve performance by reading chunks.

Example:

```java
BufferedReader br = new BufferedReader(new FileReader("input.txt"));
String line;
while ((line = br.readLine()) != null) {
    System.out.println(line);
}
br.close();
```

---

## Interview Point

* Byte streams → binary
* Character streams → text
* Always close streams (or use try-with-resources)

---

# 4. Serialization in Java

## What is Serialization?

Serialization is the process of **converting an object into a byte stream** so it can be:

* Stored in a file
* Sent over a network

Deserialization is the reverse process.

---

## Why Serialization?

* Save object state
* Transfer object between JVMs

---

## Serializable Interface

A class must implement `Serializable`.

```java
class Student implements Serializable {
    int id;
    String name;
}
```

---

## Serialization Example

```java
Student s = new Student();
s.id = 1;
s.name = "Manish";

ObjectOutputStream oos =
    new ObjectOutputStream(new FileOutputStream("data.ser"));
oos.writeObject(s);
oos.close();
```

---

## Deserialization Example

```java
ObjectInputStream ois =
    new ObjectInputStream(new FileInputStream("data.ser"));

Student s = (Student) ois.readObject();
ois.close();
```

---

## transient Keyword

Fields marked `transient` are **not serialized**.

```java
transient int password;
```

---

## serialVersionUID

Used for **version control** of serialized objects.

```java
private static final long serialVersionUID = 1L;
```

---

## Interview Point

* Serialization is **JVM specific**
* Use `transient` for sensitive data
* Needed in RMI, caching, session storage

---

## Quick Viva Summary (One-Line)

| Topic           | One Line                       |
| --------------- | ------------------------------ |
| Optional        | Avoids null pointer exceptions |
| Streams Collect | Converts stream to collection  |
| I/O Streams     | Reads and writes data          |
| Serialization   | Converts object to byte stream |



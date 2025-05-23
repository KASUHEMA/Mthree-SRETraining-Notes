# Python OOP Concepts and File Handling

This document covers various Python Object-Oriented Programming (OOP) concepts such as inheritance, polymorphism, method overriding, method overloading, abstraction, encapsulation, constructor, destructor, getter and setter, shallow copy, deep copy, class method, static method, and class variables. Additionally, it includes exception handling and file handling operations.

---

## **1. Inheritance**
### **Explanation:**
Inheritance allows a child class to acquire properties and behaviors of a parent class, promoting code reuse and organization.

### **Code Implementation:**
```python
class Animal:
    def __init__(self, name):  # Constructor initializes the object
        self.name = name  # Encapsulated variable
    
    def __str__(self):  # String representation
        return f"Animal {self.name}"
    
    def speak(self):
        return f"Animal {self.name} is speaking"

class Dog(Animal):  # Inheriting from Animal
    def speak(self):  # Overriding parent method
        return f"Dog {self.name} is barking"
```

### **Expected Output:**
```
Dog Buddy is barking
```

---

## **2. Polymorphism**
### **Explanation:**
Polymorphism allows multiple classes to have the same method but with different implementations. 

### **Code Implementation:**
```python
class Cat(Animal):
    def speak(self):
        return f"Cat {self.name} is meowing"

class Bird(Animal):
    def speak(self):
        return f"Bird {self.name} is chirping"
```

### **Expected Output:**
```
Cat Whiskers is meowing
Bird Tweety is chirping
```

---

## **3. Method Overriding**
### **Explanation:**
Method overriding allows a child class to provide a specific implementation of a method that is already defined in its parent class. This enables customization of inherited behavior.

### **Code Implementation:**
```python
class Dog(Animal):
    def speak(self):  # Overriding the speak method from Animal
        return f"Dog {self.name} is barking loudly"
```

### **Expected Output:**
```
Dog Bruno is barking loudly
```

---

## **4. Method Overloading**
### **Explanation:**
Method overloading allows multiple methods with the same name but different parameters. Python does not support method overloading explicitly, but we can achieve similar functionality using default arguments.

### **Code Implementation:**
```python
class Dog(Animal):
    def speak(self, age=0):  # Overloading via default argument
        return f"Dog {self.name} is barking and {age} years old"
```

### **Expected Output:**
```
Dog Bruno is barking and 0 years old
Dog Bruno is barking and 5 years old
```

---

## **5. Encapsulation**
### **Explanation:**
Encapsulation restricts direct access to variables, allowing controlled modification through methods like getters and setters.

### **Code Implementation:**
```python
class Person:
    def __init__(self, name, age):
        self.__name = name  # Private variable
        self.__age = age  # Private variable

    def get_name(self):
        return self.__name

    def set_name(self, name):
        self.__name = name
```

### **Expected Output:**
```
John
```

---

## **6. Shallow Copy and Deep Copy**
### **Explanation:**
- **Shallow Copy:** Copies object references without creating separate copies of nested objects.
- **Deep Copy:** Recursively copies all objects within it, making them completely independent.

### **Code Implementation:**
```python
import copy

class Address:
    def __init__(self, city, country):
        self.city = city
        self.country = country

class Person:
    def __init__(self, name, address):
        self.name = name
        self.address = address

address = Address("New York", "USA")
person = Person("John", address)
shallow_person = copy.copy(person)
deep_person = copy.deepcopy(person)
```

### **Expected Output:**
```
Original address ID: 12345
Shallow copy address ID: 12345
Deep copy address ID: 67890
```

---

## **7. Exception Handling**
### **Explanation:**
- **Try-Except Block:** Handles errors and prevents program crashes.
- **Custom Exceptions:** Allows creating user-defined exceptions for specific error handling.

### **Code Implementation:**
```python
class CustomException(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(self.message)

try:
    raise CustomException("This is a custom exception")
except CustomException as e:
    print(e)
finally:
    print("Finally block executed")
```

### **Expected Output:**
```
This is a custom exception
Finally block executed
```

---

## **8. File Handling**
### **Explanation:**
Basic operations such as creating, writing, reading, and deleting files.

### **Code Implementation:**
```python
import os

FILE_PATH = "test.txt"

def create_file():
    with open(FILE_PATH, "w") as file:
        file.write("Hello, World!\n")

def read_from_file():
    with open(FILE_PATH, "r") as file:
        print(file.read())

def delete_file():
    if os.path.exists(FILE_PATH):
        os.remove(FILE_PATH)

def check_if_file_exists():
    print("File exists" if os.path.exists(FILE_PATH) else "File does not exist")

if __name__ == "__main__":
    create_file()
    read_from_file()
    delete_file()
    check_if_file_exists()
```

### **Expected Output:**
```
Hello, World!
File does not exist
```

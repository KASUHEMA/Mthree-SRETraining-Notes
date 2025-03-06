# Kubernetes Concepts

## Minikube: A Local Kubernetes Cluster

Minikube is a Kubernetes cluster that runs locally. It includes both master node and worker node processes within a single node. A full Kubernetes cluster usually has separate master and worker nodes, which require more resources. Minikube allows developers to run Kubernetes locally with minimal resource requirements.

### **Master Node and Worker Node**

#### **Master Node:**
- Manages the entire Kubernetes cluster.
- Decides which worker node runs which pod.
- Does not handle application requests directly.

#### **Worker Node:**
- Runs applications inside pods.
- Handles traffic and processes application requests.

### **NodePort and Localhost**

#### **NodePort:**
- Opens a port on every worker node, allowing external access.
- Routes requests to the appropriate pod.
- Runs on worker nodes.

#### **Localhost:**
- Refers to the master components inside a master node.
- Refers to a single worker node inside a worker.
- Cannot be used to access pods from outside the cluster.

## **Replicas in Kubernetes vs. AWS Instances**

Replicas in Kubernetes are similar to AWS instances but function within a Kubernetes cluster instead of cloud provider infrastructure.

### **Kubernetes Replicas:**
- Defined in the `replicas` field of a Deployment.
- Ensures multiple identical Pod instances are running.
- Used for containerized applications.

### **AWS Instances:**
- Standalone virtual machines (VMs).
- Managed by Auto Scaling Groups.
- Provide full operating system environments.

## **Mapping Kubernetes Concepts to AWS**

| **Kubernetes** | **AWS Equivalent** |
|---------------|-----------------|
| **Pod** | One EC2 instance running an app |
| **Replica** | Auto Scaling Group with multiple instances |
| **Cluster** | Infrastructure distributing traffic across multiple pods |
| **Load Balancer** | AWS ELB (Elastic Load Balancer) |

# Kubernetes YAML Files

## **1. `namespace.yaml`**
Defines a Kubernetes Namespace called `k8s-demo` for logically separating resources within a cluster.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: k8s-demo
  labels:
    environment: demo
    app: k8s-master
```

## **2. `deployment.yaml`**
Defines a Deployment for `k8s-master-app` within the `k8s-demo` namespace, ensuring two pod replicas are running with a rolling update strategy.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: k8s-master-app
  namespace: k8s-demo
spec:
  replicas: 2
  strategy:
    type: RollingUpdate
  template:
    spec:
      containers:
        - name: k8s-master-app
          image: k8s-master-app:latest
          ports:
            - containerPort: 5000
          livenessProbe:
            httpGet:
              path: /api/health
              port: 5000
```

## **3. `configmap.yaml`**
Defines a ConfigMap named `app-config`, storing non-sensitive configuration data.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: k8s-demo
data:
  APP_NAME: "Kubernetes App"
  APP_VERSION: "1.0"
  ENVIRONMENT: "Production"
  DATA_PATH: "/data"
  LOG_PATH: "/logs"
```

## **4. `secret.yaml`**
Defines a Secret named `app-secrets`, securely storing sensitive information like API keys and passwords.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secrets
  namespace: k8s-demo
type: Opaque
data:
  SECRET_KEY: ZGV2LXNlY3JldC1rZXktMTIzNDU=
  DB_PASSWORD: cGFzc3dvcmQxMjM=
```

## **5. `service.yaml`**
Defines a Kubernetes Service named `k8s-master-app`, exposing it via NodePort on port 30080.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: k8s-master-app
  namespace: k8s-demo
spec:
  type: NodePort
  selector:
    app: k8s-master
  ports:
    - port: 80
      targetPort: 5000
      nodePort: 30080
```

## **6. `hpa.yaml`**
Defines a Horizontal Pod Autoscaler (HPA) for scaling the number of pods based on CPU and memory utilization.

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: k8s-master-hpa
  namespace: k8s-demo
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: k8s-master-app
  minReplicas: 1
  maxReplicas: 5
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
```

## **7. `volumes.yaml`**
Defines a ConfigMap named `app-files`, providing files as volumes inside Kubernetes pods.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-files
  namespace: k8s-demo
data:
  hello.txt: "Hello from the Kubernetes volume!"
  info.txt: "This is a sample file stored in a ConfigMap."
  sample-config.txt: |
    log_level=info
    max_connections=100
    timeout=30
```

### **📝 Notes:**
- `emptyDir` volumes are used for temporary storage within a pod's lifecycle.
- For production, `PersistentVolumes (PV)` should be used with cloud storage integration.

---

This Markdown file provides an organized and structured overview of Kubernetes concepts and YAML configurations, making it easy for you to upload to your Git repository. 🚀


# Object-Oriented Programming (OOP) in Python

## **1. Classes and Objects**
A class is a blueprint for creating objects. An object is an instance of a class with its own attributes and methods.

### **Example:**
```python
class Dog:
    species = "Canis familiaris"
    
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def bark(self):
        return f"{self.name} says Woof!"

fido = Dog("Fido", 3)
print(fido.bark())  # Output: Fido says Woof!
```
### **Explanation:**
- `Dog` is a class with attributes (`name`, `age`, `species`) and methods (`bark`).
- `self` represents the instance being created.
- `fido = Dog("Fido", 3)` creates an instance of the `Dog` class.

---

## **2. Inheritance**
Inheritance allows one class to inherit attributes and methods from another class.

### **Example:**
```python
class Pet:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Cat(Pet):  # Cat inherits from Pet
    def __init__(self, name, age, color):
        super().__init__(name, age)
        self.color = color

whiskers = Cat("Whiskers", 4, "gray")
print(whiskers.name, whiskers.color)  # Output: Whiskers gray
```
### **Explanation:**
- `Cat` class inherits from `Pet`, reusing its properties.
- `super().__init__(name, age)` calls the parent class constructor.

---

## **3. Encapsulation**
Encapsulation restricts direct access to an object's data and requires interaction via methods.

### **Example:**
```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance  # Private attribute
    
    def deposit(self, amount):
        self.__balance += amount
    
    def get_balance(self):
        return self.__balance

account = BankAccount("Alice", 1000)
print(account.get_balance())  # Output: 1000
```
### **Explanation:**
- `__balance` is a private attribute.
- Methods `deposit()` and `get_balance()` provide controlled access.

---

## **4. Polymorphism**
Polymorphism allows different classes to have the same method name but different implementations.

### **Example:**
```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Bark"

class Cat(Animal):
    def speak(self):
        return "Meow"

dog = Dog()
cat = Cat()
print(dog.speak())  # Output: Bark
print(cat.speak())  # Output: Meow
```
### **Explanation:**
- The `speak()` method is defined in the `Animal` class but implemented differently in `Dog` and `Cat`.

---

## **5. Abstraction**
Abstraction hides implementation details and only exposes essential features.

### **Example:**
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius ** 2

circle = Circle(5)
print(circle.area())  # Output: 78.5
```
### **Explanation:**
- `Shape` is an abstract class and cannot be instantiated.
- `Circle` implements `area()`, making it a concrete class.

---

## **6. Method Overriding**
A subclass can provide its own version of a method inherited from a parent class.

### **Example:**
```python
class Parent:
    def show(self):
        print("Parent method")

class Child(Parent):
    def show(self):
        print("Child method")

child = Child()
child.show()  # Output: Child method
```
### **Explanation:**
- The `Child` class overrides `show()` with its own implementation.

---

## **7. Operator Overloading**
Python allows custom behavior for operators like `+`, `-`, `*`, etc.

### **Example:**
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

v1 = Vector(2, 3)
v2 = Vector(4, 5)
result = v1 + v2  # Calls __add__
print(result.x, result.y)  # Output: 6 8
```
### **Explanation:**
- `__add__` allows `v1 + v2` to add two vectors element-wise.

---

## **8. Metaclasses**
A metaclass defines how a class behaves, similar to how a class defines object behavior.

### **Example:**
```python
class SingletonMeta(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Database(metaclass=SingletonMeta):
    pass

db1 = Database()
db2 = Database()
print(db1 is db2)  # Output: True
```
### **Explanation:**
- Ensures only one instance of a class is created (Singleton pattern).

---

## **Summary**
- **Classes & Objects:** Blueprint for creating instances.
- **Inheritance:** Reusing and extending functionality.
- **Encapsulation:** Restricting access to internal state.
- **Polymorphism:** Different classes implementing the same method differently.
- **Abstraction:** Hiding details using abstract classes.
- **Method Overriding:** Redefining methods in child classes.
- **Operator Overloading:** Custom behavior for operators.
- **Metaclasses:** Controlling class creation.

These concepts form the foundation of Object-Oriented Programming in Python. 🚀


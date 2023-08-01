---
bookCollapseSection: true
weight: 20
---

# Structural Design Patterns

> Structural Design Patterns are concerned with how classes and objectes can be composed

## Python Examples

### Adapter Pattern

> allows the interface of an existing class to be used another interface.

```python
class OldClass:
	def old_method(self):
		return "Old Method"
class Adapter:
	def __init__(self, obj):
		self.obj = obj
	def new_method(self):
		return f"{self.obj.old_method()} plus Adapter"
old_class = OldClass()
adapter = Adapter(old_class)
print(adapter.new_method())
```

### Decorator Pattern

> Allows behaviors to be added to an individual object

```python
class Component:
	def operation(self):
		pass
class ConcreteComponent(Component):
	def operation(self):
		return "ConcreteComponent"
class Decorator(Component):
	def __init__(self, component):
		self._component = component
	def operation(self):
		return self._component.operation()
class ConcreteDecoratorA(Decorator):
	def operation(self):
		return f"ConcreteDecoratorA({self._component.operation()})"
simple = ConcreteComponent()
decorator = ConcreteDecoratorA(simple)
print(decorator.operation())
```

### Composite Pattern 

> Composes objects into tree structures to represent part-whole hierachies.

```python
class Component:
	def operation(self):
		pass
class Leaf(Component):
	def operation(self):
		return "Leaf"
class Composite(Component):
	def __init__(self):
		self._children = []
	def add(self, component):
		self._children.append(component)
	def operation(self):
		results = []
		for child in self._children:
			results.append(child.operation())
		return f"Branch({'+'.join(results)})"
simple = Leaf()
tree = Composite()
tree.add(simple)
print(tree.operation())  # Outputs: Branch(Leaf)
```

### Proxy Pattern

> Provides a surrogate or placeholder for another object to control access to it.

```python
class RealImage:
	def __init__(self, filename):
		self.filename = filename
	def load_image_from_disk(self):
		print(f"Loading {self.filename}")
	def display_image(self):
		print(f"Displaying {self.filename}")
class ProxyImage:
	def __init__(self, filename):
		self.filename = filename
		self.real_image = None
	def display_image(self):
		if self.real_image is None:
			self.real_image = RealImage(self.filename)
		self.real_image.display_image()
proxy_image = ProxyImage("test_image.jpg")
proxy_image.display_image()
proxy_image.display_image()
```

### Bridge Pattern

> This pattern decouples an abstraction from its implementation so that the two can vary independently.

### Facade Pattern

> This pattern provides a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.
class Subsystem1:
	def operation1(self):
		return "Subsystem1: Ready!\n"


### Flyweight Pattern

> This pattern uses sharing to support large numbers of fine-grained objects efficiently. A flyweight is a shared object that can be used in multiple contexts simultaneously. The flyweight acts as an independent object in each context — it's indistinguishable from an instance of the object that's not shared.
		

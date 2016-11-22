---
layout: post
title: Object Oriented Programming in Python- Part I
---
I recently learned the object oriented part of _Python_. The concepts are similar to any other object oriented programming language.

----
Creating a class with constructor-

```Python
class Employee:
    def __init__(self, first, last):
        self.first = first
        self.last = last        
    def fullname(self)
        return self.first + " " + self.last
emp1 = Employee('Nikhil', 'Gupta')
print(emp1.fullname())
#print(Employee.fullname(emp1))
```

Points to note-

1. \_\_init\_\_ function acts as a constructor.
2. The first parameter is the object reference which is passed automatically to all the functions of the class. It is named as _self_ by convention.
3. emp1.fullname() and Employee.fullname(emp1) are equivalent. When object name is used, the reference is passed automatically. When the class name is used, object reference (that is _self_) needs to be passed explicitly.

---

##### Class Variables
These variables are common for all objects of that class.

```Python
class Employee:
    raise_amt = 1.05
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
    def apply_raise(self):
        self.pay = int(self.pay * Employee.raise_amt)

##########################################

emp1 = Employee('Nikhil', 'Gupta', 5000)
emp2 = Employee('Niki', 'Gupta', 10000)

print(emp1.raise_amt) # prints 1.05
print(emp2.raise_amt) # prints 1.05
print(Employee.raise_amt) # prints 1.05

emp1.apply_raise()
print(emp1.pay) # prints 5250

##########################################

Employee.raise_amt = 1.1

print(emp1.raise_amt) # prints 1.1
print(emp2.raise_amt) # prints 1.1
print(Employee.raise_amt) # prints 1.1

print(emp1.__dict__) # prints {'pay': 5250, 'first': 'Nikhil', 'last': 'Gupta'}
print(emp2.__dict__) # prints {'pay': 10000, 'first': 'Niki', 'last': 'Gupta'}
print(Employee.__dict__) # prints {...,'raise_amt': 1.1,...}

##########################################

emp2.raise_amt = 1.05

print(emp1.raise_amt) # prints 1.1
print(emp2.raise_amt) # prints 1.05
print(Employee.raise_amt) # prints 1.1

print(emp1.__dict__) # prints {'pay': 5250, 'first': 'Nikhil', 'last': 'Gupta'}
print(emp2.__dict__) # prints {'first': 'Niki', 'last': 'Gupta', 'raise_amt': 1.05, 'pay': 10000}
print(Employee.__dict__) # prints {...,'raise_amt': 1.1,...}
```

Points to note-

1. Object namespace is searched first, for the variable. If it isn't found there, class namespace is searched.
2. This allows setting a common class variable for all objects and if need be, that variable can be tinkered for individual objects.
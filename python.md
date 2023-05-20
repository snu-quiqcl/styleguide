# QuIQCL Python Style Guide

Basically we follow the [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html).
ONLY the additional conventions will be considered in our guide.
If there is any conflict with the Google's guide, a link to the corresponding part will be given.

## 1. PyQt projects
### 1.1. Naming conventions
PyQt package or other C/C++ package bindings use C/C++ style naming conventions,
which differ from Python's.
C/C++ uses `camelCase` while Python uses `snake_case` for variables, methods and functions.
Use `camelCase` for codes related to Qt (or other C/C++ package bindings) and `snake_case` for python native codes.
#### 1.1.1. Definition
PyQt is a python binding of Qt, which is a C/C++ package.
Therefore, all the variables, properties, methods and functions use `camelCase`.
#### 1.1.2. Pros
Usually the codes related to Qt can be separated easily from Python-only parts.
The code will be more readable when a group of codes shares the same naming convention.
#### 1.1.3. Cons
The code linter configuration might be tricky; it should allow multiple naming conventions.
Moreover, the criteria of convention choice is not naive, hence automatic convention checking would not be possible.
#### 1.1.4. Decision
For simple criteria, use `camelCase` for variables, attributes (properties), methods and its arguments in a class which inherits a PyQt's class, e.g., `QObject`, `QWidget`, etc.
In other words, no `snake_case` in PyQt classes.

For pylint, the following configuration would work:
```
[BASIC]
argument-rgx=_?_?(?:(?:[a-z0-9]+(?:_[a-z0-9]+)*_?_?)|(?:[a-z0-9]+(?:[A-Z][a-z0-9]*)*))$
attr-rgx=_?_?(?:(?:[a-z0-9]+(?:_[a-z0-9]+)*_?_?)|(?:[a-z0-9]+(?:[A-Z][a-z0-9]*)*))$
method-rgx=_?_?(?:(?:[a-z0-9]+(?:_[a-z0-9]+)*_?_?)|(?:[a-z0-9]+(?:[A-Z][a-z0-9]*)*))$
variable-rgx=_?_?(?:(?:[a-z0-9]+(?:_[a-z0-9]+)*_?_?)|(?:[a-z0-9]+(?:[A-Z][a-z0-9]*)*))$
```
```python
# Yes:
class Foo(QObject):
  attrOne = 1
  def __init__(self, argOne, kwargTwo=None, parent=None):
    super().__init__(parent=parent)
    self.attrOne = argOne
    varTwo = kwargTwo
  def methodOfFoo(self):
    pass

# No:
class Bar(QObject):
  attr_one = 1
  def __init__(self, arg_one, kwarg_two=None, parent=None):
    super().__init__(parent=parent)
    self.attr_one = arg_one
    var_two = kwarg_two
  def method_of_bar(self):
    pass
```

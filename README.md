# Method-Agument-in-Python
<br>First, [read the docs](https://docs.python.org/3/library/functions.html#setattr) about it. I know documentation can sometimes be hard to read, but getting in the habit of 
reading it, starting there, will help you a lot in the long run.</br>

Now, let's try an experiment. I have a class:
```python
class Animal:
    def __init__(self, **kwargs):
        self.species = kwargs.get("species")
        self.age = kwargs.get("age")
        self.sound = kwargs.get("sound")
        ```
I'm using `**kwargs` here to pack any and all keyword arguments into a dictionary. And then I'll make a wolf using that class.
```python
>>> wolf = Animal(species="Canus Lupus", age=5, sound="howl", color="gray")
>>> wolf.species
"Canus Lupus"
```
<br>Great. No errors, Python's happy, I have an instance of my Animal class. In the `__init__`, I set three attributes:
species, age, and sound. I didn't set color, though. Is it available?</br>
```python
>>> wolf.color
AttributeError...
```
No, it's not! But there weren't any errors when I created the instance. Why isn't the attribute available?
<br>
Well, because I didn't create it. Remember, Python is very explicit. If I don't do something explicitly, Python 
doesn't do it at all. Since I didn't assign a `color` attribute to `self`, my instance doesn't have a color attribute.
</br>
<br>This is where setattr comes in. `setattr` lets me set attributes that I don't know about beforehand. I can, of
course, go back and explicitly define a color attribute but what if the next user comes along and she wants a 
`height` or `weight` attribute? A year from now, `Animal`.`__init__` might be hundreds of lines long with attribute 
declarations! And some of those attributes will only apply to a few animals!</br>
<br>
But...if I'm clever and use setattr, I can just happily accept any and all attributes that someone gives for a 
particular `Animal` instance without having to continually update `__init__`.
</br>
```python
class Animal:
    def __init__(self, **kwargs):
        for attribute, value in kwargs.items():
            setattr(self, attribute, value)
```
 <br>So, since I have a handy-dandy `kwargs` dict due to using `**kwargs` in the method parameters, I can loop through 
 it's items method and pull out the two values from each iteration into `attribute` and `value` variables.
 </br>
 <br> The `setattr` function takes three arguments: the object to work on, the attribute name to define, and the value 
 to give that attribute. Now, no matter what attribute values I give to my object (assuming they're valid attribute 
 names), my class will happily apply them.
 </br>
 <br>So what's the sneakier way than using `setattr()?` Every object has an attribute named `__dict__` that is a 
 dictionary representation of the writable attributes of an object. You can update dictionaries so you could do:</br>
 ```python
 class Thief:
    def __init__(self, name, **kwargs):
        self.name = name
        self.__dict__.update(kwargs)
 ```
<br>Usually, though, you don't want to update .`__dict__` directly as it's mostly meant to be a read-only resource. 
ust because you can write to it doesn't mean you should!</br>
 





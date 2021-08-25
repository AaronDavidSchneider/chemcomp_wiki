`chemcomp` uses object oriented programming.  
It is vital that you familiarise with OOP in python. Otherwise you will not understand how `chemcomp` works.

## Small python Test:
I recommend doing this small python test that helps to understand objects in python.
<details><summary>Unveil the Test</summary>
<p>

```python
class A:  # Base class (parent)
  def __init__(self, x, y):
    self.x = x
    self.y = y
  def update_x(self, val):
    self.x += val

class B(A):  # Inheritance (child)
  def __init__(self, x, y):
    super().__init__(x, y) 
  def update_y(self, val):
    self.y += val

class C:
  def __init__(self, obj):
    self.obj = obj
  def update_obj(self, val):
    self.obj.update_x(val) 
  
a = A(1,1)
b = B(1,1)
c = C(b)
print("1:",a.x, b.x, a.y, b.y)

b.update_x(1)
print("2:",b.x)
b.update_y(1)
print("3:",b.y)
c.update_obj(1)
print("4:",b.x)
```

Do you know what it returns? 

<details><summary>Solution</summary>
<p>

```bash
1: 1 1 1 1
2: 2
3: 2
4: 3
```

Objects are passed as reference!

</p>
</details>
</p>
</details>

## Design of `chemcomp`:
`chemcomp` uses modules (objects) that are initialised at the beginning of the simulations. Those objects are then constantly updated during the time evolution. Variables pointing to other objects are always up-to-date, since python passes objects by reference (see above code example).

It is highly recommended to use numpy masking if possible. Loops should be avoided at any cost! Python is very slow when it comes to loops but very efficient if it uses numpy vectoring.

### [Disk (click here)](Disk-Module)
The Disk module has all the physics of the protoplanetary disk included. It is possible to create your own disk (for examples of disks see `chemcomp/disks` folder). 

### [Planet (click here)](Planet-Module)
Supervisor module that handles the growth of the planet (see `grow_mass()`) and updates all other modules. It is possible to overwrite methods (for examples of planets see `chemcomp/planets` folder). The most advanced planet is certainly `BertPlanet`, since it uses all kinds of migration techniques.

### [Chemistry (click here)](Chemistry-Module)
Supplies the chemical model used in `chemcomp`. 

### [Accretion (click here)](Accretion-Module)
Used in the flavours of pebble, planetesimal and gas accretion. Calculates the accretion rates.


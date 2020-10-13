`chemcomp` uses object oriented programming.  
It is vital that you familiarise with OOP in python. Otherwise you will not understand how `chemcomp` works.

### Small python Test:
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
</br>


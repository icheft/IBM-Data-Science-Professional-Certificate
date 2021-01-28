# Objects and Classes

+ every **object** has
    + a **type**
    + an internal data representation (a blueprint)
    + a set of procedures for interacting with the object (**methods**)
+ an **object** is an **instance** of a particular **type**


## Exception Handling
```py
a = 1

try:
    b = int(input("Please enter a number to divide a"))
    a = a/b
except ZeroDivisionError:
    print("The number you provided cant divide 1 because it is 0")
except ValueError:
    print("You did not provide a number")
except:
    print("Something went wrong")
else:
    print("success a=",a)
finally:
    print("Processing Complete")
```
## closure
**A closure is actually a function, that passed into another function.**

---
**Step 1.** First of all, let us take a look at a simple function.
```
func manipulateValue(x:Int) -> Int {
  return x*2+3
}
```
The function name is "manipulateValue" and its type is **(x:Int) -> Int**.  

Other function types are;  
**() -> ()**      take in no parameter and return no value  
**() -> Int**     take in no parameter and return a value of a type  
**(x:Int) -> ()** take in a parameter (or multiple parameters) and return no value  

An example of type **(x:Int) -> ()** is
```
func printValue(x:Int) {
  print("The value is \(x)")
}
```
---
**Step 2.** Next, let us create another function. This function will take in one integer and one function, and return an integer value. Yes, we are going to pass a function into this function. The function that is being passed into is called **closure**.
```
func processValue(input:Int, _closure:(_ x:Int)->Int) -> Int {
  var y=input+3
  var z=_closure(y) // << using the given function to manipulate y
  return z
}
```
At this point of time, we only define the function **_closure** as type **(x:Int)->Int**. We do not know how **_closure** is going to manipulate **x**.
  
---
**Step 3.** Now we are going to create a function that complies to the _closure type **(x:Int)->Int**. The function created in **Step 1** fits this requirement.
```
func processValue(input:Int, _closure:(_ x:Int)->Int) -> Int {
  var y=input+3
  var z=_closure(y) // << using the given function to manipulate y
  return z
}

func manipulateValue(x:Int) -> Int {
  return x*2+3
}
```

---
**Step 4.** Now, we are going to use function processValue in our program.
```
func processValue(input:Int, _closure:(_ x:Int)->Int) -> Int {
  var y=input+3
  var z=_closure(y) // << using the given function to manipulate y
  return z
}

func manipulateValue(x:Int) -> Int {
  return x*2+3
}

var result:Int = processValue(input:3, _closure:manipulateValue)

print("The result is \(result)") // 15 will be printed
...
```
As can be seen from the above example, user passes an integer 3 and a function *manipulateValue* to the *processValue* function. Function *manipulateValue* will be used by function *processValue* for manipulating data. By looking at the *var result* statement, one cannot tell how does function *manipulateValue* works unless searching for its definition.  

There is a way to define the body of function *manipulateValue* within function *processValue*.  

Let us go through the steps of function merging *"evolution"*. The steps are for illustration purpose and the syntax may be invalid.  

---
**Step A.** Substitute the definition of *manipulateValue* function into *processValueNow* function.
```
var result:Int = processValue(input:3, _closure:manipulateValue(x:Int) -> Int {return x*2+3})
```

---
**Step B.** Remove the curly brackets and replace with the keyword *"in"*.
```
var result:Int = processValue(input:3, _closure:manipulateValue(x:Int) -> Int in return x*2+3)
```

---
**Step C.** Enclose the whole *manipulateValue* function with curly brackets.
```
var result:Int = processValue(input:3, _closure:{manipulateValue(x:Int) -> Int in return x*2+3})
```

---
**Step D.** Remove the function name *manipulateValue* since the function name serve purpose here.
```
var result:Int = processValue(input:3, _closure:{(x:Int) -> Int in return x*2+3})
```

---
**Step E.** Remove the data type of x since the data type can be inferred from the declaration of function *processValue*.
```
var result:Int = processValue(input:3, _closure:{(x) -> Int in return x*2+3})
```

---
**Step F.** Remove *return* since there is only one statement, i.e. x\*2+3, in the function body. Hence, this is implicitly known as the return value.
```
var result:Int = processValue(input:3, _closure:{(x) -> Int in x*2+3})
```

---
**Step G.** Remove *-> Int* since by declaration this function is already known to return an integer.
```
var result:Int = processValue(input:3, _closure:{(x) in x*2+3})
```

---
**Step H.** Remove the bracket around x since it is redundant now.
```
var result:Int = processValue(input:3, _closure:{x in x*2+3})
```

---
**Step I.** If the closure is the last arguement of the function, then the statement can be further simplified by removing the urgement *_closure* and leave the whole closure right after the function.
```
Step 1. Remove the urgement _closure
var result:Int = processValue(input:3, {x in x*2+3})

Step 2. Remove the comma .... stop here

```
As you can see, the *manipulateValue* function is now well described in the *processValue* function by its simplified form;
**{x in x\*2+3}**. It is read as *"take in an integer value x and return an integer produced by x\*2+3."*  
  
## What happen if the closure has more than one statement in its body?
Assuming the closure body has 3 statements instead of just x\*2+3.
```
var result:Int = processValue(input:3, _closure:{x in print("I am a closure")
                                                      print("Embedded in another function")
                                                      x*2+3})
```
In this case, the last statement of the closure body must be started with the keyword *return* as shown.
```
var result:Int = processValue(input:3, _closure:{x in print("I am a closure")
                                                      print("Embedded in another function")
                                                      return x*2+3})
```
Since the closure is the last arguement of the *processValue* function, this closure can be detached from the *processValue* function as shown.
```
var result:Int = processValue(input:3) _closure:{x in print("I am a closure")
                                                      print("Embedded in another function")
                                                      return x*2+3}
```
The arguement name *_closure* is removed, and the *trailing closure* is achieved.
```
var result:Int = processValue(input:3) {x in print("I am a closure")
                                             print("Embedded in another function")
                                             return x*2+3}
```










  
  
[End. Go back to homepage.](https://siewmeng.github.io/swift/)

-------------------------------------------------------------------------

**About Markdown**

**Markdown** is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)

`Highlight background`

--- Draw line

```
For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

**Jekyll Themes**
Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/siewmeng/sm/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

**Support or Contact**
Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

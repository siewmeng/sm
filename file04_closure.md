## closure
**Closure is actually a function, but presented slight differently.**

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
**Step E.** Remove the data type of x since the data type can be inferred from the function declaration of 
```

```







To implement **do-try-catch**, there are 3 portions in the program must be in place;  
1. *Define errors*.  
2. *A function that is able to produce these errors*.  
3. *Main code that uses this function must be able to receive these errors when occurs*.  
  
**Step 1. Define errors**  
Using enum to define different error messages, and declare this enum as **Error** type (which is a must!).
```
enum mySystemErrors:Error {
    case lowVoltage
    case highVoltage
    case systemNoResponse
    case systemHalt
}
```
**Step 2. Function**  
Assuming we create a function to test a electronic system. At the end of the test, this function will read sensor input to determine if the system is healthy, otherwise, raise an error if the sensor reading does not meet the specification.  
  
The function raises errors by **throw**ing the errors defined in enum. The keyword **throws** must be used after the function name to indicate this function will throw out errors.
```
func testSystem() throws {
    // Run codes that test the system.
    // When test is completed, read the
    // voltage and speed sensors to check
    // if readings are within specifications,
    // and update the error variable with status code.
 
    if voltageSensorInput < 1 { throw mySystemErrors.lowVoltage }
    else if voltageSensorInput > 10 { throw mySystemErrors.highVoltage }
    else if speedSensorInput > 200 { throw mySystemErrors.overSpeed }
    else if speedSensorInput < 100 { throw mySystemErrors.underSpeed }
}
```
**Step 3. Main code**  
In the main program, function testSystem() is called. Since this function throws error, it must be preceeded by the keyword **try**.
```
try testSystem()
```
In order to catch error thrown out by testSystem(), the **try testSystem()** needs to be placed within the do-catch statement. The function will be executed within **do**, and statement in **catch** will be executed whenever there is error caught.
```
do{
    try testSystem()
    print("Test completed without errors!")
}
catch{
    print("Got error!")
}
```
The complete program that uses do-try-catch is shown as follows.
```
// Assuming these are the sensor input
var voltageSensorInput = 5 // volt sensor reads 5V
var speedSensorInput = 250 // speed sensor reads 300rpm

// Step 1
enum mySystemErrors:Error {
    case lowVoltage
    case highVoltage
    case overSpeed
    case underSpeed
}

// Step 2
func testSystem() throws {
    // Run codes that test the system.
    // When test is completed, read the
    // voltage and speed sensors to check
    // if readings are within specifications,
    // and update the error variable with status code.
 
    if voltageSensorInput < 1 { throw mySystemErrors.lowVoltage }
    else if voltageSensorInput > 10 { throw mySystemErrors.highVoltage }
    else if speedSensorInput > 200 { throw mySystemErrors.overSpeed }
    else if speedSensorInput < 100 { throw mySystemErrors.underSpeed }
}

// Step 3
do{
    try testSystem()
    print("Test completed without errors!")
}
catch{
    print("Got error!")
}
```
When the above is executed, the printed result will be
```
Got error!
```
because the speedSensorInput reads 250 which is greater than 200. This causes error **mySystemErrors.overSpeed** to be thrown out from the testSystem() function, and caught by the **catch** which in turn prints the "Got error!" message.
  
catch can be responding to specific error caught;
```
do{
    try testSystem()
    print("Test completed without errors!")
}
catch mySystemErrors.lowVoltage {print("Voltage Low") }
catch mySystemErrors.highVoltage {print("Voltage High")}
catch mySystemErrors.overSpeed {print("Over Speed")}
catch mySystemErrors.underSpeed {print("Under Speed")}
```
*Over Speed* will be printed in this case.

## What is try?
**try?** will turn the result into **nil** if there is an error thrown out from the function. That is to say, even there is an error, it will be not seen by the catch. As a result, statements in **catch** can never be executed and hence serve no purpose.
```
do{
    try? testSystem()
    print("Test completed without errors!")
}
catch mySystemErrors.lowVoltage {print("Voltage Low") }
catch mySystemErrors.highVoltage {print("Voltage High")}
catch mySystemErrors.overSpeed {print("Over Speed")}
catch mySystemErrors.underSpeed {print("Under Speed")}
```
*Test completed without errors!* will be printed although there is an *Over Speed* error.


## What is try!
**try!** will force unwrap the result. If there is an error thrown out by the function, using try! will be like force-unwrap a nil value, and causes execution interruption (i.e. program crash). If there is no error thrown out by the function, program will be executed normally. Hence, one must be very sure that there will be no error thrown by the function before using **try!**. Again, statements in **catch** can never be executed and hence serve no purpose.
```
do{
    try! testSystem()
    print("Test completed without errors!")
}
catch mySystemErrors.lowVoltage {print("Voltage Low") }
catch mySystemErrors.highVoltage {print("Voltage High")}
catch mySystemErrors.overSpeed {print("Over Speed")}
catch mySystemErrors.underSpeed {print("Under Speed")}
```
Program will crash in this case. Because the overSpeed error will turn the testSystem() into a nil. Force-unwrap a nil by **try!** will cause program crash.

  
  
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

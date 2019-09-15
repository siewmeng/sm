## do try catch
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


## What is try!

  
  
  
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

**do try catch**  
To implement **do-try-catch**, there are 3 portions in the program must be in place;  
1. *Define errors*.  
2. *A function that is able to produce these errors*.  
3. *Main code that uses this function must be able to receive these errors when occurs*.  
  
**Step 1. Define errors**  
Using enum to define different error messages, and declare this enum as **Error** type (which is a must!).

enum mySystemErrors:**Error** {
    case lowVoltage
    case highVoltage
    case systemNoResponse
    case systemHalt
}

**Step 2. Function**  
Assuming we create a function to test a electronic system. This function will read sensors input to determine if the system is health or raise an error if the sensor reading does not meet the specification.
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


It stands for **structure**. It is a user-defined datatype that consists of a set of variables and/or constants.  
  
The syntax for structure is
```
struct <struct name> {
    declare variable or constant
    declare variable or constant
    ...
}
```
For a start, let's use car as an example. A car can have such characteristics as model, colour and value. These characteristics can be represented by variables or constants.
```
let model:String
var colour:String
var value:Int
```
To represent my car using these variables and constant, we assign values to them.
```
let model:String
var colour:String
var value:Int

// Characteristics of my car
model="Sprina"
colour="Red"
value=12000
```
If I buy another new car, it can be represented by another set of variables and constant as
```
let model:String
var colour:String
var value:Int

let modelNew:String
var colourNew:String
var valueNew:Int

// Characteristics of my car
model="Sprina"
colour="Red"
value=12000

// Characteristics of my new car
modelNew="Accorda"
colourNew="Black"
valueNew=24000
```
If I have 10 cars, there will be 30 variables/constants in this program. To solve this problem, the 3 characteristics can be grouped into a user-defined type using **struct**.
```
struct Car {
    let model:String
    var colour:String
    var value:Int
}
```
Now, **Car** is a user-defined type, which consists of 3 characteristics (or attributes). I can now using this **Car** type to represent my cars.
```
struct Car {
    let model:String
    var colour:String
    var value:Int
}

let myCar1=Car(model:"Sprina", colour:"Red", value:12000)
let myCar2=Car(model:"Accorda", colour:"Black", value:24000)
let myCar3=Car(model:"Lanice", colour:"White", value:30000)
...
```
To access the attributes of myCar1, for example, can be done by
```
struct Car {
    let model:String
    var colour:String
    var value:Int
}

let myCar1=Car(model:"Sprina", colour:"Red", value:12000)
let myCar2=Car(model:"Accorda", colour:"Black", value:24000)
let myCar3=Car(model:"Lanice", colour:"White", value:30000)

print(myCar1.model)
print(myCar1.colour)
print(myCar1.value)
```
The output will be as follows
```
Sprina
Red
12000
```
Since myCar1 is a constant (as declared using *let*), values of its members cannot be changed although the members are variables. For example, wish to change myCar1.value from 12000 to 15600 will cause an error.
```
myCar1.value=15600 // error: Cannot assign to property: 'myCar1' is a 'let' constant
```
Unless change myCar1 to variable, i.e.
```
var myCar1=Car(model:"Sprina", colour:"Red", value:12000)

myCar1.value=15600 // valid
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

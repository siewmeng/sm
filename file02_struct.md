**struct**  
It stands for **structure**. It is a user-defined datatype that consists of a set of variables and/or constants.  
  
The syntax for enumeration is
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
When executed, will print the following which sound funny!
```
Hello! light, invalid signal.
```
To avoid such situation from arising, we restrict colour to a set of values i.e. only allows Red, Green and Yellow.  

First of all, we define a data type using keyword **enum** and give this data type a name called MyColour (also known as *enum name*). This data type has 3 members(or known as *identifiers*); Red, Green and Yellow.

```
enum MyColour {
    case Red
    case Green
    case Yellow
}
```

Now, declare variable colour as MyColour data type, and assign it a pre-defined value.
```
var colour:MyColour

colour=.Red
```
Please note that there must be a dot before the identifier Red.  
  
Below are some of the "correct" and "incorrect" assignments.
```
colour=Red      // incorrect
colour="Red"    // incorrect
colour=.Purple  // incorrect as Purple is not a member of MyColour

colour=.Red         // correct
colour=Mycolour.Red // correct
```
By declaring variable *colour* as the user-defined type MyColour, its values are now restricted to .Red, .Green and .Yellow. Just a reminder, .Red, .Green and .Yellow are not strings. They are identifiers defined within MyColour.
  
Now, re-write the above example as:
```
enum MyColour {
    case Red
    case Green
    case Yellow
}
var colour:MyColour

colour = .Red

switch colour {
case .Red:
    print("\(colour) light, cars stop.")
case .Green:
    print("\(colour) light, cars move.")
case .Yellow:
    print("\(colour) light, cars stopping.")
}
```
Please note that the *default:* case in the above *switch* can be removed as all cases have been covered.  
Since no other values besides .Red, .Green and .Yellow are allowed, one of the three printed outputs is expected.  

When executed, it will print
```
Red light, cars stop.
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

**enum**  
It stands for **enumeration**. It is a user-defined datatype that has a finite set of values.

Let's consider the following string variable.  

```markdown
var colour:String

colour="Red"      // assigned Red
colour="Green"    // change to Green
colour="Yellow"   // change to Yellow

... and so on
```  
We can even assign non-colour word to this variable, as long as the data type is a string.
```
colour="hello!"
```
This is nothing wrong syntactically, however it does not sound so correct logically. Look at the example below.
```
var colour:String
colour="Hello!"

switch colour {
case "Red":
    print("\(colour) light, cars stop.")
case "Green":
    print("\(colour) light, cars move.")
case "Yellow":
    print("\(colour) light, cars stopping.")
default:
    print("\(colour) light, invalid signal.")
}
```
When executed, will print the following which sound funny!
```
Hello! light, invalid signal.
```
To avoid such situation from arising, we restrict the values to a set of strings, e.g. only allows Red, Green and Yellow.  

First of all, we define a data type and let's call it MyColour. MyColour has 3 members; Red, Green and Yellow.  
*Please note that they are just identifiers and no string data types.*

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
By using the user-defined type MyColour, variable *colour* is now restricted to values of .Red, .Green and .Yellow.  
Please note that .Red, .Green and .Yellow are not strings.  
  


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

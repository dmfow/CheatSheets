
## Strings
```
# remove the second character
var myString = "whatever"
var i = myString.index(string.startIndex, offsetBy: 1)
var newString = myString.remove(at: i)
# myString = watever
# newString = h

# Remove subrange
var versionIndex = myString.indx(myString.startIndex, offsetBy: 5)
myString.removeSubrange(myString.startIndex..<versionIndex)
# myString = ver

# Insert last
let lastIndex = myString.index(myString.endIndex, offsetBy: 0)
myString.insert"5", at: lastIndex)

# Reverse
revString = String(myString.reversed())

# Concat
let s1 = "1234"
let s2 = "5678"
var s3 = s1 + s2
# s3 = 12345678

# Concat 2
var myString = "This is"
myString += " it"
# myString = This is it

# Append
var myString = "This is"
myString.append(" it")

# Span over several lines
let description = """
	a long
  	long 
      	long description
	"""
    
let num = 4
let name = "This is a \(num)"
    
var myString = "Fathers"
myString.append(" day")



removeFirst()       remove the first character
removeLast()        remove the last character
lowercased()        get a new string, lowercased
uppercased()        get a new string, uppercased
starts(with:)       returns true if the string starts with a specific substring
contains()          returns true if the string contains a specific character
    
# Index of the first character
myString.startIndex


let myString = "Longcar"
let i = myString.index(myString.startIndex, offsetBy: 2)
myString.suffix(from: i)
# OR
myString[i...]


# *** When you get a substring from a string, the type of the result is Substring, not String.
let myString = "Longcar"
let i = myString.index(myString.startIndex, offsetBy: 2)
print(type(of: myString.suffix(from: i))) 

# Strings are collections, and they can be iterated over in loops


```

## Conversion to string
```
var num = 123
var myString = "\(num)"

var myString = String(num)


# Array
let myArray = ["This", "is", "it"]
let myString = myArray.joined(separator: " ")
# This is it

```

## Conversion from string
```
var myString = "123"
var num = Int(myString) ?? 678
# num = 123

var myString = "123ab"
var num = Int(myString) ?? 678
# num = 678

```

## String content - Remove stuff (parentheses stuff)
```
let myString = "This () is it (with some more stuff)"
let newString = myString.replacingOccurrences(of: "\\s?\\([\\w\\s]*\\)", with: "", options: .regularExpression)

Searches for:
- An optional whitespace character \\s?.
- An opening parenthesis \\(.
- Zero or more word or whitespace characters [\\w\\s]*.
- A closing parenthesis \\).

Alternative pattern is "\\s?\\([^)]*\\)" which represents:
- An optional whitespace character \\s?.
- An opening parenthesis \\(.
- Zero or more characters anything but a closing parenthesis [^)]*.
- A closing parenthesis \\).


```

## Finding
```
let myString = "It's red green"
if myString.contains("red") {
    print("Found")
}

# OR

let strgArray = ["manage", "values"]
if stringArray.contains("values") {
    print("yes")
}

# OR

let myString = "this is the best car"
if myString.range(of: "the best") != nil {
    print("Substring found")
}

# OR


let myString = "this is the best car"
let subStr = "best"
let pattern = "\\b\(subStr)\\b"
let regex = try! NSRegularExpression(pattern: pattern, options: .caseInsensitive)
let range = NSRange(location: 0, length: myString.utf16.count)
if regex.firstMatch(in: myString, options: [], range: range) != nil {
    print("Found")
}


```




## Formatting
```
let num: Int = 12
let str1 = String(format: "%03d", num)
# 012

let str1 = String(format: "%.2f", num)
# 12.00

let str1 = String(format: "%2X", num)
# C (Hex)

let str1 = String(format: "%2x", num)
# c (Hex)


```

## Text
```
Text("The text to display")
      .frame(alignment: .leading)
      .foregroundColor(Color(#colorLiteral(red: 0.234564, green: 0.45632, blue: 0.63344, alpha: 1)))
                .foregroundColor(Color.white)
      .font(.title)
      .padding()
      .padding(.bottom, 16)
      .background(Color.white)
      .multilineTextAlignment(.center)
      .border(.yellow)
      .padding([.bottom, .trailing], 20)
      .fontWeight(.bold)
```

## Image
```

   Image(image)
      .aspectRatio(contentMode: .fill)
      .aspectRatio(contentMode: .fit)
      .background(Color.blue)
      .clipped(antialiased:true)
      .cornerRadius(10)
      .foregroundColor(.white)
      .frame(minWidth: 0, maxWidth: .infinity)
      .frame(width: 50, height: 50)
      .frame(width:g.size.width, height:g.size.height/4*3)
      .offset(x: 3, y: -3)
      .padding()
      .resizable()
      .shadow(radius:25, x:0, y:0)

      .overlay(LinearGradient(gradient: Gradient(colors: [Color(#colorLiteral(red: 0, green: 0, blue: 0, alpha: 0.2345666)), Color(#colorLiteral(red: 0, green: 0, blue: 0, alpha: 0))]), startPoint: .bottom, endPoint: .top))
                .frame(width: 50, height: 50)
      .overlay(
            Text(text)
            .foregroundColor(Color.white)
            .font(.title)
            .padding(),
            
            alignment: .bottomLeading
        )
       .addVerifiedBadge(eventIsVerified)
```
      
## Use a Template
```
MyBestText(text: "This is a nice text to show")
        .padding(.all)


struct MyBestText: View {
  private(set) var text: String
  var body: some View {
    Text(text)
      .frame(alignment: .leading)
      .foregroundColor(Color(#colorLiteral(red: 0.2901960784, green: 0.2901960784, blue: 0.2901960784, alpha: 1)))
  }
}
```

## Stackars and spacers
```
        HStack(alignment: .top, spacing: 15) {
            VStack {
                CalendarView()
                Spacer()
            }
            VStack(alignment: .leading) {
                Text("Event title").font(.title)
                Text("Location")
            }
            Spacer()
        }.padding()
```

## Comments
```
//this is a comment

let a = 1 //this is a comment

/* this
 is
    a multi-line
 comment
*/

/* this
 is
    a /* nested */ multi-line
 comment
*/
```


## Numerical conversion
```
let age : UInt8 = 3
let intAge = Int(age)

let age = Double(3)
let count = Int(3.14)
```


## SETs
```
# While an array can contain many times the same item, you only have unique items in a set.
# Unlike arrays, there is no order or position in a set. Items are retrieved and inserted randomly.
# Sets, like arrays, are passed by value. This means that if you pass it to a function, or return it from a function, the set is copied.

let set: Set<Int> = [1, 2, 3]
# OR
let set = Set([1, 2, 3])
set.insert(17)
set.contains(2)
set.count
set.isEmpty
# Remove a specific value (not on the index)
set.remove(1)

set.removeAll()
# If you want to print it in order. Convert it to an array
let orderedList = set.sorted()


# Sets can perform set math operations like intersection, union, subtracting, and more
intersection(_:)
symmetricDifference(_:)
union(_:)
subtracting(_:)
isSubset(of:)
isSuperset(of:)
isStrictSubset(of:)
isStrictSuperset(of:)
isDisjoint(with:)

```

## Dictionaries
```
# A dictionary must be declared as var to be modified. If it's declared with let, you cannot modify it by adding or removing elements
var dict = ["South": 8, "North": 7]
var dict: [String: Int] = ["South": 8, "North": 7]

var dict = [String: Int]()
# OR
var dict: [String: Int] = [:]


print(dict["South"])    // gives 8

# Change
dict["South"] = 9
# New pair
dict["West"] = 3
# Remove a keypair
dict["West"] = nil
# OR
dict.removeValue(forKey: "West")

dict.count
dict.isEmpty

```


## Tuples
```



```





        
## Mix of others
```
# Check if multiple
var age = 8
print(age.usMultiple(of: 5))

# Number of characters in a string
age.count


# Operators
# +, -, *, / (division), % (remainder)

# Compound operators
# +=
# -=
# *=
# /=
# %=

# Comparison operators
#   You can use those operators to get a boolean value (true or false)
# ==
# !=
# >
# <
# >=
# <=

# Range operators
0...5 //6 times
0..<2 //2 times

0...count //"count" times
0..<count //"count-1" times

# Example
let count = 5
for i in 0...count {
  // Stuff
}

# Logical operators
# NOT: !
# AND: &&
# OR: ||

#Example
if this && that {
  // Stuff
}

# If
if checkme == true {
    // Stuff
}

# If - ternary conditional operator
let num1 = 1
let num2 = 2
let smallerNumber = num1 < num2 ? num1 : num2 

# Switch
var myString = "Blue"

switch myString {
case "Blue":
    print("Blue color is best")
default: 
    print("What is \(myString)")
}

# Switch with range
var age = 20
switch age {
case 0..<18:
    print("You can't drive!!")
default: 
    print("You can drive")
}


# Enum
enum Animal {
    case dog
    case cat
}
var animal: Animal = .dog
switch animal {
case .dog:
    print("Hello, dog!")
case .cat:
    print("Hello, cat!")
}

# For loop
for index in 0...3 {
  // 4 times, index is: 0, 1, 2, 3
}

let list = ["a", "b", "c"]
for item in list {
  // Stuff
}


let list = ["a": 1, "b": 2, "c": 2]
for (key, value) in list {
  // Stuff
}

# While
var item = 0
while item <= 3 { 
    // Stuff
    // repeats 3 times
    item += 1
}

# Repeat
var item = 0
repeat { 
    // Stuff, repeats 3 times
    item += 1
} while item < 3

# 2 statements that you can use to control the flow inside a loop: continue and break
# continue to stop the current iteration, and run the next iteration of the loop
# break ends the loop, not executing any further operations or iterations

let list = ["a", "b", "c"]
for item in list {
  if (item == "b") {
    break
  }
  //do something
}

var a = 2; let b = 3



# 64-bit (32-bit on 32-bit systems)
Int
Double


Int8    is an integer with 8 bits
Int16   is an integer with 16 bits
Int32   is an integer with 32 bits
Int64   is an integer with 64 bits
UInt8   is an unsigned integer with 8 bits
UInt16  is an unsigned integer with 16 bits
UInt32  is an unsigned integer with 32 bits
UInt64  is an unsigned integer with 64 bits
UInt    is like Int, but unsigned, and it ranges from 0 to Int.max * 2.
Float   is a decimal number with 32 bits.
    
with Cocoa API you might use other numeric types like CLong, CGFloat and others


Bool

# Arrays
var list: [Int] = []
# OR
var list = [Int]()

var list: [Int] = [1, 2, 3, 4]
# OR
var list = Array(1...4)

list.isEmpty
list.append(4)
# Array operations, Index start with 0
list.insert(17, at: 2)
list.remove(1)

list.removeLast() 
list.removeFirst()
list.sort()

list.removeAll()
# OR
list = []

Arrays are equal when they contain the same elements, of the same type:
[1, 2, 3] == [1, 2, 3]

```



        

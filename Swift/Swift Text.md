
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

## Remove stuff (parentheses stuff)
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
      .resizable()
      .aspectRatio(contentMode: .fit)
      .resizable()
      .frame(width: 50, height: 50)
      .padding()
      .background(Color.blue)
      .cornerRadius(10)
      .offset(x: 3, y: -3)
      .foregroundColor(.white)
      .background(Color.red)
      .frame(minWidth: 0, maxWidth: .infinity)
      .frame(width: 50, height: 50)
      .background(Color.red)
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
        
        
        

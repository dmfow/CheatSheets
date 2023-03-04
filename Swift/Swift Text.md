
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
        
        
        

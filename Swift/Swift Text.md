
## Text
Text("The text to display")
      .frame(alignment: .leading)
      .foregroundColor(Color(#colorLiteral(red: 0.2901960784, green: 0.2901960784, blue: 0.2901960784, alpha: 1)))


## Use a Template

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

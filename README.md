# FlutterJSX
Framework that adds JSX syntax capabilities in Flutter framework with Dart!
This framework is in development.
Steps that should be done:
1) Make a syntax for a JSX.
2) Make a JSX parser for Dart.
3) Make parser result in Flutter nested tree component.
4) Allow parser to work with third component widgets.
5) Make a compiler from .flx files to dart code.
6) Make a compiler of .flx files to dart code using parser.
7) Make compiler analize code.
8) Make compiler show warnings and errors.
9) Find a way to connect it to Flutter app.
10) Test it.
11) Make hot reload for each .flx file.
12) Etc.
    
### Rules 
Widget gets property children when it will have multiple child elements at the same level. Gets child when it have only one child element. If you want a widget with children property to have only one child then you should put "child" value in its attributes. Like:
```jsx
var Component = <>
  <Row child>
    <Text>Child</Text>
  </Row>
</>
```

Also widgets with text property must have any text or {"string like this"} or string {variable}. But it is better to put it in attribute:
```jsx
var Component = <>
  <Text>Hi</Text>
  <Text text="Hi"> 
  <Text>{variable}</Text>
  <Text text={variable}> 
  <Text>{"Hi"}</Text>
  <Text text={"Hi"}>
</>
```
### Condition elements 
There is a new way to render a widget by condition putting them in <if {condition}></if> tag:
```jsx
var Component = <>
  <if {true}>
    <Text>Hi</Text>
  </if>
</>
```
or with else if:
```jsx
var Component = <>
  <if {true}>
    <Text>Hi</Text>
  </if>
  <elif {1==1}>
    <Text>Hi</Text>
  </elif> 
  <elif {1!=2}>
    <Text>Hi</Text>
  </elif> 
  <else>
    <Text>Hi</Text>
  </else>
</>
```
Notice that elif and else need to be placed after if or another elif tag, while tag if can be alone.
This tags will create an ugly condition?widget1:contition?widget2... code which you don't need to worry.

### Right now JSX syntax way is not selected. You can offer your variant and wants in discussion issue. Possible syntax:
```jsx
var counter = 0;
//Components should be <></> tags or (props) => <></> function(right now it is the best decision, mention in issues if you have better).
var ItemText = (props) => <>
  <Text TextStyle=(fontWeight: FontWeight.bold)>
    {props.name}
  </Text>
</>;
var ItemStatus = <>
  <Text>Caliph: <Text/>
</>;

var MyComponent = <>
  <Column>
    {
      for(var name in ["Abubakr", "Omar", "Osman", "Ali"])
        <Row>
          <ItemStatus />
          <ItemText name={name} />
        </Row>
    }
    <Row>
      <Text id="text-id" style={fontWeight: FontWeight.bold}> //or should it be style={TextStyle(fontWeight: FontWeight.bold)}
        {counter}//state like in Svelte
      </Text>
      <Button onPress={(){counter++;}} style={backgroundColor: Colors.purple}> //or should it be style={ElevatedButton.styleFrom(backgroundColor: Colors.purple)}
        <Text>Add 1</Text>
      </Button>
    </Row>
  </Column>
</>;
```
### or like in https://pub.dev/packages/xml_layout (it has ready parser, but makeup is kinda verbose):
```dart
//Components should be in <></> tags.
var Component = <>
  <Column mainAxisAlignment="center">
      <for count="$counter">
          <Text>$item, You have pushed the button this many times:</Text>
          <if candidate="equal(1, mod($item, 2))">
              <Text>Test2</Text>
          </if>
      </for>
      <Text id="text-id">
          <attr:style>
              <TextStyle color="red"/>
          </attr:style>
          $counter
      </Text>
      <Icon color="blue">airport_shuttle</Icon>
  </Column>
</>;

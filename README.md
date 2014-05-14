XAML Coding guidelines
======================

## How to contribute

You can open an issue on this project to raise an issue/argument about an existing rule, or to submit a new rule. For each submission, please at least produce the following items:

- Cause
- Rule description
- Justification
- How to fix violation

You can also add a code sample of the violation and a code sample with the violation fixed.

### Want to translate the XAML coding guidelines in another language ?

Sure! Please create an issue and we can discuss how we can work on creating multilingual versions of these guidelines.

## Guideline principles

- **Be easy to follow**: Each rule must be explained as simply as possible. Any developer on his/her 1st day with Xaml must be able to follow these rules,
- **Be as uncontroversial as possible**: These rules must be out of debate. We're not here to determine if it's better to have a white-themed Visual Studio or a black-themed one (Pro-Tip: the correct answer is of course black). So, each rule must have a justification. An inspiration from [StyleCop](http://www.stylecop.com/docs/StyleCop%20Rules.html) rules can be useful,
- **Be usable for any Xaml-based project**: Windows Phone, WPF or Universal apps. It must apply for all of them. If a rule only applies to one platform, it should go under a platform-specific section.


## Rules

### XA1x. Code readability

#### XA1001 - Put one attribute per line
##### **Cause**
Multiple attributes are declared on the same line.

##### **Rule description**
A violation of this rule occurs whenever an element has multiple attributes declared on the same line. For example: 

```xml
<Button x:Name="MyButton" Text="Hello world" Foreground="Blue"  />
```

Quickly, this can lead to *forgotten attributes*, because the XAML code editor is often split in two with code view and design view. We could apply a specific rule, like "limit to 60 column caracters" or "limit to 2 attributes per line". However, all these rules create special cases and interpretations that lead to difficulties in implementing this rule in our brain. Therefore, it's more suitable to apply a simple rule every time.

##### **How to fix violation**
To fix a violation of this rule, place only one attribute per line.

You can also use the default key combo `Ctrl+K, Ctrl+F` to automatically format the current selection/document.

```xml
<Button x:Name="MyButton" 
        Text="Hello world" 
        Foreground="Blue"  />
```

#### XA1002 - Put the first attribute on the element line

##### **Cause**
When an element has at least one attribute defined, the first line contains only the element.

##### **Rule description**
A violation of this rule occurs whenever an element is the only thing declared on the line.

```xml
<Button 
    x:Name="MyButton" 
    Text="Hello world" 
    Foreground="Blue"  />
```

Declaring only the element without one of the attributes can lead to too many carriage returns when the element contains only one attribute. We can't create an exception for these one-attribute element declarations.

Moreover, adding the attributes on subsequent lines can lead to a tab alignment which is under the element. This alignment is not optimal for reading.

##### **How to fix violation**
Place the first attribute on the same line as the opening element.
```xml
<Button x:Name="MyButton" 
        Text="Hello world" 
        Foreground="Blue"  />
```

#### XA1003 - Within an element, order attributes alphabetically
##### **Cause**
Within an element tag, attributes are unordered.
```xml
<Button Text="Hello world" 
        Foreground="Blue"
        TextAlignment="Center"
        />
```

##### **Rule description**
A violation of this rule occurs whenever attributes within an element are not ordered alphabetically within the element's declaration.

**Current proposal and discussions**
There are discussions about this rule. Please see the [related proposal](https://github.com/cmaneu/xaml-coding-guidelines/issues/1).

##### **How to fix violation**
Order all attributes in alphabetical order, while complying with the related rules.

```xml
<Button Foreground="Blue"
        Text="Hello world" 
        TextAlignment="Center"
        />
```


##### **Related rules**

- **XA1004**: Put the x:Name or x:Key as the first attribute
- **XA1005**: Put attached properties at the beginning of the element, eventually after the x:Name/x:Key

#### XA1004 - Put the x:Name or x:Key as the first attribute
##### **Cause**
Within an element tag, with the attribute `x:Name` or `x:Key` declared, this attribute is not the first declared.

```xml
<Button Text="Hello world" 
        x:Name="ValidationButton"
        TextAlignment="Center"
        />
```

##### **Rule description**
A violation of this rule occurs when an element declares multiple attributes and at least a `x:Name` or `x:Key` attribute, this attribute must be placed first.

These attributes are more important than any others because:
- They identify the uniqueness of a control, 
- They identify that the control is used elsewere (storyboard, code behind, binding, ...).

Setting this attribute at the top helps to identify these controls and ensure any changes made to the control are done carefully.


##### **Related rules**

- **XA1005**: Put the attached properties at the beginning of the element, eventually after the x:Name/x:Key
- **XA2001**: Name elements with the `x:Name` attribute

##### **How to fix violation**
Place the `x:Name` or `x:Key` attribute first.
```xml
<Button x:Name="ValidationButton"
        Text="Hello world" 
        TextAlignment="Center"
        />
```



#### XA1005 - Put the attached properties at the beginning of the element, eventually after the x:Name/x:Key
##### **Cause**
Attached properties are declared in any order within the element properties.

```xml
<Button x:Name="ValidationButton"
        Text="Hello world" 
        Grid.Column="2"
        Grid.Row="0"
        TextAlignment="Center"
        />
```

##### **Rule description**
A violation of this rule occurs when an element declares attached properties and their declaration is not at the top of all attribute declarations, except the `x:Name` and `x:Key` attributes.

Attached properties can change the appearence or behavior of your control. They can also surcharge some of the control's properties. Declaring them at the top helps you identify these cases.

##### **How to fix violation**
Place all the attached properties, in alphabetical order, first. If `x:Name` and `x:Key` attributes are declared, they are declared before any attached property declaration.

```xml
<Button x:Name="ValidationButton"
        Grid.Column="2"
        Grid.Row="0"
        Text="Hello world" 
        TextAlignment="Center"
        />
```


#### XA1006 - If an element has no content, use a self-closing element
##### **Cause**
An element uses a closing tag without defining child elements.

```xml
<Button x:Name="ValidationButton"
        Text="Hello world" 
        ></Button>
```

##### **Rule description**
A violation of this rule occurs when an element does not declare child tags and uses an explicit closing tag.
This leads to too much space waste.

Visual Studio and Blend XAML code editors can easily expand closing tags if needed when adding the first child of an element, therefore that argument is not pertinent.

##### **How to fix violation**
Use a self-closing element instead.

```xml
<Button x:Name="ValidationButton"
        Text="Hello world" 
        />
```

### XA2x. Naming

#### XA2001 - Name elements with the `x:Name` or `x:Key` attribute
##### **Cause**
Name or Key attributes are used without the namespace prefix.

```xml
<Button Name="ValidationButton"
        Text="Hello world" 
        />
```

##### **Rule description**
A violation of this rule occurs when the `Name` or `Key` attributes are declared without the `x:` namespace prefix.

These attributes are more important than any others because:
- They identify the uniqueness of a control, 
- They identify that the control is used elsewere (storyboard, code behind, binding, ...).

Making this attribute more visible with the namespace prefix helps to identify these controls and ensure any changes made to them are done carefully.

##### **How to fix violation**
Always declare `x:Name` or `x:Key` with their `x:` namespace prefix.

```xml
<Button x:Name="ValidationButton"
        Text="Hello world" 
        />
```

#### XA2002 - Use Pascal Casing

This rule is under editing, waiting for comments.


#### XA2003 - Suffix XAML names with a type indication
##### **Cause**
An element is named without a type indication.

```xml
<Button x:Name="Checkout"
        Text="Checkout" 
        />
```

##### **Rule description**
A violation of this rule occurs when an element's name does not include any hint about the elment's type at the end of its name.

Suffixing an element's name helps identify the page/control class members that are part of the UI and get a sense of what we can do with them.

##### **How to fix violation**
Suffix the element's name with a type indication.

```xml
<Button x:Name="CheckoutButton"
        Text="Checkout" 
        />
```

##### **Related rules**

- **XA2004** Do not use a precise type indication suffix, unless it's required

#### XA2004 - Do not use a precise type indication suffix, unless it's required
##### **Cause**
An element's name indicates a precise type, however no code uses any type-specific properties/methods.

```xml	
<StackPanel x:Name="ActionsStackPanel">
    ...
</StackPanel>
```

```
ActionsStackPanel.Opacity = 0;
```

##### **Rule description**
A violation of this rule occurs when an element's name contains precise type indication and no code is using specificities of this class, but only properties/methods defined on a base class/interface.

For a lot of use cases, you don't need to know the exact element type. Let's see it in an example: 
```xml	
<StackPanel x:Name="ActionsPanel">
    ...
</StackPanel>
```
In this case, if you are just using `ActionsPanel` to change the visibility, the name is correct. `ActionsStackPanel` will convey too many details and prevents you from changing at a later time the `StackPanel` for a `Grid`.

However, if you will change the `Orientation` property somewhere, `ActionsStackPanel` is an appropriate name, as you should be aware that you will use specific properties of the `StackPanel` class.

##### **How to fix violation**
Remove precise indication suffix.

#### XA2005 - Name only nodes used in code-behind, element binding or animation
##### **Cause**
An element defines a name and nobody uses it.
```xml	
<StackPanel x:Name="ActionsPanel">
    ...
</StackPanel>
```

```
    ...
```

##### **Rule description**
A violation of this rule occurs when an element defines a `x:Name` or `x:Key` attribute and this name/key is not referenced/used in any code-behind code, element binding, or storyboard.

##### **How to fix violation**
Remove `x:Name` or `x:Key` attribute.

```xml	
<StackPanel>
    ...
</StackPanel>
```

### XA3x. Maintenability

#### XA3001 - Use the rule of 3 to decide if a value must be declared as a resource
##### **Cause**
A property value is used at least three times.

##### **Rule description**
A violation of this rule occurs when a property value is used more than 2 times at different places. If so, this value will likely be used elsewhere. For greater maintenability, this property value must be declared as a resource.

##### **How to fix violation**

- Move the value to a resource, 
- Replace all value usage by a StaticResource binding.

#### XA3002 - All the implicit styles must be placed at the top of the file and must be annotated with a comment
##### **Cause**
An implicit style is declared elsewhere on a page/resource dictionary.

##### **Rule description**
A violation of this rule occurs when an implicit style is declared anywhere on a page/resource dictionary file, except at the top.

The implicit style must be used only when they apply to a whole page/app. If they apply only to a subset of a page/app, they must be declared as explicit styles.

As these styles have a broad impact, they must be declared first and commented properly to give them visibility.

##### **How to fix violation**
If the style is used throughout the file:
- Move the style declaration to the top of the `Resources` element,
- Add a comment before the style declaration, stating the implicit nature.

If the style is used only on a portion of the file:
- Make the style an explicit style,
- Add the proper style binding in all involved controls.

#### XA3003 - Name should reflect usage scenario
##### **Cause**
As the application evolves, styles tend to get used on controls and/or cases that weren’t necessarily thought of in the first place. Having style names reflecting their usage eases app maintenance.

##### **Rule description**
A violation of this rule occurs when a style is used for something else that it was initially meant for causing its name to be out of sync with its purpose. For example:

```xml	
<Style x:Key="ListBoxStyle" TargetType="phone:LongListSelector" />
```

As soon as the use of a style is changed and/or extended it should be renamed to reflect its new use.

##### **How to fix violation**

Rename your style to reflect its use.

```xml	
<Style x:Key=" LongListSelectorStyle" TargetType="phone:LongListSelector" />
```

### XA4x. Resource file organization

The following rules are under editing.

#### XA4001 - Put the default styles within App.xaml, put the others styles in another file
#### XA4002 - Within a resource file, declare the elements in the following order
```
<!-- #Constants -->
<!-- #Colors -->
<!-- #Brushes -->
<!-- #Converters -->
<!-- #Objects (such as Data) or commands (for ribbon),etc. -->
<!-- #Styles -->
<!-- #DataTemplates -->
```

## Guideline authors

Please see [repository contributors](https://github.com/cmaneu/xaml-coding-guidelines/graphs/contributors).


## Work in progress

Please see [open issues](https://github.com/cmaneu/xaml-coding-guidelines/issues?state=open).

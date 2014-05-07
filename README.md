XAML Coding guidelines
======================

## How to contribute

You can open an issue on this project to raise an issue/argument about an existing rule, or to submit a new rule. For each submission, please at least produce the following items:

- Cause
- Rule description
- Justification
- How to fix violation

You can also add a code sample with violation, and a code sample with violation fixed.

## Guidelines principles

- **Be easy to follow**: Each rule must be explained as simple as possible. Any developer on his/her 1st day with Xaml must be able to follow these rules,
- **Be as uncontroversial as possible**: These rules must be out of debate. We're not here to determine if it's better to have a white-themed Visual Studio or a black-themed one (Pro-Tip: the correct answer is of course black). So, each rule must have a justification. An inspiration from [StyleCop](http://www.stylecop.com/docs/StyleCop%20Rules.html) rules can be useful,
- **Be usable for any Xaml-Based project**: Windows Phone, WPF or Universal apps. It must apply for all of them. If a rule only apply to one platform, it should go under a platform-specific section.


## Rules


### XA1x. Code readability

#### XA1001 - Put the first attribute on the element line

##### **Cause**
##### **Rule description**
##### **Justification**
##### **How to fix violation**

#### XA1002 - Within an element, order attributes alphabetically or with the proposed solution
#### XA1003 - Put the x:Name or x:Key
#### XA1004 - Put the attached properties at the beginning of the element, eventually after the x:Name/x:Key
#### XA1005 - If an element has no content, use a self-closing element


### XA2x. Naming

#### XA2001 - Name elements with the `x:Name` attribute
#### XA2002 - Use Pascal Casing
#### XA2003 - Suffix XAML names with a type indication
#### XA2004 - Do not use a precise type indication suffix, unless it's required
#### XA2005 - Name only node used in code-behind, element binding or animation



# XA3x. Maintenability

#### XA3001 - Use the rule of 3 to decide if a value must be declared as a resource
#### XA3002 - All the implicit styles must be placed at the top of the file, and must be annotated with a comment



### XA4x. Resource files organization

#### XA4001 - Put the default styles within App.xaml, put the others styles in another file
#### XA4002 - Within a resource file, declare the elements in the following order
#### XA4003 - When defining a SolidColorBrush resource, always define a Color resource as well


## Guidelines authors

Please see repository contributors.

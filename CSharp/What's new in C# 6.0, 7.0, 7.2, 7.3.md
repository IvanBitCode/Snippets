# What's new in C# 6.0, 7.0, 7.2, 7.3

## Out variables
You can now declare out variables in the argument list of a method call, rather than writing a separate declaration statement:

```cs
if (int.TryParse(input, out int result))
    Console.WriteLine(result);
else
    Console.WriteLine("Could not parse input");
```
 
The most common use for this feature will be the `Try` pattern. In this pattern, a method returns a bool indicating success or failure and an out variable that provides the result if the method succeeds.

## Tuples
You may often write methods that need a simple structure containing more than one data element. To support these scenarios tuples were added to C#. Tuples are lightweight data structures that contain multiple fields to represent the data members.
 
You can create a tuple by assigning a value to each member:

```cs
var letters = ("a", "b");
```
 
You can change the syntax to create a tuple that provides semantic names to each of the members of the tuple:
```cs
var alphabetStart = (Alpha: "a", Beta: "b");
```
 
Tuples are most useful as return types for private (user defined types, either classes or structs, are preferred for public APIs) and internal methods. Tuples provide a simple syntax for those methods to return multiple discrete values: You save the work of authoring a class or a struct that defines the type returned. There is no need for creating a new type.
 
The example method below returns the minimum and maximum values found in a sequence of integers:

```cs
private static (int Max, int Min) Range(IEnumerable<int> numbers)
{
    int min = int.MaxValue;
    int max = int.MinValue;

    foreach(var n in numbers)
    {
        min = (n < min) ? n : min;
        max = (n > max) ? n : max;
    }
    return (max, min);
}
```
 
When you call the method, the return value is a tuple whose fields are `Max` and `Min`:

```cs
var range = Range(numbers);
```
 
There may be times when you want to unpackage the members of a tuple that were returned from a method. You can do that by declaring separate variables for each of the values in the tuple. This is called deconstructing the tuple:

```cs
(int max, int min) = Range(numbers);
```
 
The names of tuple elements can be inferred from the variables used to initialize the tuple in C# 7.1:

```cs
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```
 
The C# tuple types now support == and != in C# 7.3.

## Expression-bodied members
Example:
```cs
// Expression-bodied constructor
public ExpressionMembersExample(string label) => this.Label = label;
 
// Expression-bodied get/set accessors.
private string _label;
public string Label
{
    get => _label;
    set => this._label = value ?? "Default label";
}
```

## Expression-bodied function members
The body of a lot of members that we write consist of only one statement that can be represented as an expression. You can reduce that syntax by writing an expression-bodied member instead. It works for methods and read-only properties. For example, an override of `ToString()` is often a great candidate:

```cs
public override string ToString() => $"{LastName}, {FirstName}";
```

## Throw expressions
In C#, throw has always been a statement. Because throw is a statement, not an expression, there were C# constructs where you could not use it.
 
The syntax is the same as you've always used for throw statements. The only difference is that now you can place them in new locations, such as in a conditional expression:

```cs
public string Name
{
    get => name;
    set => name = value ?? 
        throw new ArgumentNullException(paramName: nameof(value), message: "New name must not be null");
}
```

## Null-conditional operators
Null values complicate code. You need to check every access of variables to ensure you are not dereferencing null. The null conditional operator makes those checks much easier and fluid.
 
Simply replace the member access `.` with `?.`:

```cs
var first = person?.FirstName;
```
 
In the preceding example, the variable `first` is assigned null if the `person` object is null. Otherwise, it gets assigned the value of the `FirstName` property. Most importantly, the `?.` means that this line of code does not generate a `NullReferenceException` when the person variable is null. Instead, it short-circuits and produces null.
 
Also, note that this expression returns a string, regardless of the value of person. In the case of short circuiting, the null value returned is typed to match the full expression.
 
You can often use this construct with the null coalescing operator to assign default values when one of the properties are null:

```cs
first = person?.FirstName ?? "Unspecified";
```
 
The most common use of member functions with the null conditional operator is to safely invoke delegates (or event handlers) that may be null. You'll do this by calling the delegate's Invoke method using the ?. operator to access the member.
 
The rules of the `?.` operator ensure that the left-hand side of the operator is evaluated only once.
 
In previous versions of C#, you were encouraged to write code like this:

```cs
var handler = this.SomethingHappened;
if (handler != null)
    handler(this, eventArgs);
 
// preferred in C# 6:
this.SomethingHappened?.Invoke(this, eventArgs);
```

## String interpolation
The string interpolation syntax supports all the format strings available using earlier formatting methods. You specify the format string inside the braces. Add a `:` following the expression to format:

```cs
public string GetGradePointPercentage() =>
    $"Name: {LastName}, {FirstName}. G.P.A: {Grades.Average():F2}";
```
 
The preceding line of code formats the value for `Grades.Average()` as a floating-point number with two decimal places.

You can use string intepolation with @:

```cs
$@"All Grades: {Grades}";
```

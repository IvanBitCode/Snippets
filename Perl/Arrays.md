# Arrays
## Basics
```perl
# Create an array or empty an existing one:
@numbers = ();

# Create an array of numbers:
@numbers = (1,2,3,4,5);
Or
@numbers = (1..5);

# Create an array of strings:
@names = ("luis", "josue", "ivan");
# Or
@names = qw(luis josue ivan);
```

## Get Length Of An Array
```perl
scalar @array
# Or
my $arrSize = @array
```

## Create And Iterate Through A Matrix
```perl
@matrix = (
    ["A", "B", "C"], 
    ["D", "E", "F"]
);
print "$matrix[0][1]"; # Will print B

# Iterate through
foreach $row (@matrix) {
    foreach $elem (@$row) {
        print "$elem ";
    }
    print "\n";
}
```
## More Operations With Arrays
```perl
# Create an array of "hello's":
@array = ("hello") x 10;

# Get an element of an array:
$firstNum = $numbers[0];

# Change an element of an array:
$numbers[0] = 0;
```

## Push, Pop, Shift and Unshift
```perl
# Add an element to the end of an array:
push(@array, "last");

# Remove the last item in the array:
$removedElem = pop(@array);

# Remove the first element of the array and return it:
$removed = shift(@array, "zero");

# Add an element at the beginning of the array:
unshift(@array, "zero");
```

## Merge And Reverse Arrays
```perl
# Merge two arrays:
@numbers1 = (1, 2, 3);
@numbers2 = (4, 5);
@numbers3 = (@numbers1, @numbers2);

# Reverse an array:
@reversed = reverse(@numbers3);
```

## Sorting Arrays
```perl
@numbers1 = (5, 8, 1, 7);
@sorted = sort(@array);
```

Sort function sorts ascendig by default. So previous statements is equivalent to:
```perl
@sorted = sort {$a <=> $b} (@array);
# To sort descending:
@sorted = sort {$b <=> $a} (@array);
```

To sort strings, we use cmp instead of <=>

## Looping Arrays
```perl
@names = ("luis", "josue", "ivan");
foreach $name (@names) {
    print "$name\n";
}
```

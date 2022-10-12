# Hashes

## Basics
Declare an empty hash
```perl
%hash = ();
```

Define fields in a hash
```perl
$hash{firstName} = "John";
$hash{age} = 25;
$hash{city} = "Queretaro";
```

We can also define the key using several words
```perl
$hash{'first name'} = "John";
```

To print an element of a hash
```perl
print "$hash{city}\n";
print "$hash{'first name'}\n";
```

To declare and define a hash
```perl
%hash = (
    'firstName', 'John'
    'age', '25'
    'city', 'Queretaro'
);
```

Or
```perl
%hash = (
    firstName => 'John'
    age       => 25
    city      => 'Queretaro'
);
```

Or
```perl
%hash = qw(
    food meat
    desset donut
    drink coke
);
```

## Looping Hashes: keys, values, each
Iterate through values and keys
```perl
while (($key, $value) = each(%hash)) {
    print "$key - $value\n";
}
```

Iterate through keys
```perl
foreach $key (keys %hash) {
    print "$key\n"; 
}
```

Iterate through values
```perl
foreach $value (values %hash) {
    print "$value\n"; 
}
```

## Hash Functions: exists, defined, delete
Consider the following hash:
```perl
%hash = qw(
    bird albatross
    fish shark
    insect spider
);

if(exists $hash{animal}) {
    print "Key does exists";
} else {
    print "Key doesn't exists";
}
```

Now, add animal element to the previous hash:
```perl
%hash = qw(
    bird albatross
    fish shark
    insect spider
    animal
);
```

The element animal exists but is not defined:
```perl
if(defined $hash{animal}) {
    print "Key defined";
} else {
    print "Key not defined";
}
```

Delete an element of a hash:
```perl
delete($hash{fish});
```

## Hashes: sort, merge
Sort a hash:
```perl
foreach $key (sort keys %hash) {
    print "$key\n"; 
}
```

Merge two hashes:
```perl
%hash1 = qw(
    drink coffee
    sugar 1
    milk yes
);

%hash2 = qw(
    drink coke
    sugar 5
    milk no
);

%hash3 = (%hash1, %hash2);
```

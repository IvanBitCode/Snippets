# Argument Parsing

## @ARGV
The command line arguments are stored in @ARGV array. 

```perl
# To get the first element
$ARGV[0]
# Or
my $first = shift(@ARGV)
# Or
my $first = shift

# Using default values
my $thing = shift(@ARGV) || 'world'
```

## Getopt::Long Library

```perl
use Getopt::Long;

my $data   = "file.txt"; # option var with default string value.
my $length = 24;         # option var with default integer value.
my $pi     = 3.14;       # option var with default real value.
my $help   = '';         # option var with default value (false).

GetOptions("file=s"   => \$data,    # string (arg can start with – or --)
           "length=i" => \$length,  # numeric
           "pi=f"     => \$pi       # real (values can be 3.14 or -6.23)
           "help|h"   => \$help)    # flag with help as name and h as alias.
or die("Error in command line arguments.");
```

Note: each argument can start with - or --.

### : type
If : is used instead of = (for instance: file:s) this means that the argument is optional. If omitted, an empty string will be assignated to string values, and 0 for numeric options.

### Calling function for options

```perl
GetOptions(
        "list_file|l=s" => \$script_list_file,
        "help|h"        => \&usage
) or usage();
```

Function usage() will be called if there is an error when parsing an argument or when the option -h is entered.

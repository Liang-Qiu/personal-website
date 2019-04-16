---
layout: post
title: "Perl Cheatsheet"
---

{{ page.title }}
================
**This is a brief version of https://www.tutorialspoint.com/perl/index.htm**

# Comments in Perl
Lines starting with = are interpreted as the start of a section of embedded documentation, and all subsequent lines until the next =cut are ignored by the compiler.

# Single and Double Quotes in Perl
Only double quotes interpolate variables and special characters such as newlines \n, whereras single quote does not interpolate any variable or special character.

# "Here" Documents
You can store or print multiline text with a great comfort. Even you can make use of variable inside the "here" document. Below is a simple syntax, check carefully there must be no space between the << and the identifier.

An identifier may be either a bare word or some quoted text like we used EOF below. If identifier is quoted, the type of quote you use determines the treatment of the text inside the here document, just as in regular quoting. An unquoted identifier works like double quotes.

# Data Types
Perl is a loosely typed language and there is no need to specify a type for your data while using you program. The Perl interpreter will choose the type based on the context of the data itself.  
Perl has three basic data types: **scalars, arrays of scalars, and hashes of scalars**, also known as associative arrays.

## Scalar:
They are preceded by a dollar sign ($). A scalar is either a number, a string, or a reference.

## Arrays:
Arrays are ordered lists of scalars that you access with a numeric index, which starts with 0. They are preceded by an "at" sign (@).
Example: 
```
#!/usr/bin/perl
@ages = (25, 30, 40);
@names = ("John Paul", "Lisa", "Kumar")

print "\$ages[0] = $ages[0]\n";
print "\$ages[1] = $ages[1]\n";
print "\$ages[2] = $ages[2]\n";
print "\$names[0] = $names[0]\n";
print "\$names[1] = $names[1]\n";
print "\$names[2] = $names[2]\n";
@array = (1, 2, 'Hello');
@array = qw/This is an array/;
```
The line uses the qw// operator, which returns a list of strings, seperating the delimited string by white space.

```
#!/usr/bin/perl

@var_10 = (1..10);
@var_20 = (10..20);
@var_abc = (a..z);

print "@var_10\n";   # Prints number from 1 to 10
print "@var_20\n";   # Prints number from 10 to 20
print "@var_abc\n";  # Prints number from a to z
```
```
#!/usr/bin/perl

@array = (1,2,3);
$array[50] = 4;

$size = @array;
$max_index = $#array;

print "Size:  $size\n";
print "Max Index: $max_index\n";
```
will print
```
Size: 51
Max Index: 50
```

## Hashes:
Hashes are unorderer sets of key/value pairs that you access using the keys as subscripts. They are preceded by a percent sign (%).  
```
#!/usr/bin/perl

%data = ('John Paul', 45, 'Lisa', 30, 'Kumar', 40);

print "\$data{'John Paul'} = $data{'John Paul'}\n";
print "\$data{'Lisa'} = $data{'Lisa'}\n";
print "\$data{'Kumar'} = $data{'Kumar'}\n";
```
will print
```
$data{'John Paul'} = 45;
$data{'Lisa'} = 30;
$data{'Kumar'} = 40;
```
you can also create hashes by 
```
$data{'John Paul'} = 45;
$data{'Lisa'} = 30;
$data{'Kumar'} = 40;
```
or
```
%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40);
```
or 
```
%data = (-JohnPaul => 45, -Lisa => 30, -Kumar => 40);
$val = %data{-JohnPaul};
$val = %data{-Lisa};
```

Perl maintains every variable type in a seperate namepsace. So you can, without fear of conflict, use the same name for a scalar variable, an array, or a slash. This means that $foo and @foo are two different variables.  
Keep a note that this is mandatory to declare a variable before we use it if we use **use strict** statement in our program.

# IF...ELSE
## unless
If the boolean expression evaluates to false, then the block of code inside the unless statement will be executed. If true, then the first set of code after the end of the unless statement will be executed.

# Subroutines
```
#!/usr/bin/perl
# Function definition
sub Hello {
   print "Hello, World!\n";
}
# Function call
Hello();
```
When above program is executed, it produces the following result −
```
Hello, World!
```
## Private Variables
By default, all variables in Perl are global variables, which means they can be accessed from anywhere in the program. But you can create **private** variables called **lexical variables** at any time with the **my** operator.

## Temporary Values via local()
```
#!/usr/bin/perl

# Global variable
$string = "Hello, World!";

sub PrintHello {
   # Private variable for PrintHello function
   local $string;
   $string = "Hello, Perl!";
   PrintMe();
   print "Inside the function PrintHello $string\n";
}
sub PrintMe {
   print "Inside the function PrintMe $string\n";
}

# Function call
PrintHello();
print "Outside the function $string\n";
```
When above program is executed, it produces the following result −
```
Inside the function PrintMe Hello, Perl!
Inside the function PrintHello Hello, Perl!
Outside the function Hello, World!
```

## State Variables via state()
```
#!/usr/bin/perl

use feature 'state';

sub PrintCount {
   state $count = 0; # initial value

   print "Value of counter is $count\n";
   $count++;
}

for (1..5) {
   PrintCount();
}
```
When above program is executed, it produces the following result −
```
Value of counter is 0
Value of counter is 1
Value of counter is 2
Value of counter is 3
Value of counter is 4
```

# References
A Perl reference is a scalar data type that holds the location of another value which could be scalar, arrays, or hashes. Because of its scalar nature, a reference can be used anywhere, a scalar can be used.
```
#!/usr/bin/perl

$var = 10;

# Now $r has reference to $var scalar.
$r = \$var;

# Print value available at the location stored in $r.
print "Value of $var is : ", $$r, "\n";

@var = (1, 2, 3);
# Now $r has reference to @var array.
$r = \@var;
# Print values available at the location stored in $r.
print "Value of @var is : ",  @$r, "\n";

%var = ('key1' => 10, 'key2' => 20);
# Now $r has reference to %var hash.
$r = \%var;
# Print values available at the location stored in $r.
print "Value of %var is : ", %$r, "\n";
```
When above program is executed, it produces the following result −
```
Value of 10 is : 10
Value of 1 2 3 is : 123
Value of %var is : key220key110
```
## References to Functions
This might happen if you need to create a signal handler so you can produce a reference to a function by preceding that function name with \& and to dereference that reference you simply need to prefix reference variable using ampersand &. Following is an example −
```
#!/usr/bin/perl

# Function definition
sub PrintHash {
   my (%hash) = @_;
   
   foreach $item (%hash) {
      print "Item : $item\n";
   }
}
%hash = ('name' => 'Tom', 'age' => 19);

# Create a reference to above function.
$cref = \&PrintHash;

# Function call using reference.
&$cref(%hash);
```
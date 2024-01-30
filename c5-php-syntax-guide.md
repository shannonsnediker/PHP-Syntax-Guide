# PHP Syntax Guide

## Comments

Comments in PHP allow you to documsql
ent your code for better understanding for yourself later and for other people working on your project. You can use them to explain the purpose of your code or to disable specific lines. 

```
/* This is a multi line comment

Meaning it can span multiple lines

Useful for long comments or disabling sections of code
/*
```

`// This is a single line comment`



## Variables
Variables are containers for storing data. They start with a dollar sign $ and are followed by the variable name. These variables can contain different types of data:

- ### string 
    - strings are sequences of characters. You can concatenate them using the '.' operator.
``` 
$recipeTitle = "Chocolate Chip Espresso Scones:" . " Courtesy of Sophia Roe" 

echo $recipeTitle
// output: Chocolate Chip Espresso Scones: Courtesy of Sophia Roe
 ```
- ### integer
    - these are whole numbers and are typically used for mathematical operations
```
// Time of each step represented in minutes
$prep = 10
$chillDough = 30
$shapeBiscuit = 10
$freezeBiscuit = 20
$bake = 20
$totalCookTime = $prep + $chillDough + $shapeBiscuit + $freezeBiscuit + $bake 

echo $totalCookTime
// output: 90
```
- float
    - these are numbers with decimal points
- boolean
    - these represent a logical value and can only have one of two values: true or false. True outputs a value of 1 and false outputs as an empty string.
```
$isCups = true;
$isGrams = false;

echo $isCups
// output:  1
// output: (empty string)


// here I am setting up two variables that will be used in a conditional statement below. Booleans are often used for logical flow of your code. In this case, I am interested in structuring my recipe code to accommodate for two different units of measurement in baking: cups and grams. I'll use a conditional statement to control the flow of my code based on the return value of $isCups or $isGrams.
```
- array
    - one of the more versatile variable types as it can allow you to store multiple values under a single variable name. These values can be all the same datatype such as integer or different such as integer and string.
```
<?php
$ingredientsVolume = array(
    "allPurposeFlour" => "3 cups",
    "butter" => "2 sticks",
    "bakingPowder" => "1 tbsp",
    "bakingSoda" => "1/4 tsp",
    "kosherSalt" => "3 tsp",
    "instantEspresso" => "2 tsp (8g)",
    "sugar" => "1/4 cup",
    "chocolateChips" => "1 cup",
    "buttermilk" => "1 cup"
);

foreach ($ingredientsVolume as $ingredient => $quantity) {
    echo "- $quantity $ingredient\n";
}
?>
```
We'll also create an array for these measurements in weight:

```
<?php
$ingredientsWeight = array(
    "allPurposeFlour" => "438g",
    "butter" => "226g",
    "bakingPowder" => "15g",
    "bakingSoda" => ".25g",
    "kosherSalt" => "18g",
    "instantEspresso" => "8g",
    "sugar" => "50g",
    "chocolateChips" => "170g",
    "buttermilk" => "242g"
);

foreach ($ingredientsWeight as $ingredient => $quantity) {
    echo "- $quantity $ingredient\n";
}
?>
```
Note how instead of calling the variable with echo, we used a foreach loop. More on that below.

- object
    - In PHP, objects aren't necessarily their own variable. Instead, they are an instance of a class. And classes are used to template objects. You can include data (called atrributes) and functions that operate on that data (called methods) within the object. A little confusing, but let's see if we can unpack this. Let's say you want to create a template catch phrase for your biscuits, in case you want to make something other than the espresso chocolate chip. We can create a class for this operation and then create objects, which are instances of the class, to fill in our catch phrase.
```
    class Biscuit { // here we are initializing the class with a name of biscuit
    public $flavor; 
    public $featureIngredient; 
    /* here we are creating two empty variables that allow us to assign data to them later on. In classes, we declare the visibility of a class property or method. Public indicitaes that our properties can be accessed from anywhere in our code (kind of like a global variable) and private would mean its only accessible within the class. Deciding between these two depends on the necessity of maintaining integrity of the class structure; one over the other can reduce the risk of unintended issues. */

    public function setFlavor($flavor) {
        $this->flavor = $flavor;
    } // created a function to set the flavor of the biscuit

    public function setFeatureIngredient($ingredient) {
        $this->featureIngredient = $ingredient;
    } // created a function to set the feature ingredient of the biscuit

    public function getCatchPhrase() {
        return "Today we are baking {$this->flavor} biscuits, and the featured ingredient is {$this->featureIngredient}.";
    } // created a function to create the structure of our catch phrase
}

$lavenderEarlGrey = new Biscuit (); /* created a new instance or object of our Biscuit class called lavenderEarlyGrey. Must be initialized with the keyword "new" */

$lavenderEarlGrey->setFlavor("Lavender Earl Grey"); // called our function setFlavor to set our biscuit flavor

$lavenderEarlyGrey->setFeatureIngredient("bergamont from Italy"); // called to function setFeatureIngredient to set our feature ingredient

echo $lavenderEarlyGrey->getCatchPhrase() . "\n" // display our updated catch phrase
```
- null
    - a variable has no value or has been explicitly set to null. If call a variable and return a value of null when you are not expecting, this indicates an error in your code. Explicitly setting a variable to null can be used in cases where we want to define the data later. We just did this in our class example when we initialied these empty variables:
```
$flavor;
$featureIngredient;
```
- resource
    - This variable represents an external resource such as a databse connection, file handle, or network socket. 

## Echo and Print

Echo and print are used to output data to the screen, they call your variables. Echo and print are more or less the same, however echo returns no value while print returns a value of 1 so it can be used in expressions. We've used echo a lot so far.

### var_dump

Not exactly the same as echo and print, however var_dump is another way to display information about a variable. It provides a detailed representation of the variable, including its data type, length, and value. This function is particularly useful during development when you need to inspect the contents of a variable or understand its structure.

```
var_dump($ingredientsWeight);
/* output:
array(9) { ["allPurposeFlour"]=> string(4) "438g" ["butter"]=> string(4) "226g" ["bakingPowder"]=> string(3) "15g" ["bakingSoda"]=> string(4) ".25g" ["kosherSalt"]=> string(3) "18g" ["instantEspresso"]=> string(2) "8g" ["sugar"]=> string(3) "50g" ["chocolateChips"]=> string(4) "170g" ["buttermilk"]=> string(4) "242g" }
```


## Constants

Constants are identifiers for simple values that don't change throughout the script. They are initialized using the 'define' function

```
<?php

define("MAX_BISCUITS", 12); // Defined a constant for the maximum number of biscuits we can bake in our oven

$numberOfBiscuits = 8; // setting a variable equal to the number of biscuits we are baking

if ($numberOfBiscuits <= MAX_BISCUITS) {
    echo "Let's bake some biscuits!";
} else {
    echo "Too many biscuits! We can only bake up to " . MAX_BISCUITS . " biscuits.";
}

// outputs: Let's bake some biscuits

?>
```


## Operators

Operators are used to perform operations on variables and values. They also assign values to variables and describe their relationship. The most common one and the only one we've used so far is "=".

```
// Arithmetic Operator
$sum = 5 + 3;      // Addition
$difference = 8 - 2; // Subtraction
$product = 4 * 6;   // Multiplication
$quotient = 10 / 2; // Division
$remainder = 7 % 3; // Modulo (remainder)

// Comparison Operator
$isEqual = 5 == '5';    // Equal
$isIdentical = 5 === '5'; // Identical (equal and of the same type)
$isNotEqual = 10 != 8;   // Not equal
$isNotIdentical = 10 !== '10'; // Not identical

Logical Operator
$andResult = true && false; // Logical AND
$orResult = true || false;  // Logical OR
$notResult = !true;         // Logical NOT

Increment and Decrement Operator
$counter = 0;
$counter++; // Increment by 1
$counter--; // Decrement by 1
// these are used in loops
```

## if, else, & elseif

Conditional statements are used to perform different actions based on different conditions.

### if Statement

The if statement is used to execute a block of code if a specified condition evaluates to true.

### else Statement

The else statement is used in conjunction with the if statement. It allows you to specify a block of code to be executed if the condition in the if statement evaluates to false.

### elseif Statement

The elseif statement allows you to specify additional conditions to be checked if the previous if or elseif conditions are false. Its essentially just saying if this then that, if not that, then this. If still not that, then this.

## Functions

Functions allow you to group code into reusable blocks. They can take parameters and return values. We used some functions in our class example. Functions can exist anywhere in your code: inside classes, inside loops, or on their own. 

```
 public function setFlavor($flavor) {
        $this->flavor = $flavor;
    } // created a function to set the flavor of the biscuit
```

## Arrays

As mentioned, arrays are variables so they are containers for storing data. Arrays stand out from other variables because they can really help create a more sophistiicated and fluid application. You can store multiple values in a single variable. We created associative arrays to store our ingredients list: see below.

### Indexed Arrays

Indexed arrays are the most basic type of arrays in PHP. Elements are assigned numeric indices starting from 0 and incrementing by 1 for each subsequent element. Accessing elements is done using these numeric indices.

### Associative Arrays

Associative arrays use named keys (strings) to associate values with specific identifiers. Each element in an associative array is a key-value pair.

```
$ingredientsVolume = array(
    "allPurposeFlour" => "3 cups", /// allPurposeFlour is our key and 3 cups is our value
    "butter" => "2 sticks",
    "bakingPowder" => "1 tbsp",
    "bakingSoda" => "1/4 tsp",
    "kosherSalt" => "3 tsp",
    "instantEspresso" => "2 tsp (8g)",
    "sugar" => "1/4 cup",
    "chocolateChips" => "1 cup",
    "buttermilk" => "1 cup"
);

```

### Multidimensional Arrays

Multidimensional arrays are arrays containing one or more arrays as their elements. They can be two-dimensional, three-dimensional, or even more.

### Empty Arrays

I want to mention empty arrays because they have so much use in an application. An empty array isn't necessarily a distinct PHP element persay, but it can serve as a dynamic container for collecting or receiving data within our code. 

Let's say you have a function that is expected to return a data set, initializing an empty array provides a placeholder for where that data can go when the function executes. This is particularly handy when the data returned from the function needs to be passed on to other functions or uses throughout the application. 

## Loop

Loops are used to execute the same block of code multiple times. 

Loops are used in conjunction with arrays quite a lot. Echo is great for calling on single variables, but if you want to call an array with echo, it will treat the entire array as one variable and output as a single string. It will also include additional data like so:

If you use a loop, you can iterate through your array and output each individual element. It makes your code a lot more readable and useable for other parts of your application. 

In order to display our arrays in our biscuit example we had to create a loop to iterate through each element to ouput each one to the screen. 

```
$ingredientsWeight = array(
    "allPurposeFlour" => "438g",
    "butter" => "226g",
    "bakingPowder" => "15g",
    "bakingSoda" => ".25g",
    "kosherSalt" => "18g",
    "instantEspresso" => "8g",
    "sugar" => "50g",
    "chocolateChips" => "170g",
    "buttermilk" => "242g"
);

foreach ($ingredientsWeight as $ingredient => $quantity) {
    echo "- $quantity $ingredient\n";
}
```

## List() 

A quick aside about the operator list(). Remember earlier when we said operators are used to perform operations on variables and values? These are essentially a set list of pre-determined operations designed into php. While we are on the topic of access elements in an array. There is a way to echo each element in an array using the list() operator. The list() construct in PHP is designed to work with indexed arrays. When you use list() with an indexed array, the elements are assigned to variables in the order in which they appear in the array. The variables take on the values of the corresponding elements based on their numeric indices. Then you can echo each array element since it is now been assigned to its own variable. 



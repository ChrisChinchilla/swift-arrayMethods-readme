# Array Methods

![Drawing](http://www.achievement.org/achievers/ang0/large/ang0-003.jpg)

> We delight in the beauty of the butterfly, but rarely admit the changes it has gone through to achieve that beauty.

## Learning Objectives - The student should be able to..

- `append()` - add element to the end of the array.
- `insert(_:atIndex:)` - insert an element at the specified index.
- `removeAtIndex()` - remove an element at the specified index.
- _Subscript Syntax_ to change elements at a specified index and access the element at a specified index to store in a variable.

```swift
var numbers = [5, 2, 3]
numbers[0] = 1

let thirdNumber = numbers[2]
// 3
```

- `count` - Returns the number of elements in the array.
- `isEmpty` - Returns true if the array is empty.

## What the student can do at this point

- Create variables and constants
- Is familiar with type annotations, type inference and string interpolation.
- Can create functions with return types.
- Is familiar with the String, Int, Double, and Bool type.
- Can perform arithmetic operations on Int and Double.
- Understands if and else clause statements.
- Can create and use Arrays.
- Can iterate over an Array using a for-in loop.
- Can iterate over an Array calling enumerate().

## Outline / Notes

- The student will not have read about structs or classes (yet) so I don't want to go too deep in an explanation of computed properties and instance methods but I think we might need to give them a short definition as they will be using them fully in this reading.
- I think it's important for them to know that they must use var here in that we need the array to be mutable in order to add anything to it. Show them a screenshot of the error they would receive if they tried using append where toys would be declared with let.

```swift
 var toys = ["Woody", "Buzz Lightyear", "Mr. Potato Head", "Slinky Dog"]
 toys.append("Rex")

 // ["Woody", "Buzz Lightyear", "Mr. Potato Head", "Slinky Dog", "Rex"]
```

- Speaking about the `insert(_:atIndex:)` method. I think it's important for them to see and recognize that calling the method like I did below inserting an element at index 0 will NOT replace the element that is currently there, it will insert it at that specific index and shift everything to the right.

```swift
 toys.insert("Tom Hanks", atIndex: 0)

 // ["Tom Hanks", "Woody", "Buzz Lightyear", "Mr. Potato Head", "Slinky Dog", "Rex"]
```

- They can then remove an element at a specified index consideirng now that Tom Hanks is not a character in the film, he is the voice of Woody.... so we need to remove him.

```swift
 toys.removeAtIndex(0)

 // ["Woody", "Buzz Lightyear", "Mr. Potato Head", "Slinky Dog", "Rex"]
```

- If instead they wanted to change an element at a specific index, they would so so as follows:

```swift
 var names = ["James", "Sarah", "Bran", "Sansa"]

 names[0] = "Jim"

 // ["Jim", "Sarah", "Bran", "Sansa"]
```

- I think it's important for them to see the error they would receive IF they tried updating a value at a certain index that is out of bounds. Or if they try accessing an element that could be out of bounds. They might then wonder HOW they can in fact make sure they are within bounds and we COULD show them this but I'm very very reluctant in explaining to them exactly what is going on here as the next lesson will introduce optionals (which is usually the hardest thing for them to grasp). **OPINION WANTED**: Do you think we should at the very least show them something like this?:

```swift
 if let index = names.indexOf("Jim") {
    names.removeAtIndex(index)
 }

 // ["Sarah", "Bran", "Sansa"]
```

- Referring to `count`, they should be exposed to the following where it is explained thoroughly what is going on:

```swift
let rainbowColors = ["Red", "Orange", "Yellow", "Green", "Blue", "Indigo", "Violet"]

 let numberOfColors = rainbowColors.count
 // 7

 print("There are \(numberOfColors) colors in the rainbow.")
 // prints "There are 7 colors in the rainbow.

 if rainbowColors.count > 5 {
    print("There are more than 5 colors in a rainbow.")
 }
 //prints "There are more than 5 colors in a rainbow."
```

- Referring to `isEmpty` - I like the idea of stepping them through the following two examples:

![deliLine](http://i.imgur.com/ivgaSon.png?1)

```swift
 var deliLine = [
    "Albert Einstein",
    "Isaac Newton",
    "Galileo Galilei",
    "Marie Curie"
 ]

 if deliLine.isEmpty {
    print("The deli line is empty")
 } else {
    print("There are people waiting to eat!")
 }

 // prints "There are people waiting to eat!"
```

![Moons](http://i.imgur.com/reNsnn6.png?1)

```swift
 let moonsOfJupiter = [
    "Europa",
    "Ganymedge",
    "Io",
    "Callisto"
]

 if !moonsOfJupiter.isEmpty {
    for moon in moonsOfJupiter {
        print("\(moon) is a moon orbiting Jupiter.")
    }
 }

 // Europa is a moon orbiting Jupiter.
 // Ganymede is a moon orbiting Jupiter.
 // Io is a moon orbiting Jupiter.
 // Callisto is a moon orbiting Jupiter.
```

--------------------------------------------------------------------------------

In Unit 1 you saw the following:

```swift
let greeting = "Hello"
let loudGreeting = greeting.uppercaseString

print(loudGreeting)
// prints "HELLO"
```

This was an example of a 'method', which can be thought of as a pre-written function that helps you accomplish common tasks.

You also saw `.append` in the last lesson, which is another method. Whilst there are some common methods, many are contextual and only work on particular types. For example, a method like `.append` that works on an array will not work for a String, and `.uppercaseString` will not work on an array.

The `.append()` method adds a value to the end of an array. You could achieve this in several ways which would involve far more code and calculation, I think you'll agree that `.append()` is far more convenient. There are many other methods for arrays, and in this lesson you'll look at some others.

## Enumeration

Before going any further, there's one other array concept to introduce.

Say you have an array of string literals which represent a list of instructions to create great tea. If you want to print these instructions, you would need to do the following:

```swift
var toMakeTea = [
    "Boil Water",
    "Add tea bag to cup",
    "Wait ten minutes",
    "Add Milk",
    "Drink"
]

print("1\. \(toMakeTea[0])")
print("2\. \(toMakeTea[1])")
// and so on

// prints "1\. Boil Water"
// prints "2\. Add tea bag to cup"
// etc
```

This way of accomplishing the task is incredibly tedious. Knowing how a `for-in` loop works, you can iterate over each value in the array of strings. You also the index of the value in the array because you want to display numbered instructions.

If steps need to be added, removed, or changed at a particular index in the array, then you also need to know what the index of the value is. When you have a simple list of unchanging values, then maybe this is simple, but with a larger list processed in a loop, there is another way, the `.enumerate` method that you call on an array variable.

```swift

for (index, step) in toMakeTea.enumerate() {
    print("\(index + 1). \(step)")
}

// 1\. Boil Water
// 2\. Add tea bag to cup
// 3\. Wait ten minutes
// 4\. Add Milk
// 5\. Drink
```

In this example you first create an array of the steps to make tea (and yes, there are intentional mistakes!) and add a couple of extra things to the `for in` loop. First inside the brackets you add variables to hold the index and value variables, the names of these are up to you. Using `index` is of course a useful name, but you can call it whatever you want. At the end of the array variable you want to iterate through, add the `.enumerate()` method. Now inside the loop you have access to the value in the current iteration as well as it's index in the array. Above, you add '1' to the index value as unlike computers, humans don't count from 0!

## Check an array has values

Before undertaking any further actions, it's a good idea to check the array you would like to work with actually has any values in it. Of course there's a method to help, `.isEmpty`.

```swift
if toMakeTea.isEmpty {
   print("No tea yet :(")
} else {
   print("Ready to make tea! :)")
}

// prints "No tea yet :("
```

This method checks to see if the array contains any values, but the array still needs to actually exist (i.e. it's you have initiated it) in the first place.

![Array not Initialized](not-init.png)

It might be a good idea to add this check to your array before any other functionality we look at in the rest of the lesson, wrapping it in `if else` statements.

You can reverse a logical check with the `!` symbol:

```swift
if !toMakeTea.isEmpty {
    print("Ready to make tea! :)")
} else {
    print("No tea yet :(")
}
```

This may seem confusing syntax, but it may feel more natural to start with a preferred or default status and then handle the alternative or fallback status.

## Array Size

There are some methods that help you access certain properties of an array, one is to find the size of an array, or the number of values it contains.

```swift
print(toMakeTea.count)
// 5
```

Just to confuse matters, `.count` returns the number of items in an array starting from 1, not 0\. This makes sense, but might confuse you the first few times you use the method.

As you try some of the other methods mentioned in the rest of this tutorial, try printing `count` throughout your code to see the affect on the array size.

## Add Items to an Array

You saw this method in the last lesson, but let's quickly look at it again. You missed an important step in the list above, telling people to enjoy their tea, so add it to the end of the array:

```swift
toMakeTea.append("Enjoy!")
print(toMakeTea)
// ["Boil Water", "Add tea bag to cup", "Wait ten minutes", "Add Milk", "Drink", "Enjoy!"]
```

The `.append()` method adds a new value (which has to also be the same type as every other value) to the end of the array.

You have also forgotten an important step at the beginning of the list, adding water to the kettle, so let's add it:

```swift
toMakeTea.insert("Add water to kettle", atIndex: 0)

print(toMakeTea)
// ["Add water to kettle", "Boil Water", "Add tea bag to cup", "Wait ten minutes", "Add Milk", "Drink", "Enjoy!"]
```

Note that this doesn't replace the item at index `0`, but **inserts** it, shifting all the elements to the right of it one place in the index.

## Change items in an array

Uh oh, unless you like strong tea, waiting ten minutes is way too long, so let's change that value:

```swift
toMakeTea[3] = "Wait 3-5 minutes"

print(toMakeTea)
// ["Add water to kettle", "Boil Water", "Add tea bag to cup", "Wait 3-5 minutes", "Add Milk", "Drink", "Enjoy!"]
```

In this example, you use similar syntax from lesson xx to assign the string of text on the right hand side of the `=` to the index in the array on the left hand side, in this case, position `3`.

## Removing items from an array

Drinking tea is a serious business, so you've decided to remove the 'Enjoy!' step. Setting that index in the array's value to be empty, i.e. "", is not enough to remove it, but there's a method that helps.

```swift
toMakeTea.removeAtIndex(6)

print(toMakeTea)
// ["Add water to kettle", "Boil Water", "Add tea bag to cup", "Wait 3-5 minutes", "Add Milk", "Drink"]
```

The `removeAtIndex()` method removes the value in the array at position 6 and then shuffles all the items to the right of the value to the left, which in this case, is no items.

Note that if you try to access or change the value of an index in the array that doesn't exist, you will receive an error. Try these commands in a Playground and see:

```swift
toMakeTea.removeAtIndex(6)
print(toMakeTea[6])
// Error
toMakeTea.removeAtIndex(6)
// Error
```

To prevent this error, you could combine the code above with some `if else` statements and the `count` method you saw earlier in the lesson. For example:

```swift
if toMakeTea.count > 6 {
    toMakeTea.removeAtIndex(6)
} else {
    print("There is no value at index 6")
}
```

This checks to see if the size of the array is greater than 6, and if so removes the value at index 6.

[View this lesson on Learn.co](https://learn.co/lessons/ArrayMethods)

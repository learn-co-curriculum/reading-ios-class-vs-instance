# Class vs Instance

## Objectives

1. Read about the influence of Simula and Smalltalk upon object-oriented programming.
2. Distinguish class methods from instance methods.
3. Distinguish classes from instance objects with the "factory" metaphor.

#### Advanced

1. Get introduced to the idea of the class object.

## Battleship!

*That's what a ship is, you know. It's not just a keel and a hull and a deck and sails. That's what a ship needs. But what a ship is...what the* Black Pearl *really is...is freedom.*  
—Jack Sparrow, [*The Pirates of the Caribbean (2003)*][imdb_potc]

[imdb_potc]: http://www.imdb.com/title/tt0325980/?ref_=nv_sr_2

If we were to write a program that simulates naval combat, we might start by creating a `ship` object with properties that detail all of the data for a naval warship: `name`, `rating`, `shipClass`, `length`, `beam`, `keel`, `displacement`, `captain`, `crew`, `topSpeed`, `currentSpeed`, `heading`, `hullCondition`, `armament`, `ammunition`, `rumSupply`, and so on. 

What if we had to manually declare the value of *every* property for *every* warship that we wish to have in our simulation program? That's a lot of variable declarations! But every warship in our simulation will have data for each of these fields; it would save us a lot of work if we could find some way of creating a "warship" template, and then populate the data for the properties of each separate warship whenever we copy the template.

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/battle_group_alpha.jpg)  
—*Battle Group Alpha (*Midway*,* Iowa*) underway, 1987*, [image by US Navy](https://en.wikipedia.org/wiki/File:Battle_Group_Alpha_(Midway,_Iowa)_underway,_1987.jpg)

This is exactly what [Ole-Johan Dahl][ojd] and [Kristen Nygaard][kristen_nygaard] realized as they worked on developing the [Simula I and Simula 67 languages][simula] in the 1960s. Simula introduced the concept of **class** and **instance** (among other breakthroughs), and was a language that was instrumental in the development of [Smalltalk][smalltalk], the first fully-realized object-oriented programming language, at [Xerox PARC][parc] in the 1970s.

[ojd]: https://en.wikipedia.org/wiki/Ole-Johan_Dahl
[kristen_nygaard]: https://en.wikipedia.org/wiki/Kristen_Nygaard
[simula]: https://en.wikipedia.org/wiki/Simula
[smalltalk]: https://en.wikipedia.org/wiki/Smalltalk
[parc]: https://en.wikipedia.org/wiki/PARC_(company)

If we can set up the template for the warships (let's call it "Warship", capitalized), then we've outlined the data points that are necessary for creating an individual "warship" (lowercase). In the object-oriented paradigm, the template "Warship" is referred to as the `Warship` **class**, and all individual "warship"s created from the "Warship" template are referred to as **instances** of the `Warship` class.

Maritime tradition often uses similar language when describing the design form (or "class") of a ship. The [USS *New Jersey* (BB-62)][uss_new_jersey], for example, is an [*Iowa*-class battleship][iowa_class]; the ship class being named after that design's "lead ship", or first constructed ship, in this case, the [USS *Iowa* (BB-61)][uss_iowa]. Two other *Iowa*-class battleships were commissioned by the U.S. Navy, the [USS *Missouri* (BB-63)][uss_missouri] and the [USS *Wisconsin* (BB-64)][uss_wisconsin]. For our purposes, we could describe each of the four battleships as **instances** of the "*Iowa*-class battleship" **class**.

[iowa_class]: https://en.wikipedia.org/wiki/Iowa-class_battleship
[uss_iowa]: https://en.wikipedia.org/wiki/USS_Iowa_(BB-61)
[uss_new_jersey]: https://en.wikipedia.org/wiki/USS_New_Jersey_(BB-62)
[uss_missouri]: https://en.wikipedia.org/wiki/USS_Missouri_(BB-63)
[uss_wisconsin]: https://en.wikipedia.org/wiki/USS_Wisconsin_(BB-64)

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/USS_Missouri_transfers.JPG)
—*USS Missouri (BB-63) (at left) transferring personnel to USS Iowa (BB-61), while operating off Japan on 20 August 1945.*, [image by US Navy](https://en.wikipedia.org/wiki/File:USS_Missouri_transfers.JPG)

**//Flat-fact:** *The* Iowa*-class was the largest and final battleship design of the US Navy, whose four ships saw intermittent service from 1943 until 1992, a span of nearly fifty years. Between them, they participated in five US wars (including the Cold War) and the* Iowa*-class is the only WWII ship class whose entire membership still survives. Each of the four ships were donated by the US Navy to preservation society who maintain them in maritime museums across the United States.*

All four of the individual battleships may have slight differences in measurements, but each share a common set of attributes such as having a length of 887 feet (270 m), a beam of 108 feet (33 m), nine 16-inch primary guns, and twenty 5-inch secondary guns. While their individual displacement tonnage, crew complements, and specific armaments varied across their service careers, the specific values of these "properties" are not part of what defines each ship as an *Iowa*-class battleship, but rather, the *possession* of these attributes is what does.

## Class Methods vs Instance Methods

Do you recall from the previous readings the mention of a difference between the `-` or `+` prefix in a method declaration? You may recall the explanation of the `+alloc` and `-init` method pair, with `alloc` being a *class* method and `init` being an *instance* method that you should have used a few times by now.

```objc
// class name,  instance object, class object,  class method, instance method 
NSMutableArray *mutableArray = [[NSMutableArray alloc]        init];
```

Even though you've only written or edited *instance* methods at this point, you should have called a handful of *class* methods by now including the `alloc` method and perhaps the `arrayWithArray:` method on `NSMutableArray`. **Class methods** are precisely what their name implies: methods that are performed by the class. 

### Manufacturing Instance Objects

![](https://curriculum-content.s3.amazonaws.com/ios/ios-intro-to-objects-unit/ios-intro-to-objects-unit/who_makes_all_these.gif)

A class, essentially, is the "factory" for creating instance objects based upon that class's template. The `NSString` class is responsible for generating every *instance* of an immutable string object that your application requires, while the `NSMutableString` class generates every *instance* of a mutable string object. Similarly, the `NSArray` class generates immutable array instances, and the `NSDictionary` class generates immutable dictionary instances. 

While the class is said to "manufacture" its instance objects, the common factory metaphor is not the best image in some ways. It's perhaps better to visualize the class as the instrument in a manufacturing process that holds the form of the product, such as the die of an injection mold or the plate in a printing press.

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/yuan_dynasty_banknote.jpg)  
—*A Yuan dynasty printing plate and banknote*, [Wikimedia Commons][yuan_banknote]

[yuan_banknote]: https://commons.wikimedia.org/wiki/File:Yuan_dynasty_banknote_with_its_printing_plate_1287.jpg

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/casting_tin_soldiers.jpg)  
—*The permanent molding process.*, [Wikimedia Commons][casting_tin_soldiers]

[casting_tin_soldiers]: https://en.wikipedia.org/wiki/File:Castingtinsoldiers.jpg

In this metaphor, it's easy to see the class as distinct from the instances that it creates—but yet, there's an inseparable relationship between the two: the shape of the template and of the mold are based upon the needs of how the print or the product will be used, and any changes made to the template or to the mold will be reflected on the printed page or in the product's shape.

It's also easy to imagine how classes aren't used to hold data, but rather to give structure to how the data should be held by an instance: it would be silly, for example, to try painting the inside of the mold while expecting the artwork to transfer to every one of the casted toys. No, each casted toy must be awarded its own coat of paint.

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/toy_soldiers.jpg)
—*54mm Toy Soldiers representing the British Coldstream Guards during the Crimean War era* by Imperial Productions, Greytown, New Zealand. Photo by J. Corey Butler, 2005. [Wikipedia Commons](https://commons.wikimedia.org/wiki/File:Toy_Soldiers_British_Coldstream_Guards.jpg)

In the same way, setting up a class file is like creating a template or a mold in code. It's not until an instance object of that class is created (or "manufactured") that we have the print or the product to apply to its intended purpose.

## Advanced

### Classes are ~~People~~ Objects, Too

You may have wondered, "how can a class perform a method if only objects are capable of performing methods?" It's not a case of the chicken or the egg: it's because classes are objects too. More specifically, each custom class file generates exactly one **class object** as part of loading the application at run time. It's the class object which performs the `alloc` method when creating an *instance object* of that class. 

**//Flat-fact:** *The class objects for Apple's frameworks (libraries) actually live within the iOS operating system and get initialized when the device starts up. Because they're a part of the operating system, they're available to any application that runs on the device.*

These class objects for custom classes and imported frameworks (such as the Specta and Expecta libraries in the testing suite) get initialized when the application is launched. The result of this is that a class "template" object for every object that you might create an instance of in your application is prepared before the application itself gets to do anything.

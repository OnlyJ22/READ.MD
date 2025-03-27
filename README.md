https://my-food-ranking.netlify.app/

https://www.thecsharpacademy.com

https://learn.microsoft.com/en-us/training/courses/az-140t00

https://algomap.io

sample pc build 
https://pcpartpicker.com/list/cNLjRV

<field name="XMLTZone">
    <![CDATA[
        <timeZoneRule>
            <standardBias>480</standardBias>
            <additionalDaylightBias>-60</additionalDaylightBias>
            <standardDate>
                <transitionRule month="11" day="su" weekdayOfMonth="first"/>
                <transitionTime>02:00:00</transitionTime>
            </standardDate>
            <daylightDate>
                <transitionRule month="3" day="su" weekdayOfMonth="second"/>
                <transitionTime>02:00:00</transitionTime>
            </daylightDate>
        </timeZoneRule>
    ]]>
</field>

Event.ts line 88

    public XMLTZone: string = '';  // Add this line

    constructor(author?: User, editor?: User, created?: Moment, modified?: Moment, id?: number, uniqueId?: Guid, etag?: number) {
        super(author, editor, created, modified, id, uniqueId, etag);

        this.XMLTZone = ''; // Initialize XMLTZone field
onlineEventServies line 85 

public track(event: Event): void;
public track(refiner: Refiner): void;
public track(refinerValue: RefinerValue): void;
public track(approvers: Approvers): void;
public track(entity: Event | Refiner | RefinerValue | Approvers): void {
    if (entity instanceof Event) {
        entity.XMLTZone = entity.XMLTZone || '';  // Ensure XMLTZone is set before persisting
        this._eventLoader.track(entity);
    } else if (entity instanceof Refiner) {
        this._refinerLoader.track(entity);
        entity.values.forEach(value => this.track(value));
    } else if (entity instanceof RefinerValue) {
        this._refinerValueLoader.track(entity);
    } else if (entity instanceof Approvers) {
        this._approversLoader.track(entity);
    }
}

onlineEventServices line 403

 createSampleEvents: async () => {
                console.log(`Starting 'createSampleEvents()'`);

                const refiners = await this._refinerLoader.all();

                const { currentUser } = this._directory;

                const events: Event[] = [];

                const timeZoneXML = `<![CDATA[
                    <timeZoneRule>
                        <standardBias>480</standardBias>
                        <additionalDaylightBias>-60</additionalDaylightBias>
                        <standardDate>
                            <transitionRule month="11" day="su" weekdayOfMonth="first"/>
                            <transitionTime>02:00:00</transitionTime>
                        </standardDate>
                        <daylightDate>
                            <transitionRule month="3" day="su" weekdayOfMonth="second"/>
                            <transitionTime>02:00:00</transitionTime>
                        </daylightDate>
                    </timeZoneRule>
                ]]>`;

                {
                    const event = new Event();
                    event.snapshot();
                    event.title = "North America East Quarterly Connect - Broadcast";
                    event.start = now().add(2, 'days').startOf('day').add(10, 'hours');
                    event.end = event.start.clone().add(2, 'hours');
                    event.location = "Online Teams Meeting";

                    for (const refiner of refiners)
                        event.refinerValues.add(refiner.values.get()[0]);

                    event.moderator = currentUser;
                    event.moderationTimestamp = now();
                    event.moderationStatus = EventModerationStatus.Approved;

                    // ADDING XMLTZone FIELD
                    event.XMLTZone = timeZoneXML; 

                    events.push(event);
                    this.track(event);



Using the transcript I provided create a lesson plan for each break it down in sections and correct any mistakes and explain it simple and straight forward 

this is everything you need to know about c-sharp in one video C sharp is part of the C family of programming languages so basically it has curly brackets and semicolons it was developed by Microsoft but it's now fully open source and cross-platform you can build c-sharp applications to run on Windows on Linux on Mac on mobile thanks to xamarin and even in webassembly thanks to Blazer here is a c-sharp application that calls a function you can see the function has a return type of void and then a name and then some arguments the body of the function is enclosed in these curly brackets here and each line is ended with a semicolon functions can also be static with a static keyword like this comments in C sharp begin with two forward stashes like this variables you use to declare variables by writing the type and then the variable name but these days c-sharp developers will almost exclusively use VAR everywhere VAR in C sharp is not the same as VAR in JavaScript it does not mean that you can put any type into this variable VAR simply means that you just want the compiler to work out what the type is for you here if I hover over this variable you can see that the compiler has worked out that this is a string and this one down here if I hover over this this is a number this is called implicitly typed variable implicit typing is good to use it there are a bunch of built-in data types in c-sharp and they're fairly similar to those in other programming languages so that's integers floating Point numbers strings that sort of thing but you can also create your own data types there are three ways to create data types in c-sharp classes structs and records records are quick and easy way to represent the shape of some data so they are fields which you declare like this in Brackets after the record name they're also immutable so once you've created this record you can't change it structs are for storing more primitive data types and the main advantage of a struct is that that exists on the execution stack of your program so it's not stored in Heap memory and given a pointer like other objects the whole struct is stored in that memory that your thread is given to run with so for small data types structs a much more efficient way to store readily accessible values in memory the third type of data type in c-sharp is by far the most common and that is the class many programming languages have classes and those in c-sharp are not much different classes are defined with the class keyword and they can have one of five access modifiers that Define the visibility of the class public means this is visible to everyone everywhere private means just within the scope of whatever was declaring this class protected is the declaring scope and anything that's inherited from it internal means Justice assembly and file means just this file classes can have methods like this one and methods can have their own access modifiers as long as they are more restrictive than that of the class so you can't have a public method on a private class basically you can also inherit classes and there's a special keyword called abstract which denotes that this class is only for inheriting you can put abstract on the class name itself and then on any method if you want to force this method to be implemented in any overriding class classes can also Implement as any interfaces as you like an interface is declared with the word interface and it just defines methods and properties that the implementing classes must contain and while we're on the subject of properties c-sharp has a really nice shorthand Syntax for declaring Properties by using these get and set keywords here you can actually expand out these gettings and Setters if you want to by adding some custom logic in there but by default you just need to like get and set and the compiler will create the property for you it's also worth noting that you can add restrictive access modifiers onto these Getters and Setters as well there's also this really useful shorthand for read only properties the arrow here is telling it to create a read-only property that returns this value so doing this is the equivalent to writing out the full getter like this c-sharp has got loads of cool features like this that will save you time and it will keep the amount of code you write to an absolute minimum which is good another thing classes have is Constructors and destructors a Constructor takes a bunch of parameters into the class when a new instance is created and a deconstructor spits out a bunch of parameters from within the class you use a Constructor when you want to create a new instance of the class with the new keyword so you do the new keyword like this and you pass in any values onto the Constructor to use a deconstructor you simply wrap the variables you want in deconstruct into brackets like this and C sharp knows to use that deconstruct method that you created to create the values from the class record types can be deconstructed like this as well just completely out the box you don't need to implement any methods for them so that's all of the object oriented stuff in C sharp what about the actual control flow of your program Well Control statements in C sharp include if which is written with the condition in Brackets and then else which comes after an f and you can chain else and if together to create an else if statement the curly brackets in if statements are required if you have more than one line of code inside the statement as well as if statements we also have the switch statement and this is how we do pattern matching you can Define each case as a constant like this but also you can put conditions in here so here we're going to drop into this case if our variable is anything above 10. the switch statement can be written like this but it can also be written like this with our conditions inside the curly braces down here this is just one of the ways that c-sharp has been introducing much more functional programming Concepts into its syntax over recent years this way of writing a switch statement is much more declarative and this will be familiar to you if you've done more functional programming in other languages so it's nice that C sharp gives us this choice of how we want to style our code you also have for loops and do while loops and the most common type of loop which is the four each for each will iterate over every element in an iterable collection if you know JavaScript then it's worth pointing out that the 4-H deep uses in here the same way that JavaScript uses off so that's nice and confusing but the compiler will help you a lot if you get it wrong and if we're going to write a loop then we should probably also look at collection types c-sharp has arrays which are declared like this but it also has a whole bunch of collection data types in the system.collections namespace you import a namespace by adding the using directive to the top of a file so by using system.collections then we can go ahead and create instances of some of these collections so there's like the list and there's a dictionary and there's a cue all of these collection methods and the array Implement an interface called I enumerable ironumable is the interface that the for each statement looks at to decide if something can be used in a for Loop and you can create your own class that implements are enumable if you want to you can also create a function that returns are innumerable and generates results of that function using the yield statement here we have a function that uses the yield statement to create an infinite array so that's kind of cool it's more often used to defer the execution of some code while iterating over a data set here we're only performing this calculation as and when this collection is iterated over so we can create much more efficient mapping functions and things that act on large arrays by using ironumable and yield c-sharp comes included with a bunch of functions that you can use on inumable collections such as select which is basically a map in other languages and aggregate which is a reduced function C sharp also supports the use of async and awaits to control asynchronous code execution you use these by adding async to the function name and then calling a weight inside the function whenever you want to await the execution of another asynchronous piece of code generics have also included in C sharp they're used with the triangle brackets like this on any function name or class definition you can use the keyword where after the argument list to add restrictions onto your generic type argument so here we're saying this generic type argument T has to be something that implements this interface and that's all the language features that we're going to go over if you want to get started writing C sharp today then go and grab an IDE install.net and get going the IDE for writing C sharp is traditionally Visual Studio but increasingly these days people are using more lightweight Visual Studio code and also this IDE called Ryder from jetbrains so go grab any of these create a new c-sharp console application by hitting.net new console on the command line and start playing Miranda C sharp yourself don't forget to subscribe to my channel I'll be publishing a few more videos soon about c-sharp and some of the cool things that you can do with it so stay tuned for that and if you've got any questions of course pop them in the comments section below my name is James charlesov and I'll see you in the next video on the train to code YouTube channel [Music] 
                    

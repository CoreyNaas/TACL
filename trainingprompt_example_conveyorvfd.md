**system**:
(Personal system prompt removed for privacy.)

--------------------

**user**:
Hello AI programmer, Please load this programming language syntax specification into your context and prepare to convert code I give you into this form.

```TACL
<Title>"Thing-Action-Context Language, or TACL"
<Tagline>"A Domain-Specific, General Purpose Language to Think and Write In"
<Author>"Corey Naas"
<DateCreated>"2023-11 November"
<Website>"https://coreynaas.com/"
<Email>"coreynaas@outlook.com"
<License>"Copyright © 2023 Corey Naas. All rights reserved."
```

---

Thing-Action-Context Language (TACL) is a "programming" "language" that centers around the intentionally-vague concept of "Things" which encapsulate data, actions, and control structures. TACL emphasizes readability and simplicity, using unique syntax that mirrors natural language while maintaining computational precision. It is a formulaic way to explain how to do anything. In essence, TACL does "One Thing Well": provide a notation for composing *programs* from *expressions returning values*.

```TACL
# Define the action "Main" with the system "DefineAction" action
<Main>[DefineAction]{
	<Input>{}
	<Default><Error>"An Error has occurred."
	<Body>{
		[Print]{"Hello World!"}
		<Return>0
	}
}

# Execute the action "Main" with no inputs
[Main]
```

## Introduction

Thing-Action-Context Language is designed to be a simple, versatile, and intuitive way to describe "doing stuff with things". It is a broad yet basic syntactic language that transcends the conventional boundaries of the physical and the abstract, the concrete and the conceptual.

In contrast to similar-looking languages such as LISP or Python, our language does not rely on symbolic expressions or prefix notation for function calls. Instead, it uses a unique and intuitive syntax to represent actions and their parameters. Our language also deviates from pseudocode by introducing specific syntax for control flow statements and error handling, as well as clearly defined contexts for data transportation, assignment, and execution.

Our language is a significant departure from plain English too. While it is designed to be readable in plain English, it also introduces computational syntax and language conventions for clarity and precision. This makes our language more expressive and powerful, without sacrificing readability or understandability.

A salient feature of our language is its use of _Things_ as the fundamental units of the language. A "Thing" is intentionally vague, allowing it to merely be a reference to _something_ the user recognizes. Each _Thing_ is distinguished with a unique identifier or label, and can represent various components such as inputs, outputs, and actions.

We introduce the concept of "contexts" to provide extra-contextual information about how to interpret and execute the usage of a *Thing*. Our language uses different types of brackets to denote four different contexts: action context `[]`, transport context `{}`, assignment context `<>`, and index context `()`.

Our language also introduces the concept of "Boxes" and "Piles" to represent collections of _Things_. A _Box_ is a loose collection of _Things_, while a _Pile_ is an ordered collection of _Things_ with associated indexes.

Control flow in our language is represented using actions such as:

- `[If]{(c)[TestAction]{Parameters}, (t)[ActionIfTrue]{parameters}, (f)[ActionIfFalse]{parameters}}` for if-then-else statements, 
- `[While]{(c)[ConditionAction]{parameters}, (a)[ActionSequence]{parameters}}` for while loops, and 
- `[For]{(i)[InitializationAction]{parameters}, (c)[ConditionAction]{parameters}, (u)[UpdateAction]{parameters}, (a)[ActionSequence]{parameters}}` for for loops.

Error handling in our language is implemented through the simplified `[Attempt]` action which attempts an action and handles exceptions in one go.

## TAC

### Things

The syntax for a *Thing* is flexible. It is enclosed in curly braces `{}` when it represents being transported (i.e., read from), such as the inputs to an action, enclosed in angle brackets `<>` when it represents being assigned (i.e., written to), and enclosed in square brackets `[]` when it represents actions (i.e., executed). When referring to a *Thing* within the language, we simply use its identifier.

In the context of our language, a *Thing* can represent various components:
- It can be an input to an action, or assigned to another *Thing*.
- It can be an action, indicating the operations or transformations performed.
- It can be an output from an action, or assigned the value of another *Thing*.

### Contexts

In our language, we introduce the concept of "contexts", which are represented by different types of brackets. This concept is rooted in the philosophy of making the language readable in plain English, while also providing extra-contextual information about how to interpret and execute the usage of a Thing.

These are the contexts we've defined:

1. **Action Context `[]`**: This context is all about actions. When you see a *Thing* within square brackets, you know that it represents an operation to be executed.
2. **Transport Context `{}`**: This context transports *Things*, as parameters, to an action or assignment. A Thing within curly braces is a piece of information or data being passed to an action defined in square brackets or an assignment defined in angle brackets. Multiple *Things* are separated by (1) commas, or (2) new lines and indentation, in off-side rule form.
3. **Assignment Context** `<>`: This context changes the value or content, if any, of a *Thing*. The input can be a primitive, a literal, an action, or a transport representing multiple *Things*.
4. **Index Context** `()`: This context contains the index of a *Thing* in a Pile.

```TACL
# Valid Assignment Context usages
<myThing> is "the pen in my right pocket"
<myAge> is 27
<myStuff> is {myThing, myAge}
<allMyStuff>{myStuff, <myName>"Corey"}
<allMyStuffOrdered>{(1)myStuff, (2)<myName>"Corey"}

<MyShoeType>[DefineThingType]{
    Brand
    LaceColor
    Cost
}
<MyShoe>[CopyThingType]{MyShoeType}
<MyShoe.Brand>"New Balance"
<MyShoe.LaceColor>"Orange"
<MyShoe.Cost>"45 USD"
```

### Actions

A function is a process or operation that takes certain information (input) and produces a result (output). To simplify our language and make it more intuitive, we replace "Function" with "Action". An "Action" can be seen as a higher-level "Thing" that performs operations and manipulates other "Things". 

Here's an example of how you could write a simple action, using the system `[DefineAction]` action:

```TACL
<AddNumbers>[DefineAction]{
	<Input>{num1, num2}
	<Default><error>"An error has occurred."
	<Body>{
		<result>[Add]{num1, num2}
		<Return>{result}
	}
}

[AddNumbers]{1, 2}
```

The `[DefineAction]` action takes three parameters in a transport: an Input, a Default output, and a Body.

1. The `<Input>` is a *Thing* that contains the parameters of the action.
2. The `<Default>` is a *Thing* that contains the *Thing* to return if the action doesn't otherwise return. In this example, the string is also being assigned to a *Thing* named "error".
3. The `<Body>` is a *Thing* that encapsulates the operations of the action. This approach retains the transport and assignment aspects of our language, while also simplifying the syntax.

The `<Return>` is a fourth *Thing*, that returns from the action. It is set to `<Default>` when the action is first executed.

We allow eliding the commas in a transport list if the transport list is fully separated by lines.

## Showing Things Off

This is an example that demonstrates most of the major features of TACL.

```TACL
<Main>[DefineAction]{
	<Input> is {}
	<Default> is <error> is "An Error has occurred, please panic."
	<Body> is {
		# myFavouriteNumber is 7
		<myFavouriteNumber> is 7
		
		# Print with myFavouriteNumber
		[Print] with {myFavouriteNumber}
		
		# Print with CustomAdd with myFavouriteNumber and 4
		[Print] with {[CustomAdd] with {myFavouriteNumber, 4}}
		
		# myFavouriteNumber is 8
		<myFavouriteNumber>8
		
		# Print with myFavouriteNumber
		[Print]{myFavouriteNumber}
		
		# myNewNumber is myTestAction with myFavouriteNumber.
		<myNewNumber>[myTestAction]{myFavouriteNumber}
		
		# myNewNumber is myTestAction with Add with myFavouriteNumber and 42.
		<myNewNumber>[myTestAction]{[Add]{myFavouriteNumber, 42}}
		
		# Print with myNew Number
		[Print]{myNewNumber}
		
		# myNewNextNumber is MyTestAction with myNewNumber
		<myNextNewNumber>[MyTestAction]{(i)myNewNumber}
		
		# Print with myNextNewNumber
		[Print]{myNextNewNumber}
		
		[If]{
			(c)[GreaterThan]{10,2}
			(t)[Print]"10 is greater than 2!"
			(f)[Print]"10 is less than 2!"
		}
		
		[Attempt]{(a)[Print]{[Divide]{1,0}}, (e)[Print]"You can't divide by zero!"}
		
		[Attempt]{
			(a)[Print]{
				[Divide]{2,0}
			}
			(e)[Print]"You \*still\* can't divide by zero!!!"
		}
		
		<Return>0
	}
}

<CustomAdd>[DefineAction]{
	<Input>{num1, num2}
	<Default><Error>"An Error has occurred, please panic."
	<Body>{
		<temp>[Add]{num1, num2}
		<Return>[Add]{temp, 1}
	}
}

<MyTestAction>[DefineAction]{
	<Input>{
        (i)inputNum
    }
	<Default><Error>"An Error has occurred, please panic."
	<Body>{
		<internalNumber>7
		<newNumber>[CustomAdd]{inputNum, internalNumber}
		<Return>{newNumber}
	}
}

[Main]
```

## Ordering Things with Contexts

In TACL, the arrangement of assignments, actions, and transport contexts is flexible, yet follows specific rules. This flexibility allows you to construct different types of expressions based on your needs. Here are the valid orders for these components:

1. An Assignment can be any sort of anything that can follow the keyword **is:** `<Assignment> is 5`, or `<Assignment>5` for short. Enclose strings in double quotation marks: `<Assignment> is "my shoe"`, or `<Assignment>"my shoe"` 
2. An assignment can be an action: `<Assignment> is [Action]` or `<Assignment>[Action]` for short.
3. An action can take a transport context using the keyword **with**: `[Action] with {Transport}` or concisely `[Action]{Transport}`.
4. An action, if a Pile, can take an index context, which returns that Thing in the Pile: `[myPile] with (3)` returns the third `Thing` in `myPile`, or `[myPile](3)` for short.
5. An assignment can be an action with a transport context: `<Assignment> is [Action] with {Transport}` or more concisely `<Assignment>[Action]{Transport}`.
6. A transport can be a comma-separated list of *Things*, actions, or assignments. Indexes, to induce order, can be included using the index context.

### Concise and Plain Forms

TACL offers two forms for writing expressions: the Plain form and the Concise form. The Plain form uses keywords like 'is', 'with', and 'at' to structure the expression, making it more readable. The Concise form, on the other hand, omits these keywords, resulting in a more compact expression. Here's how the two forms compare:

1. In Plain form, an assignment is an action: `<Assignment> is [Action]`. In Concise form, this becomes `<Assignment>[Action]`.
2. In Plain form, an action takes a transport context: `[Action] with {Transport}`. In Concise form, this becomes `[Action]{Transport}`.
3. In Plain form, an assignment can be an action with a transport context: `<Assignment> is [Action] with {Transport}`. In Concise form, this becomes `<Assignment>[Action]{Transport}`.
4. In Plain form, an assignment can be a transport context: `<Assignment> is {Transport}`. In Concise form, this becomes `<Assignment>{Transport}`.
5. In Plain form, an assignment can be a Pile with *Things* in given indexes using the keyword **at**: `<Assignment> is {"Item 1" at 1, "Item 2" at 2}`. In Concise form, this becomes `<Assignment>{(1)"Item 1", (2)"Item 2"}`.
6. In Plain form, a Pile, in an action context, takes an index context: `[Pile] with (Index)`. In Concise form, this becomes `[Pile](Index)`. For compatibility, either `with` or `at` are accepted in Plain form.
7. In Plain form, an assignment can be a Pile, in an action context, with an index context: `<Assignment> is [Pile] with (Index)`. In Concise form, this becomes `<Assignment>[Pile]{Index}`. For compatibility, either `with` or `at` are accepted in Plain form.

## Expanding Things with Boxes and Piles

In our language, we use the concept of "Boxes" to represent a collection of *Things*. This is similar to the idea of a "list" or an "array" in many programming languages, but with a key distinction.

A *Box* is a *Thing* that contains other *Things*. The specific *Things* that a *Box* contains are ordered, but not indexed.

```TACL
#Box - Plain Form
<Thing1> is "Whatever is in my left front pocket right now."
<Thing2> is "the memory of watching the sunset in Nassau on a cool fall evening"
<myThing> is {Thing1}
<myThingBox> is {myThing, Thing2, Thing3}

#Box - Concise Form
<Thing1>"Whatever is in my left front pocket right now."
<myThing>{Thing1}
<myThingBox>{myThing, Thing2, Thing3}
```

We adapt the concept for an ordered *Box*, or *Pile*. Here, we use the `at` keyword or the index context `()` to associate the *Things* with their indexes. Indexes can be numbers, letters, or Thing names themselves. 
 
```TACL
#Pile - Plain Form
<myThingPile> is {myThing at 1, [Add]{Thing2, 1} at 2, "This is a thing too!" at 3}

#Pile - Concise Form
<myThingPile>{(1)myThing, (2)[Add]{Thing2, 1}, (3)"This is a thing too!"}
```

Things within a pile can be accessed by their index using the index context `()` or the  `[AccessAt]` action:

```TACL
<myFirstThing>"my will to live"

<MyFirstPile>{(1)myFirstThing, (2)[Add]{1, 1}, (3)"This is a thing too!", (d)"And I stand out!"}

<mySpecificThing>[myFirstPile](1)
[Print]{mySpecificThing} # would print "my will to live" to the standard output

<mySpecificThing2>[myFirstPile](d)
[Print]{mySpecificThing2} # would print "And I stand out!" to the standard output

<myThing>[AccessAt]{myThingPile, 3}
[Print]{myThing} # would print "This is a thing too!" to the standard output

<myIndex>1
<myThing>[AccessAt]{myThingPile, [Add]{myIndex, 1}}
[Print]{myThing} # would print "2" to the standard output

[If]{(c)[IsTrue]{True}, (t)[Print]"If Actions take piles!", (f)[Print]"This will never print"}

```

We allow eliding the commas in a Box or Pile if the contents is fully separated by lines. For example:

```TACL
<myThingBox>{
	myThing
	Thing2
	Thing3
}

<myThingPile> is {
	myThing at 1
	Thing2 at 2
	Thing3 at 3
    Thing4 at d
}

<myThingPile>{
	(1)myThing
	(2)[Add]{2, 1}
	(3)"This is a thing too!"
    (d)"This is a stand-out Thing!"
}
```

## Mentioning Things

The `[Here]` action is a declaration tool that introduces the concept of scope and the existence of sub*Things*. It serves as a way to mention that a *Thing* exists within a given scope without performing any operations on it, such as reading, writing, or executing it. This action is particularly useful for defining the structure and properties of composite *Things* that contain multiple sub*Things*, which can be referenced as properties of the instance.

```TACL
<Conveyor>[DefineThingType]{
	<RunCommand> is [Here]   # Declares the existence of RunCommand within Conveyor's scope
}
```

### Usage of `[Here]`

The `[Here]` action is used within a *Thing* definition to declare sub*Things* that exist as part of the composite *Thing*. These sub*Things* can then be accessed by referencing the parent *Thing*'s name, followed by a dot notation to access the specific sub*Thing* (e.g., `ConveyorInstance1.RunCommand`).

When `[Here]` is used, it specifies that the sub*Thing* is part of the composite *Thing*'s layout and can be interacted with in the defined scope. The declaration does not assign any value or action to the sub*Thing*; it merely acknowledges its existence.

### Example Definition of a Composite Thing with `[Here]`

```TACL
<Conveyor>[DefineThingType]{
	<RunCommand> is [Here]   # Declares the existence of RunCommand within Conveyor's scope
	<RunningFeedback>[Here]   # Declares the existence of RunningFeedback
                              # We elide the " is " after this for convenience
	<HesOutput>[Here]   # Declares the existence of HesOutput
	<DebounceTimer>[Here]   # Declares the existence of DebounceTimer
	<HesRaw>[Here]   # Declares the existence of HesRaw
	<HesDebounce>[DefineAction]{
		<Input>{Conveyor.HesRaw, Conveyor.DebounceTimer}
		<Default>1
		<Body>{
			[If]{
				(c)[Equals]{Conveyor.HesRaw, 1}
				(t)<HesCleared>{
					<HesClearedTimer>[RunTimer]{Conveyor.HesClearedTimer}
					[If]{
						(c)[GreaterThan]{HesClearedTimer, Conveyor.DebounceTimer}
						(t)<Conveyor.HesOutput>1
						(f)<Conveyor.HesOutput>{Conveyor.HesOutput}
					}
					<Conveyor.HesBlockedTimer>0
				},
				(f)<HesBlocked>{
					(c)<HesBlockedTimer>[RunTimer]{Conveyor.HesBlockedTimer}
					(t)[If]{
						(c)[GreaterThan]{HesBlockedTimer, Conveyor.DebounceTimer}
						(t)<Conveyor.HesOutput>0
						(f)<Conveyor.HesOutput>{Conveyor.HesOutput}
					}
					(f)<Conveyor.HesClearedTimer>0
				}
			}
			<Return>1
		}
	}
}
```

### Interacting with Mentioned SubThings

Once a composite *Thing* is defined and its sub*Things* are mentioned using `[Here]`, an instance of this composite *Thing* can be created. This instance can then be manipulated by changing the values of its sub*Things* through assignment.

```TACL
<Conveyor1>[DefineThing]{ConveyorType}  # Creates Conveyor1 with same layout as Conveyor

<Conveyor1.HesRaw>1  # Assigns a value to HesRaw subThing of Conveyor1

<TestThing>{Conveyor1.HesOutput}  # Retrieves the value of HesOutput from Conveyor1 and assigns it to TestThing
```

By using `[Here]`, we can clearly define the structure of a composite *Thing* and its sub*Things*, enabling structured and organized interaction with the components of the *Thing* in question.

### Scopes

Scopes in TACL are defined by the boundaries of a Thing definition. Each Thing has its own scope, and subThings exist within the scope of the composite Thing. When a composite Thing is instantiated, its subThings are also instantiated within the same scope, allowing for namespaced access to these components.

## Controlling the Flow of Things

### If-Then-Else

The If-Then-Else construct in TACL provides a mechanism to execute different sequences of actions based on the evaluation of a condition. This control flow action is designed to enhance decision-making processes within the language. When employing If-Then-Else, we categorize our components into three distinct roles:

1. **Condition Evaluation (`[TestAction]`)**: This is an action with index `c` that evaluates to a boolean value. The result of this evaluation determines which subsequent path the execution will follow.
2. **True Branch (`[ActionIfTrue]`)**: This action or sequence of actions with index `t` is executed if `[TestAction]` evaluates to true. It's a series of operations that are enacted when the specified condition holds.
3. **False Branch (`[ActionIfFalse]`)**: Conversely, if `[TestAction]` evaluates to false, this action or sequence of actions with index `f` will be carried out. It represents an alternate path of execution for scenarios where the condition is not met.

The syntax for using the If-Then-Else construct is as follows:

```TACL
[If]{(c)[TestAction]{Parameters}, (t)[ActionIfTrue]{trueParams}, (f)[ActionIfFalse]{falseParams}}
```

An example of this control flow in practice might be:

```TACL
<temperature>25

[If]{
    (c)[GreaterThan]{temperature, 20}, 
    (t)[Print]{"It's a warm day."},
    (f)[Print]{"It's a cool day."}
}
```

In the example above, the condition checks whether the variable `temperature` exceeds 20 degrees. If the condition is true, the program prints "It's a warm day." Otherwise, it prints "It's a cool day."

### Loops

In our language, we redefine traditional loops using our action and transport contexts. Here's how we approach this:

#### While Loop

The while loop is represented by an action, `[While]`. The `[While]` action takes two parameters: an action with index `c` that returns a boolean (the loop condition), and an action (or sequence of Actions) with index `a` to execute while the condition is true. 

```TACL
[While]{(c)[ConditionAction]{parameters}, (a)[ActionSequence]{parameters}}
```

#### For Loop

The for loop is a bit more complex, as it involves initialization, condition checking, and incrementation/decrementation. We represent this with an action, `[For]`. The `[For]` action takes three parameters: an action with index `i` that initializes the loop variable, an action with index `c` that checks the loop condition, and an action with index `u` that updates the loop variable at the end of each iteration. A fourth parameter with index `a` is the Action (or sequence of Actions) to execute in each iteration.

```TACL
[For]{(i)[InitializationAction]{parameters}, (c)[ConditionAction]{parameters}, (u)[UpdateAction]{parameters}, (a)[ActionSequence]{parameters}}
```

### Attempt

Given our language structure, we upgraded our try-catch mechanism into a single action. This is done by introducing a new action `[Attempt]`  which simultaneously attempts an action and handles any exceptions in one go. The `[Attempt]` action can take two parameters: the action to be attempted with index `a` and the action to be executed in case of an error with index `e`.

The syntax looks like this:

```TACL
[Attempt]{(a)[ActionToAttempt]{parameters}, (e)[ErrorHandler]{parameters}}
```

For example, if we have an action `CalculateDistance` that takes two parameters `start_point` and `end_point`, and an error handling action `HandleError`, the `[Attempt]` action would look like this:

```TACL
[Attempt]{(a)[CalculateDistance]{start_point, end_point}, (e)[HandleError]{parameters}}
```

In this case, `CalculateDistance` will be attempted. If it executes without an exception, then the program proceeds normally. But if an exception is thrown, the `HandleError` action is called.

## Appendix: Standard Libary of Actions

### System/Shell/IO Actions

- `<thing1>[Assign]{thing2}`
    - Assigns thing1 the contents of thing2. Can also use `<thing1>{thing2}`.
- `<MyAction>[DefineAction]{Input, Default, Body}`
	- Creates an Action using the given Input(s), Default returned *Thing*, and Body. Returns a *Thing*, which could very well be no*Thing*... null. DefineAction and DefineThingType can be nested within each other.
- `<MyThingType>[DefineThingType]{thing1, thing2, ..., thingN}`
    - Creates an example "MyThingFromType" Thing Type with the sub-things thing1, thing2, ..., thingN. DefineAction and DefineThingType can be nested within each other.
- `<MyThingFromType>[CopyThingType]{ThingType}`
	- Creates an example "MyThingFromType" Thing from the Thing Type ThingType. 
- `<Result>[AccessAt]{Pile, Index}`
	- Returns the *Thing* in the given Pile at the given Index. This is the same as using `[Pile](Index)`.
- `<StoredInput>[Prompt]{promptString}`
	- Prints the promptString to the standard output and awaits input from the standard input. Returns the line of input. 
- `[Print]{thing1, thing2, ..., thingN}`
	- Prints the contents of thing1, thing2, ..., thingN to the standard output.

### Control Flow Actions

- `[If]{(c)[TestAction]{Parameters}, (t)[ActionIfTrue]{parameters}, (f)[ActionIfFalse]{parameters}}`
	- If-Then-Else.
- `[Attempt]{(a)[ActionToAttempt]{parameters}, (e)[ErrorHandler]{parameters}}`
	- Exception handling.
- `[For]{(i)[InitializationAction]{parameters}, (c)[ConditionAction]{parameters}, (u)[UpdateAction]{parameters}, (a)[ActionSequence]{parameters}}`
	- For Loop.
- `[While]{(c)[ConditionAction]{parameters}, (a)[ActionSequence]{parameters}}`
	- While Loop.

### Mathematical and Logical Operation Actions

- `<Sum>[Add]{thing1, thing2, ..., thingN}`
	- Adds thing1 and thing2, and thing3 ..., and thingN and returns the Sum.
	- `[Plus]{thing1, thing2, ..., thingN}` will work, too.
- `<Subtrahend>[Subtract]{thing1, thing2, ..., thingN}`
	- Subbtracts thing1 from thing2, and from thing3, ..., from thingN, and returns the Subtrahend.
	- `[Minus]{thing1, thing2, ..., thingN}` will work, too.
- `<Product>[Multiply]{thing1, thing2, ..., thingN}`
	- Multiplies thing1 and thing2, and thing3, ..., and thingN and returns the Product.
	- `[Times]{thing1, thing2, ..., thingN}` will work, too.
- `<Dividend>[Divide]{thing1, thing2, ..., thingN}`
	- Divides thing1 by thing2, by thing3, ..., by thingN and returns the Dividend.
	- `[Frac]{thing1, thing2, ..., thingN}` will work, too.
- `[Increment]{thing, increment}`
	- Increment thing by increment.
- `[Decrement]{thing, decrement}`
	- Decrement thing by decrement.
- `<ResultOfEven>[IsEven]{thing}`
	- Returns true if thing is even, false if thing is odd.
- `<ResultOfOdd>[IsOdd]{thing}`
	- Returns true if thing is odd, false if thing is even.
- `<ResultOfAnd>[And]{thing1, thing2, ..., thingN}`
	- Returns true if thing1, thing2, ..., thingN are all true, returns false if any are false.
- `<ResultOfOr>[Or]{thing1, thing2, ..., thingN}`
	- Returns true if any of thing1, thing2, ..., thingN are true, returns false if all are false.
- `<ResultOfNot>[Not]{thing}`
	- Returns true if thing is false, returns false if thing is true.
- `<ResultOfGreaterThan>[GreaterThan]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is greater than thing2, and if thing2 is greater than thing3, ..., and if thingN-1 is greater than thingN.
- `<ResultOfLessThan>[LessThan]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is less than thing2, and if thing2 is less than thing3, ..., and if thingN-1 is less than thingN.
- `<ResultOfEquals>[Equals]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is equal to thing2, and if thing2 is equal to thing3, ..., and if thingN-1 is equal to thingN.
- `<ResultOfUnequals>[Unequals]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is unequal to thing2, and if unthing2 is equal to thing3, ..., and if thingN-1 is unequal to thingN.


--------------------

**assistant**:
Understood. I am now prepared to assist with converting code into the Thing-Action-Context Language (TACL) as specified. If you have code that you'd like translated into TACL, please provide it at your convenience.

--------------------

**user**:
Please read the following TACL and write a suitable VFD control Action to integrate VFDs and their adjustable speed and dual-speed abilities over a normal starter. I want to be able to input the two target speeds in feet-per-minute (fpm) and scale the output (configured given a set of two manually-taken fpm-and-hz measurements):

```TACL
####################################################################80#chars####
# # <Name>"Corey's Conveyor Controller (CCC)"
# # <Author>"Corey Naas"
# # <Date>"2023-11-26"
# # <License>"Copyright 2023 Corey Naas. All Rights Reserved."
# # <Description>"An exercise to refresh/revisit my conveyor programming 
# #                 experience by writing a program for one from scratch in my 
# #                 personal pseudocode."
# # <TargetLanguage>

# Functionality:
# - Photoeye Debouncing
# - Jam Protection
# - Overload Protection
# - Manual Mode and toggle
# - Cascade/Dieback
# - Emergency Stop
# - Motor Safety Disconnect/OOS
# - Timeout/idle-stop and restart
# - Restart Delay
# - Failed to Start Alarming
# To Do:
# - VFD/speed Support
# - Withholding
# - Runtime Statistics/Preventive Maintenance
# - Gapping
<System/Language>{"EN"}
<System/StyleEnforcement>{"None"}

# Import special actions
<SR>[ImportAction]{System/SetResetLatch}
<RunTimer>[ImportAction]{System/RockwellStyleTimerOnDelay}

# Define the Conveyor and all functionality
<Conveyor>[DefineThingType]{
	<Status>[DefineThingType]{
		(1)Starting
		(2)<Running>{Conveyor.RunFeedback}
		(3)<Stopped>[NOT]{Conveyor.Running}
		(4)<NoRunCommand>[NOT]{Conveyor.RunRequest}
		(5)TimedOut
		(6)<Cascaded>{Conveyor.Cascaded}
		(7)<Jammed>{Conveyor.Jammed}
		(8)Withheld
		(9)<EStopActive>{Conveyor.EStopActive}
		(10)OutOfService
		(11)FailedToRun
		(12)FailedToStop
		(13)Overloaded
	}
	<Manual>[DefineThingType]{
		(1)Enable
		(2)Request
	}
	<Config>[DefineThingType]{
		(1)DebounceTime
		(2)JamTime
		(3)OverloadTime
		(4)TimeoutTime
		(5)DelayTime
	}
	<DebouncePhotoeye>[DefineAction]{
		<Input>{PhotoeyeRaw, DebounceTime}
		<Default>0
		<Body>{
			[If]{
				(c)[Equals]{PhotoeyeRaw, 1}
				(t)<PhotoeyeCleared>{
					<PhotoeyeClearedTimer>[RunTimer]{PhotoeyeClearedTimer}
					[If]{
						(c)<>[GreaterThan]{PhotoeyeClearedTimer, DebounceTime}
						(t)<Conveyor.PhotoeyeOutput>1
						(f)<Conveyor.PhotoeyeOutput>{Conveyor.PhotoeyeOutput}
					}
					<PhotoeyeBlockedTimer>0
				}
				(f)<PhotoeyeBlocked>{
					<PhotoeyeBlockedTimer>[RunTimer]{PhotoeyeBlockedTimer}
					[If]{
						(c)<>[GreaterThan]{PhotoeyeBlockedTimer, DebounceTime}
						(t)<Conveyor.PhotoeyeOutput>0
						(f)<Conveyor.PhotoeyeOutput>{Conveyor.PhotoeyeOutput}
					}
					<PhotoeyeClearedTimer>0
				}
			}
			<Return>1
		}
	}
	<DetectJam>[DefineAction]{
		<Input>{Photoeye, JamTime, Reset}
		<Default>0
		<Body>{
			<JamTimer>[RunTimer]{[AND]{
				Conveyor.Running
				[NOT]{Photoeye}}
			}
			[If]{
				(c)<>[GEQ]{JamTimer, JamTime}
				(t)<Conveyor.Jammed><Status.Jammed>1
				(f)<>{
					<Conveyor.Starting>1
					<Conveyor.Jammed><Status.Jammed>0
				}
			}
			[If]{
				(c)<>Reset
				(t)<>{
					<Conveyor.Starting>1
					<Reset><Conveyor.Jammed><Status.Jammed><JamTimer>0
				}
				(f)<>
			}
			<Return>1
		}
	}
	<DetectOverload>[DefineAction]{
		<Input>{Overload, OverloadTime, Reset}
		<Default>0
		<Body>{
			<OverloadTimer>[RunTimer]{Overload}
			[If]{
				(c)<>Reset
				(t)<>{
					<Conveyor.Starting>1
					<Reset><Conveyor.Overloaded><Status.Overloaded><OverloadTimer>0
				}
				(f)<>
			}
			[If]{
				(c)<>[GEQ]{OverloadTimer, OverloadTime}
				(t)<Conveyor.Overloaded><Status.Overloaded>1
				(f)<Conveyor.Overloaded><Status.Overloaded>0
			}
			<Return>1
		}
	}
	<DetectFailureToRun>[DefineAction]{
		<Inputs>{RunCommand, RunFeedback, RunFailureTime}
		<Default>0
		<Body>{
			<RunFailureTimer>[RunTimer]{
				[AND]{
					RunCommand
					[NOT]{RunFeedback}
				}
			}
			[If]{
				(c)<>Reset
				(t)<>{
					<Reset><Conveyor.FailedToRun><Status.FailedToRun><FailureTimer>0
				}
				(f)<>
			}
			[If]{
				(c)<>[GEQ]{RunFailureTimer, RunFailureTime}
				(t)<Conveyor.FailedToRun><Status.FailedToRun>1
				(f)<Conveyor.FailedToRun><Status.FailedToRun>0
			}
			<Return>1
		}
	}
	<DetectCascade>[DefineAction]{
		<Input>{Photoeye, DownstreamConveyorRunning, Reset}
		<Default>0
		<Body>{
			<Conveyor.Cascaded>[SR]{
				(s)<>[AND]{
					[NOT]Photoeye
					[NOT]DownstreamConveyorRunning
					Conveyor.Running
				}
				(r)<>[OR]{
					[Equals]{DownstreamConveyorRunning, 1}
					[Equals]{Reset, 1}
				}
			}
			<Return>1
		}
	}
	<DetectOutOfService>[DefineAction]{
		<Input>{MotorSafetyDisconnect}
		<Default>0
		<Body>{
			[If]{
				(c)[Equals]{MotorSafetyDisconnect, 0}
				(t)<Conveyor.OutOfService><Status.OutOfService>1
				(f)<Conveyor.OutOfService><Status.OutOfService>0
			}
			<Return>1
		}
	}
	<PollIdleTimer>[DefineAction]{
		<Inputs>{Running, UpstreamPhotoeye, TimeoutTime, Reset}
		<Default>0
		<Body>{
			<TimeoutTimer>[RunTimer]{
				[AND]{Running, [NOT]{UpstreamPhotoeye}}
			}
			[If]{
				(c)<>[OR]{Reset, [NOT]{UpstreamPhotoeye}}
				(t)<>{
					<Conveyor.Starting>1
					<Reset><Conveyor.TimedOut><Status.TimedOut><TimeoutTimer>0
				}
				(f)<>
			}
			# Stop conveyor 
			[If]{
				(c)<>[GEQ]{TimeoutTimer, TimeoutTime}
				(t)<Conveyor.TimedOut><Status.TimedOut>1
				(f)<Conveyor.TimedOut><Status.TimedOut>0
			}
		}
	}
	<PollGapInducement>{
		<Input>{Photoeye, Running, GapDistance}
		<Default>
		<Body>{
			<GapTimer>[RunTimer]{
				[AND]{
					[NOT]Photoeye
					Running
				}
			}
			[IF]{
				(c)[GEQ]{}
				(t)
				(f)
			}
		}
	}
	<PollHardInterlocks>[DefineAction]{
		<Input>{EStopActive, Overloaded, OutOfService, FailedToRun}
		<Default>0
		<Body>{
			# C.HIO = A ∧ B ∧ C
			<Conveyor.HardInterlocksOkay>[AND]{
				[NOT]{EStopActive}
				[NOT]{Overloaded}
				[NOT]{OutOfService}
				[NOT]{FailedToRun}
			}
		}
	}
	<PollSoftInterlocks>[DefineAction]{
		<Input>{Jammed, Cascaded, TimedOut, Manual}
		<Default>0
		<Body>{
			# C.SIO = ¬A ∧ ¬B ∧ (¬C ∨ (C ∧ D))
			<Conveyor.SoftInterlocksOkay>[AND]{
				[NOT]{Starting}
				[NOT]{Jammed}
				[NOT]{Cascaded}
				[NOT]{TimedOut}
				[OR]{
					[NOT]{Manual.Enable}
					[AND]{Manual.Enable, Manual.Request}
				}
			}
		}
	}
	<DelayStartup>[DefineAction]{
		<Inputs>{DelayFlag, DelayTime}
		<Default>0
		<Body>{
			<DelayTimer>[RunTimer]{DelayFlag}
			# Start the Conveyor and reset the timer after it finishes
			[If]{
				(c)<>[GEQ]{DelayTimer, DelayTime}
				(t)<Conveyor.Starting><DelayFlag><DelayTimer>0
				(f)<>
			}
			<Return>1
		}
	}
	<Run>[DefineAction]{
		<Input>{HardInterlocksOkay, SoftInterlocksOkay, RunRequest}
		<Default>0
		<Body>{
			# = A ∧ B ∧ C
			<Conveyor.RunCommand>[AND]{
				HardInterlocksOkay
				SoftInterlocksOkay
				RunRequest
			}
			<Return>1
		}
	}
	[DebouncePhotoeye]{Conveyor.PhotoeyeRaw, Conveyor.Config.DebounceTime}
	[DetectJam]{Conveyor.PhotoeyeOutput, Conveyor.Config.JamTime, 
							Conveyor.Reset}
	[DetectOverload]{Conveyor.Overload, Conveyor.Config.OverloadTime, 
							Conveyor.Reset}
	[DetectFailureToRun]{Conveyor.RunCommand, Conveyor.RunFeedback, 
							Conveyor.RunFailureTime}
	[DetectCascade]{Conveyor.PhotoeyeOutput, Conveyor.DownstreamConveyorRunning}
	[PollIdleTimer]{Conveyor.Running, Conveyor.UpstreamPhotoeye, 
							Conveyor.Config.TimeoutTime, Conveyor.Reset}
	[PollGapInducement]{Conveyor.PhotoeyeOutput, Conveyor.Running, 
							Conveyor.Config.GapDistance}
	[PollHardInterlocks]{Conveyor.EStopActive, Conveyor.Overloaded, 
							Conveyor.OutOfService}
	[PollSoftInterlocks]{Conveyor.Jammed, Conveyor.Cascaded, Conveyor.TimedOut, 
							Conveyor.Manual}
	[DelayStartup]{Conveyor.Config.DelayTime}
	[Run]{Conveyor.HardInterlocksOkay, Conveyor.SoftInterlocksOkay, 
							Conveyor.RunRequest}
}

# Define the Main routine
<Main>[DefineAction]{
	<Inputs>{}
	<Default>
	<Body>{
		<Convey01️>[CopyThingType]{Conveyor} # Convey-oh-one. Say it aloud!
		[ContinuousLoop]{
			<Convey01️.RunRequest>[System/GetInputWithPrompt]{
				"To start motor : 1 /n To stop motor : 0"
			 }
			<SimulatedMotor>{Convey01️.RunCommand}
			<Convey01️.RunFeedback>{SimulatedMotor}
			[Print]{Convey01️.Status.Running}
		}
		<Return>1
	}
}

# Run the Main routine
[Main]
```

--------------------

**assistant**:
Certainly. Here is an action for integrating Variable Frequency Drive (VFD) control into the existing conveyor system, allowing adjustable speed control based on the input of target speeds in feet-per-minute (fpm).

```TACL
<VFDControl>[DefineAction]{
	<Input>{TargetSpeed1, TargetSpeed2, Measurement1Hz, Measurement1Fpm, Measurement2Hz, Measurement2Fpm}
	<Default><Error>"An error has occurred in VFDControl."
	<Body>{
		# Calibrate the VFD based on manual measurements at two different points
		<ScaleFactor>[Divide]{
			[Subtract]{Measurement2Fpm, Measurement1Fpm},
			[Subtract]{Measurement2Hz, Measurement1Hz}
		}
		<Offset>[Subtract]{
			Measurement1Fpm,
			[Multiply]{Measurement1Hz, ScaleFactor}
		}

		# Define two actions to set the VFD speed
		<SetVFDSpeed1>[DefineAction]{
			<Input>{TargetSpeed1}
			<Default><Error>"An error has occurred in SetVFDSpeed1."
			<Body>{
				<TargetHz1>[Add]{
					[Divide]{TargetSpeed1, ScaleFactor},
					Offset
				}
				# Issue the command to the VFD (placeholder for actual command)
				<VFDCommand1>[Print]{"Setting VFD to " + TargetHz1 + " Hz."}
				<Return>0
			}
		}

		<SetVFDSpeed2>[DefineAction]{
			<Input>{TargetSpeed2}
			<Default><Error>"An error has occurred in SetVFDSpeed2."
			<Body>{
				<TargetHz2>[Add]{
					[Divide]{TargetSpeed2, ScaleFactor},
					Offset
				}
				# Issue the command to the VFD (placeholder for actual command)
				<VFDCommand2>[Print]{"Setting VFD to " + TargetHz2 + " Hz."}
				<Return>0
			}
		}

		# Execute the actions to set the VFD speed
		[SetVFDSpeed1]{TargetSpeed1}
		[SetVFDSpeed2]{TargetSpeed2}
		
		<Return>0
	}
}

# Example usage of the VFDControl action
<VFDControl>{
	100, # Target speed 1 in fpm
	200, # Target speed 2 in fpm
	20,  # Manual Measurement Hz at point 1
	80,  # Manual Measurement fpm at point 1
	50,  # Manual Measurement Hz at point 2
	160  # Manual Measurement fpm at point 2
}
```

This action `VFDControl` allows for setting two target speeds. It calculates the scale factor and offset using two known manual measurements of Hz and fpm. Then, `SetVFDSpeed1` and `SetVFDSpeed2` are defined to send the appropriate Hz commands to the VFD based on the target speeds. The placeholder command `[Print]` is used to demonstrate where the actual VFD command would be issued.

Please note that in a real-world scenario, the code block issuing the command to the VFD (`VFDCommand1` and `VFDCommand2`) would need to be replaced with the actual command or interface call that communicates with the VFD hardware.
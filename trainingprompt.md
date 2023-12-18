# AI Training Prompt

This is a version of the specification I've pruned and tried to update for use with priming an AI with how TACL works so that it can attempt to convert anything given into it. In my tests with GPT-4, It works pretty well the first or second try. 

## Prompt Text


Hello AI programmer, Please load this programming language syntax specification into your context and prepare 1to convert code I give you into this form.
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

Thing-Action-Context Language (TACL) is a "programming" "language" that centers around the universal concept of "Things" which encapsulate data, actions, and control structures. TACL emphasizes readability and simplicity, using unique syntax that mirrors natural language while maintaining computational precision. It attempts to be a formulaic way to explain how to do anything.

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

Thing-Action-Context Language is designed to be a simple, versatile, and intuitive way to describe "doing stuff with things". In contrast to similar-looking languages such as LISP or Python, our language does not rely on symbolic expressions or prefix notation for function calls. Instead, it uses a quasi-postfix syntax to represent actions and their parameters. Our language also deviates from pseudocode by introducing specific syntax and clearly defined contexts for data transportation, assignment, and execution.

Our language is a significant departure from plain language too. While it is designed to be readable in plain language, it also introduces computational syntax and conventions for clarity and precision. This makes our language more constrained than traditional language without sacrificing readability or understandability.

[Thing Summary Paragraph]

We introduce the concept of "contexts" to provide additional information about how to interpret or execute the usage of a *Thing* contained within. Our language uses different types of brackets to denote four different contexts: action context `[]`, transport context `{}`, assignment context `<>`, and index context `()`.

Our language also introduces the concept of "Boxes" and "Piles" to represent collections of *Things*. A *Box* is a loose collection of *Things*, while a *Pile* is an ordered collection of *Things* with associated indexes.

"Control flow" in our language is represented using actions such as:

- `[If]{(c)[TestAction]{Parameters}, (t)[ActionIfTrue]{parameters}, (f)[ActionIfFalse]{parameters}}` for if-then-else statements, 
- `[While]{(c)[ConditionAction]{parameters}, (a)[ActionSequence]{parameters}}` for while loops, and 
- `[For]{(i)[InitializationAction]{parameters}, (c)[ConditionAction]{parameters}, (u)[UpdateAction]{parameters}, (a)[ActionSequence]{parameters}}` for for loops.

"Error handling" in our language is implemented through the simplified `[Attempt]` action which attempts an action and handles exceptions in one go.

## TAC

### Things

A *Thing* is anything that can be described in plain language. We surround *Things* in different kinds of brackets to represent different kinds of "being". It is enclosed in curly braces `{}` when it represents being transported (i.e., read from), such as the inputs to an action, enclosed in angle brackets `<>` when it represents being assigned (i.e., written to), and enclosed in square brackets `[]` when it represents actions (i.e., executed). When referring to a *Thing* within the language, we simply use its identifier.

In the context of our language, a *Thing* can represent various components:
- It can be an input to an action, or assigned to another *Thing*.
- It can be an action, indicating the operations or transformations performed.
- It can be an output from an action, or assigned the value of another *Thing*.

### Contexts

In our language, we introduce the concept of "contexts", which are represented by different types of brackets. This concept is rooted in the philosophy of making the language readable in plain language, while also providing additional information about how to interpret or execute the usage of a Thing.

These are the contexts we've defined:

1. **Action Context `[]`**: This context represents an operation to be executed, and is denoted by square brackets.
2. **Transport Context `{}`**: This context transports *Things*, as a box or pile, to an action or assignment. A Thing within curly braces is a piece of information or data being passed to an action (defined in square brackets) or an assignment (defined in angle brackets). Multiple *Things* are separated by (1) commas, or (2) new lines and indentation, in off-side rule form.
3. **Assignment Context** `<>`: This context changes the value or content, if any, of a *Thing*. The input can be a primitive, a literal, an action, or a transport representing multiple *Things*.
4. **Index Context** `()`: This context contains the index of a *Thing* in a Pile. An index may be a primitive, a literal, or a *Thing*.

```TACL
# Valid Assignment Context usages
<myThing>"the pen in my right pocket"
<myAge>27
<myStuff>{myThing, myAge}
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

A function is a process or operation that takes given information (input) and produces a result (output). In keeping with "plain language" principles, we replace "Function" with "Action". An "Action" can be seen as a higher-level "Thing" that performs operations and manipulates other "Things". 

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

<Result>[AddNumbers]{1, 2}
[Print]{Result}
```

The `[DefineAction]` action takes three *Things* in a transport: an Input, a Default output, and a Body.

1. The `<Input>` is a *Thing* that contains the passed Box or Pile of inputs to the action.
2. The `<Default>` is a *Thing* that contains the *Thing* to return if the action doesn't otherwise return. In this example, the string is also being assigned to a *Thing* named "error".
3. The `<Body>` is a Box that encapsulates the operations of the action. This approach retains the transport and assignment aspects of our language, while also simplifying the syntax. when this Thing is called in in action context, the Body is what is excecuted.

The `<Return>` is a fourth *Thing*, that returns from the action. It is set to `<Default>` when the action is first executed. It may be omitted, in which case the action will always return the default.

We allow eliding the commas in a transport list if each *Thing* is fully separated by lines.

## Showing Things Off

This is an example that demonstrates some of the features of TACL.

```TACL
<Main>[DefineAction]{
	<Input>{}
	<Default><error>"An Error has occurred, please panic."
	<Body>{
		# myFavouriteNumber is 7
		<myFavouriteNumber>7
		
		# Print with myFavouriteNumber
		[Print]{myFavouriteNumber}
		
		# Print with CustomAdd with myFavouriteNumber and 4
		[Print]{[CustomAdd]{myFavouriteNumber, 4}}
		
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

# AI Training Prompt Example

# User Prompt

**system**:
(Personal system prompt removed for privacy.)

--------------------

**user**:
Hello AI programmer, Please load this programming language syntax specification into your context and prepare to convert code I give you into this form.

```TACL
<Title>"Thing-Action-Context Language, or TACL"
<Tagline>"A Domain-Specific, General Purpose Language to Think and Write In"
<Author>"**Corey Naas**, November 2023"
<Website>"https://coreynaas.com/"
<Email>"coreynaas@outlook.com"
<License>"Copyright © 2023 Corey Naas. All rights reserved."
```

---

Thing-Action-Context Language (TACL) is a "programming" "language" that centers around the intentionally-vague concept of "Things" which encapsulate data, actions, and control structures. TACL emphasizes readability and simplicity, using unique syntax that mirrors natural language while maintaining computational precision. It is a formulaic way to explain how to do anything. In essence, TACL does "One Thing Well": provide a notation for composing *programs* from *expressions returning values*.

```TACL
# Define the action "Main" with the system "DefineAction" action
<Main>[DefineAction]{
	<Input> is {}
	<Default><Error>"An Error has occurred."
	<Body>{
		[Print]{"Hello World!"}
		<Return>{0}
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
- `[While]{[ConditionAction]{parameters}, [ActionSequence]{parameters}}` for while loops, 
- and `[For]{[InitializationAction]{parameters}, [ConditionAction]{parameters}, [UpdateAction]{parameters}, [ActionSequence]{parameters}}` for for loops.

Error handling in our language is implemented through the simplified `[Attempt]` action which attempts an action and handles exceptions in one go.

This language specification serves as a comprehensive guide to our language, providing detailed explanations of its unique features, syntax, and conventions. We hope it will serve as a useful tool for understanding and using our language to its fullest potential.

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
	<Input>{num1, num2},
	<Default><error>"An error has occurred.",
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
		<myNewNumber> is [myTestAction] with {myFavouriteNumber}
		
		# myNewNumber is myTestAction with Add with myFavouriteNumber and 42.
		<myNewNumber>[myTestAction]{[Add]{myFavouriteNumber, 42}}
		
		# Print with myNew Number
		[Print]{myNewNumber}
		
		# myNewNextNumber is MyTestAction with myNewNumber
		<myNextNewNumber> is [MyTestAction] with {myNewNumber}
		
		# Print with myNextNewNumber
		[Print] with {myNextNewNumber}
		
		[If]{
			(c)[GreaterThan]{10,2}
			(t)[Print]"10 is greater than 2!"
			(f)[Print]"10 is less than 2!"
		}
		
		[Attempt]{[Print]{[Divide]{1,0}}, [Print]"You can't divide by zero!"}
		
		[Attempt]{
			[Print]{
				[Divide]{2,0}
			}
			[Print]"You \*still\* can't divide by zero!!!"
		}
		
		<Return>0
	}
}

<CustomAdd>[DefineAction]{
	<Input>{num1, num2}
	<Default><Error>"An Error has occurred, please panic."
	<Body>{
		<temp>[Add]{num1, num2}
		<Return>{[Add]{temp, 1}}
	}
}

<MyTestAction>[DefineAction]{
	<Input>{inputNum}
	<Default>"An Error has occurred, please panic."
	<Body>{
		<internalNumber>7
		<newNumber>[CustomAdd]{inputNum, internalNumber}
		<Return>{newNumber}
	}
}

[Main]
```

## Orderings Things with Contexts

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

We adapt the concept for an ordered *Box*, or *Pile*. Here, we use the `at` keyword or the index context `()` to associate the *Things* with their indexes.
 
```TACL
#Pile - Plain Form
<myThingPile> is {myThing at 1, [Add]{Thing2, 1} at 2, "This is a thing too!" at 3}

#Pile - Concise Form
<myThingPile>{(1)myThing, (2)[Add]{Thing2, 1}, (3)"This is a thing too!"}
```

Things within a pile can be accessed by their index using the index context `()` or the  `[AccessAt]` action:

```TACL
<myFirstThing>"my will to live"

<MyFirstPile>{(1)myFirstThing, (2)[Add]{1, 1}, (3)"This is a thing too!"}

<mySpecificThing>[myFirstPile](1)
[Print]{mySpecificThing} # would print "my will to live" to the standard output

<myThing>[AccessAt]{myThingPile, 3}
[Print]{myThing} # would print "This is a thing too!" to the standard output

<myIndex>1
<myThing>[AccessAt]{myThingPile, [Add]{myIndex, 1}}
[Print]{myThing} # would print "2" to the standard output

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
}

<myThingPile>{
	(1)myThing
	(2)[Add]{2, 1}
	(3)"This is a thing too!"
}
```

## Mentioning Things

The `[Here]` action is a declaration tool that introduces the concept of scope and the existence of sub*Things*. It serves as a way to mention that a *Thing* exists within a given scope without performing any operations on it, such as reading, writing, or executing it. This action is particularly useful for defining the structure and properties of composite *Things* that contain multiple sub*Things*, which can be referenced as properties of the instance.

```TACL
<Conveyor>[DefineThing]{
	<RunCommand> is [Here]   # Declares the existence of RunCommand within Conveyor's scope
}
```

### Usage of `[Here]`

The `[Here]` action is used within a *Thing* definition to declare sub*Things* that exist as part of the composite *Thing*. These sub*Things* can then be accessed by referencing the parent *Thing*'s name, followed by a dot notation to access the specific sub*Thing* (e.g., `ConveyorInstance1.RunCommand`).

When `[Here]` is used, it specifies that the sub*Thing* is part of the composite *Thing*'s layout and can be interacted with in the defined scope. The declaration does not assign any value or action to the sub*Thing*; it merely acknowledges its existence.

### Example Definition of a Composite Thing with `[Here]`

```TACL
<Conveyor>[DefineThing]{
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
<Conveyor1> is [Conveyor]  # Creates Conveyor1 with same layout as Conveyor

<Conveyor1.HesRaw> is 1  # Assigns a value to HesRaw subThing of Conveyor1

<TestThing> is {Conveyor1.HesOutput}  # Retrieves the value of HesOutput from Conveyor1 and assigns it to TestThing
```

By using `[Here]`, we can clearly define the structure of a composite *Thing* and its sub*Things*, enabling structured and organized interaction with the components of the *Thing* in question.

### Scopes

Scopes in TACL are defined by the boundaries of a Thing definition. Each Thing has its own scope, and subThings exist within the scope of the composite Thing. When a composite Thing is instantiated, its subThings are also instantiated within the same scope, allowing for namespaced access to these components.

## Controlling the Flow of Things

### If-Then-Else

The If-Then-Else construct in TACL provides a mechanism to execute different sequences of actions based on the evaluation of a condition. This control flow action is designed to enhance decision-making processes within the language. When employing If-Then-Else, we categorize our components into three distinct roles:

1. **Condition Evaluation (`[If]`)**: This is an action that evaluates to a boolean value. The result of this evaluation determines which subsequent path the execution will follow.
2. **True Branch (`[ActionIfTrue]`)**: This action or sequence of actions is executed if `[TestAction]` evaluates to true. It's a series of operations that are enacted when the specified condition holds.
3. **False Branch (`[ActionIfFalse]`)**: Conversely, if `[TestAction]` evaluates to false, this action or sequence of actions will be carried out. It represents an alternate path of execution for scenarios where the condition is not met.

The syntax for using the If-Then-Else construct is as follows:

```TACL
[If]{(c)[TestAction]{Parameters}, (t)[ActionIfTrue]{trueParams}, (f)[ActionIfFalse]{falseParams}}
```

An example of this control flow in practice might be:

```TACL
<temperature>25

[If]{
    (c)<>[GreaterThan]{temperature, 20}, 
    (t)<>[Print]{"It's a warm day."},
    (f)<>[Print]{"It's a cool day."}
}
```

In the example above, the condition checks whether the variable `temperature` exceeds 20 degrees. If the condition is true, the program prints "It's a warm day." Otherwise, it prints "It's a cool day."

### Loops

In our language, we redefine traditional loops using our action and transport contexts. Here's how we approach this:

#### While Loop

The while loop is represented by an action, `[While]`. The `[While]` action takes two parameters: an action that returns a boolean (the loop condition), and an action (or sequence of Actions) to execute while the condition is true. 

```TACL
[While]{[ConditionAction]{parameters}, [ActionSequence]{parameters}}
```

#### For Loop

The for loop is a bit more complex, as it involves initialization, condition checking, and incrementation/decrementation. We represent this with an action, `[For]`. The `[For]` action takes three parameters: an action that initializes the loop variable, an action that checks the loop condition, and an action that updates the loop variable at the end of each iteration. A fourth parameter is the Action (or sequence of Actions) to execute in each iteration.

```TACL
[For]{[InitializationAction]{parameters}, [ConditionAction]{parameters}, [UpdateAction]{parameters}, [ActionSequence]{parameters}}
```

### Attempt

Given our language structure, we upgraded our try-catch mechanism into a single action. This is done by introducing a new action `[Attempt]` which simultaneously attempts an action and handles any exceptions in one go. The `[Attempt]` action can take two parameters: the action to be attempted and the action to be executed in case of an error.

The syntax looks like this:

```TACL
[Attempt]{[ActionToAttempt]{parameters}, [ErrorHandler]{parameters}}
```

For example, if we have an action `CalculateDistance` that takes two parameters `start_point` and `end_point`, and an error handling action `HandleError`, the `[Attempt]` action would look like this:

```TACL
[Attempt]{[CalculateDistance]{start_point, end_point}, [HandleError]{parameters}}
```

In this case, `CalculateDistance` will be attempted. If it executes without an exception, then the program proceeds normally. But if an exception is thrown, the `HandleError` action is called.

## Appendix: Standard Libary of Actions

### System/Shell/IO Actions

- `<thing1>[Assign]{thing2}`
    - Assigns thing1 the contents of thing2. Can also use `<thing1>{thing2}`.
- `[Assign]{thing1, thing2}`
	- Assigns thing1 the contents of thing2. This is the same as using the assignment context `<>`.
- `[AccessAt]{Pile, Index}`
	- Returns the *Thing* in the given Pile at the given Index. This is the same as using `[Pile](Index)`.
- `<MyAction>[DefineAction]{Input, Default, Body}`
	- Creates an Action using the given Input(s), Default returned *Thing*, and Body. Returns a *Thing*, which could very well be no*Thing*... null.
- `<MyThingType>[DefineThingType]{thing1, thing2, ..., thingN}`
    - Creates an example "MyThingFromType" Thing Type with the sub-things thing1, thing2, ..., thingN
- `<MyThingFromType>[CopyThingType]{ThingType}`
	- Creates an example "MyThingFromType" Thing from the Thing Type ThingType. 
- `[Print]{thing1, thing2, ..., thingN}`
	- Prints the contents of thing1, thing2, ..., thingN to the standard output.
- `[Prompt]{promptString}`
	- Prints the promptString to the standard output and awaits input from the standard input. Returns the line of input. 

### Control Flow Actions

- `[if]{(c)[TestAction]{Parameters}, (t)[ActionIfTrue]{parameters}, (f)[ActionIfFalse]{parameters}}`
	- If-Then-Else.
- `[Attempt]{[ActionToAttempt]{parameters}, [ErrorHandler]{parameters}}`
	- Exception handling.
- `[For]{[InitializationAction]{parameters}, [ConditionAction]{parameters}, [UpdateAction]{parameters}, [ActionSequence]{parameters}}`
	- For Loop.
- `[While]{[ConditionAction]{parameters}, [ActionSequence]{parameters}}`
	- While Loop.

### Mathematical and Logical Operation Actions

- `[Add]{thing1, thing2, ..., thingN}`
	- Adds thing1 and thing2, and thing3 ..., and thingN and returns the Sum.
	- `[Plus]{thing1, thing2, ..., thingN}` will work, too.
- `[Subtract]{thing1, thing2, ..., thingN}`
	- Subbtracts thing1 from thing2, and from thing3, ..., from thingN, and returns the Subtrahend.
	- `[Minus]{thing1, thing2, ..., thingN}` will work, too.
- `[Multiply]{thing1, thing2, ..., thingN}`
	- Multiplies thing1 and thing2, and thing3, ..., and thingN and returns the Product.
	- `[Times]{thing1, thing2, ..., thingN}` will work, too.
- `[Divide]{thing1, thing2, ..., thingN}`
	- Divides thing1 by thing2, by thing3, ..., by thingN and returns the Dividend.
	- `[Frac]{thing1, thing2, ..., thingN}` will work, too.
- `[Increment]{thing, increment}`
	- Increment thing by increment.
- `[Decrement]{thing, decrement}`
	- Decrement thing by decrement.
- `[IsEven]{thing}`
	- Returns true if thing is even, false if thing is odd.
- `[IsOdd]{thing}`
	- Returns true if thing is odd, false if thing is even.
- `[And]{thing1, thing2, ..., thingN}`
	- Returns true if thing1, thing2, ..., thingN are all true, returns false if any are false.
- `[Or]{thing1, thing2, ..., thingN}`
	- Returns true if any of thing1, thing2, ..., thingN are true, returns false if all are false.
- `[Not]{thing}`
	- Returns true if thing is false, returns false if thing is true.
- `[GreaterThan]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is greater than thing2, and if thing2 is greater than thing3, ..., and if thingN-1 is greater than thingN.
- `[LessThan]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is less than thing2, and if thing2 is less than thing3, ..., and if thingN-1 is less than thingN.
- `[Equals]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is equal to thing2, and if thing2 is equal to thing3, ..., and if thingN-1 is equal to thingN.
- `[Unequals]{thing1, thing2, ..., thingN}`
	- Returns true if thing1 is unequal to thing2, and if unthing2 is equal to thing3, ..., and if thingN-1 is unequal to thingN.

--------------------
# GPT-4 Response

**assistant**:
Understood. I've loaded the syntax specification for Thing-Action-Context Language (TACL) into context. I'm ready to assist with converting code into TACL form whenever you're ready to proceed.

--------------------
# User Prompt

**user**:
"morningpod.py"
```python
from bs4 import BeautifulSoup
from datetime import datetime
import os
import requests
import subprocess
from sys import platform 
import time
import vlc

def download_latest_weather_podcast(feed_url):
    response = requests.get(feed_url)
    response.raise_for_status() # will raise an HTTPError if the HTTP request returned an unsuccessful status code
    
    # Parse the feed using BeautifulSoup
    soup = BeautifulSoup(response.content, features='xml')
    # Find the first <item> node
    first_item = soup.find('item')
    # Get the URL of the first enclosure in the first <item>
    audio_url = first_item.find('enclosure')['url']
    
    # Download the audio file
    audio_response = requests.get(audio_url)
    audio_response.raise_for_status()
    
    # Generate a file name based on the current date and time
    file_name = f"weather_podcast_{datetime.now().strftime('%Y%m%d%H%M%S')}.mp3"
    
    # Save the file
    with open(file_name, 'wb') as file:
        file.write(audio_response.content)
    
    return file_name

def play_audio_file(file_name):
    # Define a VLC instance
    player = vlc.MediaPlayer(file_name)
    
    # Play the audio file
    player.play()
    # Wait for the audio to play
    time.sleep(1) # Give player time to start
    duration = player.get_length() / 1000 # Get the duration in seconds
    time.sleep(duration) # Wait for the file to finish playing

def print_text_document(file_path):
    # Ensure the file exists to avoid errors
    if os.path.exists(file_path):
        # Command to print the document
        command = f'notepad /p "{file_path}"'
        os.system(command)
    else:
        print(f"The file {file_path} does not exist.")

def print_text_document2(file_path):
    # Check the OS
    if platform == "win32":
        # Windows command
        command = ["notepad", "/p", file_path]
    elif platform == "linux":
        # Linux command (you may need to change 'lp' to another command depending on your setup)
        command = ["lp", file_path]
    elif platform == "darwin":
        # macOS command
        command = ["lp", file_path]
    else:
        print("Unsupported operating system.")
        return
    
    # Run the command
    try:
        subprocess.run(command, check=True)
    except subprocess.CalledProcessError as e:
        print(f"An error occurred while trying to print the document: {e}")

def main():
    feed_url = 'https://feed.pod.co/usa-weather-today'
    
    # Download the latest weather podcast
    print("Downloading today's weather podcast...")
    audio_file = download_latest_weather_podcast(feed_url)
    
    # Play the downloaded weather podcast
    print("Playing today's weather podcast...")
    play_audio_file(audio_file)

    # Cleanup: delete the audio file after playing
    os.remove(audio_file)

    # Print the daily form
    print("Printing Today's Form...")
    print_text_document('morningpod.txt')

    
    print("Morning routine completed.")

if __name__ == "__main__":
    main()

```

--------------------
# GPT-4 Response

**assistant**:
```TACL
<Main>[DefineAction]{
    <Input> is {}
    <Default><Error>"An Error has occurred."
    <Body>{
        <FeedUrl>"https://feed.pod.co/usa-weather-today"

        # Download the latest weather podcast
        [Print]{"Downloading today's weather podcast..."}
        <AudioFile>[DownloadLatestWeatherPodcast]{FeedUrl}

        # Play the downloaded weather podcast
        [Print]{"Playing today's weather podcast..."}
        [PlayAudioFile]{AudioFile}

        # Cleanup: delete the audio file after playing
        [RemoveFile]{AudioFile}

        # Print the daily form
        [Print]{"Printing Today's Form..."}
        [PrintTextDocument]{"morningpod.txt"}

        [Print]{"Morning routine completed."}
    }
}

<DownloadLatestWeatherPodcast>[DefineAction]{
    <Input>{FeedUrl},
    <Default><Error>"An Error occurred during podcast download."
    <Body>{
        <Response>[GetRequest]{FeedUrl}
        [RaiseForStatus]{Response}
        <Soup>[ParseWithBeautifulSoup]{Response.content, "xml"}
        <FirstItem>[Soup.find]{"item"}
        <AudioUrl>[FirstItem.find]{"enclosure"}["url"]
        <AudioResponse>[GetRequest]{AudioUrl}
        [RaiseForStatus]{AudioResponse}
        <FileName>[FormatString]{"weather_podcast_%s.mp3", [CurrentDateTime]{"%Y%m%d%H%M%S"}}
        [WriteToFile]{FileName, AudioResponse.content}
        <Return>{FileName}
    }
}

<PlayAudioFile>[DefineAction]{
    <Input>{FileName},
    <Default><Error>"An Error occurred while playing the audio file."
    <Body>{
        <Player>[CreateVLCMediaPlayer]{FileName}
        [Player.play]
        [Sleep]{1}
        <Duration>[Player.get_length] / 1000
        [Sleep]{Duration}
    }
}

<PrintTextDocument>[DefineAction]{
    <Input>{FilePath},
    <Default><Error>"An Error occurred while printing the document."
    <Body>{
        [If]{
            (c)[FileExists]{FilePath},
            (t)<Command>[FormatString]{"notepad /p \"%s\"", FilePath},
            (f)[Print]{[FormatString]{"The file %s does not exist.", FilePath}}
        }
        [SystemCommand]{Command}
    }
}

<PrintTextDocument2>[DefineAction]{
    <Input>{FilePath},
    <Default>"Unsupported operating system."
    <Body>{
        [If]{
            (c)[Equals]{[Platform], "win32"},
            (t)<Command> is ["notepad", "/p", FilePath],
            (f)[If]{
                (c)[Equals]{[Platform], "linux"},
                (t)<Command> is ["lp", FilePath],
                (f)[If]{
                    (c)[Equals]{[Platform], "darwin"},
                    (t)<Command> is ["lp", FilePath],
                    (f)[Print]{"Unsupported operating system."}
                }
            }
        }
        [Attempt]{
            [SubprocessRun]{Command, True},
            [Print]{[FormatString]{"An error occurred while trying to print the document: %s", [Error]}}
        }
    }
}

[RemoveFile][DefineAction]{
    <Input>{FileName},
    <Default><Error>"An Error occurred while removing the file."
    <Body>{
        [OsRemove]{FileName}
    }
}

[Main]
```

Please note that for actions such as `GetRequest`, `RaiseForStatus`, `ParseWithBeautifulSoup`, `FormatString`, `CurrentDateTime`, `WriteToFile`, `CreateVLCMediaPlayer`, `Sleep`, `SubprocessRun`, `FileExists`, `SystemCommand`, and `OsRemove`, you would need to define these with the appropriate functionality as they correspond to the Python's requests, os, subprocess, datetime, and vlc library functions and classes. Also, the handling of attributes in TACL, such as `["url"]` and `["content"]`, needs to be adapted to match the TACL's way of accessing properties or elements.
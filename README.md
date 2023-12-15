# Thing-Action-Context Language, or TACL

A Domain-Specific, General Purpose Language to Think and Write In

---

**Corey Naas**, November 2023

https://coreynaas.com/

coreynaas@outlook.com

Copyright © 2023 Corey Naas. All rights reserved.

---

[Specification](specification.md)
[Appendices (original examples)](appendices.md)

Thing-Action-Context Language, or TACL, is a "programming" "language" I designed to act as an "intermediate language" between my brain and a language model or AI that can produce code. I "write" code in plain English, using a simple brackets-only syntax, and give that to the AI to turn into actual code in my target language. I can then review the code, and focus on the last 90% of programming that requires a human mind. The syntax is flexible enough that I can manually "call out" target-language-specific expressions (such as an "AssignType" action that would be required in C-targeted TACL but not in Python-targeted TACL; ) as needed, and focus on declaring what I want to see performed in the target code, as brief as possible and as detailed as required.

It also forces me to think about programming in a semi-abtract way; not quite plain-english pseudocode, but equally not quite a proper language like python, whose syntax is straightforward enough to look like pseudocode at times! The fact that it doesn't exist, and doesn't have truly have any "wrong" ways to use it (the end-goal is that the *AI* understands what you want to do!), makes it so that one can use it however they use language. It doesn't even have to be English! I can take TACL that's written in Korean, translate the words in-place to the syntax, and have code that's logically and expressedly equivalent (depending on the precision of translation, comments, idiosyncratic writing, etc.).

I asked GPT-4 what the "do one thing well" that this language provides is, given the specification, and this is what it said:

> The "do one thing well" for Thing-Action-Context Language (TACL) can be summarized as providing a clear and expressive framework for programmatic instruction and control flow that closely aligns with natural language constructs. It excels at allowing users to define and manipulate data, actions, and contexts with an emphasis on readability and ease of understanding. TACL achieves this through a unique syntax that organizes code into "Things" (data or actions) and their associated contexts.

## Hello World

In this program, we define a `Main` action that takes no inputs. This action simply prints "Hello World!" to the standard output and then returns 0.

```TACL
# Define the action "Main" with the system "DefineAction" action
<Main>[DefineAction]{
	<Input>{myName}
	<Default><Error>"An Error has occurred."
	<Body>{
		[Print]{"Hello World! My name is ", myName, "!"}
		<Return>{0}
	}
}

# Execute the action "Main" with my name as the input
[Main]{"Corey"}

# As output in the command line of your brain:
# > Hello World! My Name is Corey!
```


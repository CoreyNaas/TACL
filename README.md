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

```
<theAcronym>[Acronomize]{"Thing-Action-Context Language"}
[Print]{theAcronym}

## Run the code above in your head and then turn your head or monitor upside down to see the answer below!
ꓶꓛⱯꓕ <
```

Thing-Action-Context Language, or TACL, is a "programming" "language" I designed to act as an "intermediate language" between my brain and a language model or AI that can produce code. I "write" code in plain English, using a simple brackets-only syntax, and give that to the AI to turn into actual code in my target language. I can then review the code, and focus on the last 90% of programming that requires a human mind. The syntax is flexible enough that I can manually "call out" target-language-specific expressions (such as an "AssignType" action that would be required in C-targeted TACL but not in Python-targeted TACL) as needed, and focus on declaring what I want to see performed in the target code, as brief as possible and as detailed as required.

It also forces me to think about and express programming in a semi-abtract way, while thinking through problems; it's more "code-like" than plain-english pseudocode, but not quite a proper "standard" language like python. The fact that it doesn't need to compile, and thus there are no true "wrong" ways to use it (the end-goal is that the *AI* understands what you want to do!), makes it so that one can use it however _they_ use _their_ language. It doesn't have to be English! I could take one's TACL that's written in a language I don't know, like Korean, and translate it to English, giving me a programming-language-agnostic yet still-precise "thought-for-thought" expression of one's code.

The brackets purposefully surround the whole "Thing" name, which allows any sequence of unicode characters to act as names. A whole sentence, with spaces? I won't stop you! Emojis???? Uhm, <👈🏠>[🔥]{⛽🕯}. Most-usefully, it allows for natural and intuitive writing in one's own language, however ordered (LTR, RTL, etc), however expressed natively or idiosyncratically, with only a few reserved characters for delimiting the part-of-speech of TACL. It is thus easily Thing-for-Thing translated into other languages using translators, or into actual code using AI.

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


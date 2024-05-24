# TACL: A Universal Pseudocode Specification

## Introduction
TACL is designed to standardize the way we write pseudocode across multiple domains. The goal is to provide a clear, concise, and domain-agnostic pseudocode specification that can be used by engineers, educators, and students alike.

![helloworldexample](helloworld.png)

## Table of Contents
- [Specification Document](#specification-document)
- [Priming an LLM](#priming-an-llm)
- [Syntax Highlighting](#syntax-highlighting)
- [Examples](#examples)
- [How to Use](#how-to-use)
- [Contribution](#contribution)
- [License](#license)
- [Contact Information](#contact-information)
- [Motivation/History](#motivation/History)
- [Asking the AI](#asking-the-AI)

## Specification Document
The specification document outlines the syntax and structure of TACL. [View the specification document](specification.md) to understand the foundational concepts that shape our pseudocode.

## Priming an LLM
To utilize TACL with an LLM, refer to the `LLM_PRIMING.md` file which includes examples and guidance on how to rewrite user prompts to adhere to our specification.

## Syntax Highlighting
We support syntax highlighting for both VSCode and Notepad++. To install, follow these steps:
- **VSCode**: Instructions here.
- **Notepad++**: Instructions here.

## Examples
A variety of examples can be found in the `/examples` directory. These are real-world applications of TACL, demonstrating its versatility and ease of use.
- [Example: TACLing Conveyors](/examples/tacling_conveyors.tacl)
- [Example: TACLing Latin](/examples/tacling_latin.tacl)
- [Example: TACling Proofs](/examples/tacling_proofs.tacl)

## How to Use
To start using TACL:
1. Familiarize yourself with the specification document.
2. Install the syntax highlighting extension for your preferred editor.
3. Browse the examples to see TACL in action.

## Contribution
Contributions are welcome! If you have ideas for improving TACL, please submit an issue or pull request.

## License
TACL is released under the Apache 2.0 License. See the `LICENSE` file for more details.

## Contact Information
For questions or feedback, please open an issue or reach out via email.

## Motivation/History

Thing-Action-Context Language, or TACL, is a "programming" "language" I designed to act as an "intermediate language" between my brain and a language model or AI that can produce code. I "write" code in plain English, using a simple brackets-only syntax, and give that to the AI to turn into actual code in my target language. I can then review the code, and focus on the last 90% of programming that requires a human mind. The syntax is flexible enough that I can manually "call out" target-language-specific expressions (such as an "[AssignType](/examples/tacling_c_pointers.tacl)" action that would be required in C-targeted TACL but not in Python-targeted TACL) as needed, and focus on declaring what I want to see performed in the target code, as brief as possible and as detailed as required.

It also forces me to think about and express programming in a semi-abstract way, while thinking through problems; it's more "code-like" than plain-English pseudocode, but not quite a proper "standard" language like Python. The fact that it doesn't need to compile, and thus there are no true "wrong" ways to use it (the end-goal is that the *AI* understands what you want to do!), makes it so that one can use it however *they* use *their* language. It doesn't have to be English! I'm able to take a TACL written a language that's new to me, such as Korean, and translate it into English, giving me an abstract yet accurate expression of someone else's foundational thoughts, as written in their own language, and independent of any specific target programming language.

The brackets purposefully surround the whole "Thing" name, and every expression in TACL, which in turn allows any sequence of unicode characters to act as names, with delimiting to separate yet connect "contexts". This makes "variable naming" totally and completely open to creativity. Basic UpperCamelCase? That's my preference, but it's only a preference. A whole sentence, with spaces? I won't stop you! Emojis? Sure, yeah. ONLY variations of the pointing fingers? Actually... `<👈🏠>[🔥]{⛽🕯}`. Most usefully, it allows for natural and intuitive writing in one's own language, however ordered (LTR, RTL, etc.), however expressed natively or idiosyncratically, with only a few reserved characters for delimiting the part of speech of TACL. It is thus easily Thing-for-Thing translated into other languages using translators, or into actual code using AI.

## Asking the AI

I asked GPT-4 what the "do one thing well" that this language provides is, given the specification, and this is what it said:

> The "do one thing well" for Thing-Action-Context Language (TACL) can be summarized as providing a clear and expressive framework for programmatic instruction and control flow that closely aligns with natural language constructs. It excels at allowing users to define and manipulate data, actions, and contexts with an emphasis on readability and ease of understanding. TACL achieves this through a unique syntax that organizes code into "Things" (data or actions) and their associated contexts.

I also asked GPT-4 how other software engineers could use TACL, and *why* they might want to over writing in the target language to begin with:

>1. Pseudocode Replacement: Software engineers often use pseudocode to outline the logic of their code before they implement it in a specific programming language. TACL can replace traditional pseudocode, providing a more structured and consistent way to represent the logic and flow of an application. This could lead to fewer errors when translating the logic into the target language.
>2. Enhancing Readability: TACL's human-readable format can serve as an intermediate representation of complex logic that might be more difficult to express clearly in a traditional programming language. By initially writing the logic in TACL, the engineer can focus on the problem-solving aspect without getting bogged down by the syntax and constraints of the main programming language.
>3. Bridging Communication Gaps: When working in a team, especially in a multidisciplinary setting, TACL can be used to describe system behaviors and algorithms to non-technical stakeholders or colleagues who might not be familiar with the intricacies of the main programming language but are still involved in the decision-making process.
>4. Prototyping: TACL can be advantageous for quick prototyping and testing of ideas. A software engineer can rapidly prototype an algorithm or workflow in TACL to validate its effectiveness before committing to a full implementation in the main programming language, saving time and resources.
>5. Documenting Intent: TACL can be used to document the intent and design decisions of a particular piece of code or system. Writing in TACL can provide a clear and concise explanation that can be referred back to when revisiting the code in the future, or when onboarding new engineers who need to understand the system's architecture.

> Although the final implementation will be in the target language, TACL can enhance the preliminary stages of software development, making the transition from concept to code smoother and more reliable.
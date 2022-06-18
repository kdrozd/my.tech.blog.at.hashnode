## What are Domain Specific Languages (DSLs)?

First, what is Domain Specific Language? 

> A Domain Specific Language is a programming language with a higher level of abstraction optimized for a specific class of problems. A DSL uses the concepts and rules from the field or domain.

This is the nice and short definition of a DSL. But then

> How are Domain Specific Languages different from "real" programming languages?
> 
> A Domain specific language is usually less complex than a general-purpose language, such as Java, C, or Ruby. Generally, DSLs are developed in close coordination with the **experts** in the field for which the DSL is being designed. In many cases, DSLs are intended to be used not by software people, but instead by non-programmers who are fluent in the domain the DSL addresses.

So both quotes come from Jetbrains MSP page: https://www.jetbrains.com/mps/concepts/domain-specific-languages.

I added emphasis on **experts** as they are in the center of DSL development process. DSL is created with their help and for them to easily express domain knowledge in a way that is easy to understand by both humans (experts) and computers.

So let's look on examples from  first page of Google results for phrase "Domain Specific Language" just to keep this article simple, and who is actually looking beyond first page?

## Wikipedia

- GameMaker Language
- ColdFusion Markup Language
- Erlang OTP
- FilterMeister
- Unreal Engine before version 4 and other games
- Gherkin

## opensource.com

- HTML
- sh, Bash, CSH, and the likes for *nix; MS-DOS, Windows Terminal, PowerShell for Windows
- XML
- UML
- SQL and its variants
- Drools
- Verilog, VHD
- Maven, Gradle
- MATLAB (commercial), GNU Octave, Scilab
- Lex, YACC, GNU Bison, ANTLR

## tomassetti.me

- DOT
- PlantUML
- SED
- gawk
- Gherkin
- Website-spec
- SQL
- HTML
- CSS
- XML
- UML
- VHDL
- ANTLR
- make
- Latex
- OCL
- BPEL

## And so one

There is a pattern in all those examples, they are all referring to programming in some way. As in *Domain Specific **Programming** Language*.  I think we can do better. If someone is Erlang, ANTLR (irony), T-SQL, YACC expert then he can programming :) 

## Different set of examples

All examples are correct, or at least I'll not argue with them. But let's bring domain experts closer to our world (computers) and let's do something together, I know strange new worlds.

### Music note

![sNg-tGHg5.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1655575836852/FXiiQKe8I.jpeg align="left")

This is a clear example of DLS outside the computer realm, used for years to write music. Composers us them to compose music - and they are the **experts**. We can help them and digitalize those notes and feed them for example to MIDI players or help them convert it from single instrument to band or orchestra. 

### Chemical equation

> A chemical equation is the symbolic representation of a chemical reaction in the form of symbols and formulae, wherein the reactant entities are given on the left-hand side and the product entities on the right-hand side with a plus sign between the entities in both the reactants and the products and an arrow that points towards the products, and shows the direction of the reaction

![Zrzut ekranu z 2022-06-18 20-16-46.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655576233906/v7i-HctQK.png align="left")

Chemist know what to expect from them and what products look like. ChemDSL (made up name) can convert this notation to visual notation.


![Zrzut ekranu z 2022-06-18 20-30-23.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655577041382/vMOc3J53q.png align="left")

Provide visualizations:

![Zrzut ekranu z 2022-06-18 20-25-32.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655576763182/GAqLnYCsQ.png align="left")

Take a look at https://en.wikipedia.org/wiki/Simplified_molecular-input_line-entry_system


## It's life

This list can go and go.

- Mathematical equations, check what Wolfram can do with them
- Human languages - NLP - Natural Language Processing - it's a thing
- Mathematical equations  - Physics as some as well
- Phonetic notation - tells you how to spell words 
- Sign language - for telling without spoken words
- Baseball score keeping - I'm surprised to: https://en.wikipedia.org/wiki/Baseball_scorekeeping#Language
- chess notations  - https://en.wikipedia.org/wiki/Chess_notation#Notation_systems_for_humans
- dance and juggling - few actually
- slangs - https://www.urbandictionary.com/ ;)
- ...

They are everywhere in or daily lives and almost every one uses them, no matter where are you or who are you. So next time, when someone tells you that they don't use DSL - tell them they probably do. 

And when you are lucky they do it for business and some automation, visualization, transformation or version control may be handy, and you can help them with the right tool.


## Links

- https://www.jetbrains.com/mps/concepts/domain-specific-languages/
- https://en.wikipedia.org/wiki/Domain-specific_language
- https://opensource.com/article/20/2/domain-specific-languages
- https://tomassetti.me/domain-specific-languages/
- https://people.cs.ksu.edu/~schmidt/505f12/Lectures/DSLS.html
- https://stackoverflow.com/questions/809574/what-is-a-domain-specific-language-anybody-using-it-and-in-what-way
- https://en.wikipedia.org/wiki/Musical_note
- https://xaktly.com/ChemicalNotation.html
- https://en.wikipedia.org/wiki/Simplified_molecular-input_line-entry_system
- https://pubchem.ncbi.nlm.nih.gov/pc3d/


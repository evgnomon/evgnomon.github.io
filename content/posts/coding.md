---
title: "Coding"
tags: ["usecode"]
aliases:
  - /coding/
  - /coding/index.html
---

# Coding

> Any programming language that is not used to develop the interpreter/compiler and the tool chain of that language is already dead!

If you use command line to perform your work, you will realize that it is much easier to automate repetitive tasks by writing small scripts.
That script is a function which saves you writing repeated commands. And that is all about programming, making functions to save time.

As there is a lot of programming languages, you need to choose one to start with, therefore you will choose one that you can create any other sort of functions with! This is the first building block of programming.
However you are not going to start from scratch as there is already many functions created by other people that you can use to build your own functions. We are not in the stone age anymore to start from zero!
I suggest starting with Python as you can automate almost everything with it, no heavy lifting. You can automate your own tasks and use APIs, databases, files, etc to produce your desired result and send/receive messages to/from other services. And create your own APIs and host it for users. Python is a very flexible language fitting to various programming paradigms (procedural, object-oriented, functional, etc) that you can choose from. There are many libraries available to help you achieve your goals faster. And it is easy to learn and read as it copes rather with your paradigm of thinking than forcing you to think in a certain way.

But you can not create all sort of APIs with Python! For example if you want to create a mobile app, you will need to learn Swift (for iOS) or Kotlin/Java (for Android). If you want to create a web front-end, you will need to learn JavaScript (or TypeScript) along with HTML and CSS. If you want to create a game, you might want to learn C# (with Unity) or C++ (with Unreal Engine). Each programming language has its own strengths and weaknesses, and is suited for different tasks. We need to add more languages to out stack. We apparently do not need to learn 100 languages for the same task, preferably one language that can do it all. But in reality, each language has its own ecosystem and community, and some tasks are better suited for certain languages. Therefore, it is good to have a basic understanding of multiple languages, at least not being limited to Python! But how many programming languages should one learn? It depends on your goals and interests. But what should be the goal and the interest for the purpose of UseCode .Dev? And how to choose the right languages?

Python hits scalability and performance issues when it comes to large scale applications and high performance requirements. Specially when you have no control over the host system. And when you have no control over the host system, you are not only fighting performance, you are also shipping your code into a machine you can not prepare. Therefore, we need to add a language that compiles to a self contained binary and stays fast on someone else's laptop. I suggest Rust.

The goal of UseCode .Dev is to empower you to create your own solutions and tools and contribute to a single branch of code. As we do not have any limitation over what is part of UseCode .Dev, we need to choose a set of programming languages that can cover a wide range of tasks and use cases and minimize the number of languages to learn. This reduces the barrier to entry as a developer. To minimize the number of languages we learn, we can prefer one eco system over another. For example if we prefer web over mobile, we can choose JavaScript/TypeScript as our main language as it can be used for both front-end and back-end development. We can release our work on the web earlier than other platforms and fund further development on other platforms. Or even use Terminal which eliminates the need for a graphical user interface!

AI is UI (and should be). Entering structured information is still difficult, but you can ask AI to generate a form to enter information! And share the form with others to use the same format. And we shouldn't need anything further than a simple unified UI to interact with AI. Preferably browser based to support languages and terminal based if the userbase is developers. Preferably all serverside so we can use Python without adding a new client stack. To have them two we need to aim to use MCP. We still need MCP and API even if we target our own UI. As we are developers, we can start with a simple TUI to use the app and leave the browser after getting users! So we can start with Tool/API development using Python and release with server generated HTML/CSS pages with minimized JavaScript. We do not need to wait for web front or mobile apps to get users! We can also use Rust when we want to make a building block for other developers to use in their own systems, or when the tool has to run on the user's own machine.

But what is left that we can not do with Python/Rust? I would say the domains that already belong to C/C++: operating systems, demanding embedded systems, codecs, engines, drivers, and the large body of existing C/C++ code that nobody is going to rewrite. C/C++ remains for those demanding domains. Rust does not remove C/C++ from the stack, it removes the reason to start something new in it.

But which one is a fit when Python and Rust both work? We use Python when the wheels are just there. If the ecosystem already ships the thing we need and the only work left is to call it, writing it again in Rust is a loss, not a win. Everything else is Rust. The same rule applies on the other end: TypeScript for client side editing, because the browser is a domain where the ecosystem is already there and the code has to run there anyway.

## Language selection always comes with tradeoffs

There is no language that wins on every axis. Every choice we make is a trade, not a victory, and pretending otherwise is how a stack ends up with ten languages and no answer to which one to open.

The one thing we do not trade away is this: we do not want to replicate logic cross language. Two implementations of the same rule drift, and the drift is silent. So the rule is one language per domain. The domain picks the language once, and everything in that domain is written in it. The question is then not "which language is best", it is "which tradeoff am I willing to pay in this domain".

We release code for users to run on their laptop. That is the deciding constraint. It rules out a runtime the user has to install first, and it rules out shipping a garbage collector and a heavy runtime into an environment we do not control. It wants one static binary, predictable memory, and a toolchain that cross compiles without a story. So we need Rust.

Zig would be the leaner answer, and for a while this article gave that answer. But we do not have the time to spend on Zig. The language is still moving, the ecosystem is still thin, and the hours go into the language instead of into the product. We prefer the higher performance ceiling and the mature ecosystem even though it makes the code a bit more complicated. We can afford that complication because the code is assisted by coding agents. Lifetimes, the borrow checker and the verbosity are exactly the kind of cost an agent absorbs well. A missing library or an unstable API is a cost nobody absorbs.

So: Rust by default. Python when the wheels are just there. TypeScript for client side editing. C/C++ for the demanding domains that are already its own. And we keep Zig for where Rust is not as easy as Zig to reach a certain optimization: talking to C directly, comptime, exact control over layout and allocation. That is a narrow slot and it should stay narrow.

## Recommended Learning Path
- Learn Rust first. It is the default for anything we ship to a user's laptop, any service, and any building block other developers link against.
- Use Python when the wheels are just there. Automate your tasks, call the libraries that already exist, work with databases and files, and get stuff done without heavy lifting.
- Learn HTML/CSS to fill all screens, and TypeScript for client side editing. Minimize JS by progresively adding `htmx` and `Scss` to your HTML pages. Add web components to fix the corner case as the last resort.
- Learn C/C++ for the demanding domains that are already written in it, and for low-level programming that has no other home.
- Learn Zig for the cases where Rust is not as easy as Zig to reach a certain optimization, and for binding C libraries conveniently.
- And of course Bash scripts to glue everything together!

Note: Go is dropped from the stack. It is a good language, but its slot — a compiled, easy, concurrent service language — overlaps almost entirely with Rust, and keeping both means writing the same logic twice in two languages, which is the one thing we said we would not do. And do not read the rest of this as a hunt for the one language to end the list. There is no single language because there is no single domain. One language per domain is the rule, and the number of languages we keep is simply the number of domains we actually work in — not one, and not one hundred either.

- [Class](classes/)
- [Struct](structs/)

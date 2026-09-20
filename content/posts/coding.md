---
title: "Coding"
tags: ["usecode"]
aliases:
  - /coding/
  - /coding/index.html
---

# Coding

> The domain picks the language.

There is no language that wins on every axis. Every choice we make is a trade, not a victory, and pretending otherwise is how a stack ends up with ten languages and no answer to which one to open.

The one thing we do not trade away is this: we do not want to replicate logic cross language. Two implementations of the same rule drift, and the drift is silent. So the rule is one language per domain. The domain picks the language once, and everything in that domain is written in it. The question is then not "which language is best", it is "which tradeoff am I willing to pay in this domain".

We release code for users to run on their laptop. That is the deciding constraint. It rules out a runtime the user has to install first, and it rules out shipping a garbage collector and a heavy runtime into an environment we do not control. It wants one static binary, predictable memory, and a toolchain that cross compiles without a story. So we need Rust.

Zig would be the leaner answer, and for a while this article gave that answer. But we do not have the time to spend on Zig. The language is still moving, the ecosystem is still thin, and the hours go into the language instead of into the product. We prefer the higher performance ceiling and the mature ecosystem even though it makes the code a bit more complicated. We can afford that complication because the code is assisted by coding agents. Lifetimes, the borrow checker and the verbosity are exactly the kind of cost an agent absorbs well. A missing library or an unstable API is a cost nobody absorbs.

So: Rust by default. Python when the wheels are just there. TypeScript for the browser. C/C++ for the demanding domains that are already its own. And we keep Zig for where Rust is not as easy as Zig to reach a certain optimization: talking to C directly, comptime, exact control over layout and allocation. That is a narrow slot and it should stay narrow.

## Recommended Learning Path
- Learn Rust first. It is the default for anything we ship to a user's laptop, any service, and any building block other developers link against.
- Use Python when the wheels are just there. Automate your tasks, call the libraries that already exist, work with databases and files, and get stuff done without heavy lifting.
- Learn HTML/CSS to fill all screens, and TypeScript for everything that runs in the browser. This used to say to minimize JavaScript and progressively add `htmx` and `Scss` to plain HTML pages. That is no longer the rule: just use TypeScript. Minimizing JS was a way of buying down maintenance cost, and the cost it was buying down now lands mostly on the agent, not on us. Most of the code is agentic, so the flexibility that comes with TypeScript is worth the maintenance burden it carries.
- Learn C/C++ for the demanding domains that are already written in it, and for low-level programming that has no other home.
- Learn Zig for the cases where Rust is not as easy as Zig to reach a certain optimization, and for binding C libraries conveniently.
- And of course Bash scripts to glue everything together!

Note: Go is dropped from the stack. It is a good language, but its slot — a compiled, easy, concurrent service language — overlaps almost entirely with Rust, and keeping both means writing the same logic twice in two languages, which is the one thing we said we would not do. And do not read the rest of this as a hunt for the one language to end the list. There is no single language because there is no single domain. One language per domain is the rule, and the number of languages we keep is simply the number of domains we actually work in — not one, and not one hundred either.

- [Class](classes/)
- [Struct](structs/)

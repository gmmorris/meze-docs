# Componentisation

Several months ago I gave a talk at one of our fortnightly **Unruly Tech Talks** about a topic that I had been mulling around in my head for several months prior.
The topic was that of an architecture abstraction, triggered by my adoption of the *React* library in order to declaratively construct user interfaces.

But, before we talk about technical stuff, I'd like to ask you an existential question as a developer.

**What's the core of our job as developers today?**

It probably **isn't** is *figuring out the next super cool & complex algorithm.*

But rather, what our job probably **is**, is to *take an existing abstraction and compose it with a second abstraction in order to form a third abstraction*.

## modularisation

I've been using *React* for a couple of years now, following many years of evangelising *Backbone* as a solution to the problems my clients and employers had been facing when tackling their Front End architectures. As a relatively early adopter of Backbone, in early 2011, I found the move from a messy soup of global Javascript objects with complex prototypical hierarchies, to a structured MVC (or rather, MVP) pattern an extremely pleasing step forward.

Backbone allowed us to focus less one how the pieces of our code fit together, and more on what they actually did. It did this by abstracting away a lot of the boilerplate and defining a clear API for each piece of our system.
This might seem obvious in hindsight, but at the time this felt groundbreaking, mostly because we were so used to Front End code existing as *a pile of code held together by duct tape* that we accepted our fate and found it hard to see that a better options existed.

But the key *unique selling point* of Backbone, beyond removing boilerplate and an enforced API, was the fact that it lay the ground work for proper **modularisation** of our Javascript codebases.

Modules are a corner stone of good code structuring, as they encourage us to break our code down into logical pieces. This makes it easier for us to write maintainable code that's easier to reason about, to test and to reuse.


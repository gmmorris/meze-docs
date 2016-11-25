# The magical world of Componentisation

Several months ago I gave a talk at one of our fortnightly **Unruly Tech Talks** about a topic that I had been mulling around in my head for several months prior.
The topic was that of an architecture abstraction, triggered by my adoption of the *React* library in order to declaratively construct user interfaces.

But we'll get to *React* in a moment. First I'd like to ask you an existential question.

**What's the core of our job as developers today?**

It probably **isn't** is *figuring out the next super cool & complex algorithm.*

But rather, what our job probably **is**, is to *take an existing abstraction and compose it with a second abstraction in order to form a third abstraction*.

## Modularisation

I've been using *React* for a couple of years now, following many years of evangelising *Backbone* as a solution to the problems my clients and employers had been facing when tackling their Front End architectures. As a relatively early adopter of Backbone, in early 2011, I found the move from a messy soup of global Javascript objects with complex prototypical hierarchies, to a structured MVC (or rather, MVP) pattern an extremely pleasing step forward.

Backbone allowed us to focus less one how the pieces of our code fit together, and more on what they actually did. It did this by abstracting away a lot of the boilerplate and defining a clear API for each piece of our system.
This might seem obvious in hindsight, but at the time this felt groundbreaking, mostly because we were so used to Front End code existing as *a pile of code held together by duct tape* that we accepted our fate and found it hard to see that a better options existed.

But the key *unique selling point* of Backbone, beyond removing boilerplate and an enforced API, was the fact that it lay the ground work for proper **modularisation** of our Javascript codebases.

Modules are a corner stone of good code structuring, as they encourage us to break our code down into individual logical pieces. This makes it easier for us to write maintainable code that's easier to reason about, to test and to reuse.

## Rachel's Trifle
Backbone, though, as it turned out, was not the be-all and end-all solution to our problems.

While we leveraged the benefits of MVC and other patterns to lay out our architecture into multitiered Object Oriented designs, striving for separation of concerns by layering our modules, designing inheritance chains meant to improve code reuse
and reduce complexity, we would inevitably hit the same wall.

As a codebase would grow, requirements changed and assumptions were discovered to be incorrect, we often find that our abstractions begin to fail us.

What we would initially envision as a well thought out and layered Trifle, turned out to be more a mixed up recipe, where layers don't quite make sense anymore, they end up seeping into the layers above and bellow them and something just doesn't taste quite right anymore. This in turn makes it harder to reuse code, to test it and to maintain it.

![](https://media.giphy.com/media/4OW5VatORVtkI/giphy.gif)
*Rachel's Trifle? Good. **Code Trifle**? Bad.*

In other words, our code would develop a smell... the unmistakable smell of a Custard, Jam, Mashed Potatoes and Meat dessert.

## Wait, but why?
Einstein never actually said that *insanity is doing the same thing over and over again and expecting different results*, but I'd like to think that he would agree that if we find ourselves repeating a mistake, we should probably rethink our approach.

I tried to identify the root causes for why, I believed, so many of the teams I'd worked on ended up with these code smells.

**Building complex and / or distributed state machines**
We often try to manage state in many different places and try to reconcile this state throughout the lifecycle of the application. This is hard to do well, and leads to many implicit assumptions which easily break.

**Big bags of instruction rather than atomic declarative pipes**
Instruction are easy to follow, but not always easy to understand. They usually describe *how* something is done, rather than *why*, and the developers are left to figure out the *why* themselves. We've all found ourselves doing this, referring to it as *reverse engineering own our code* and we often misinterpret the *why*.

**Terrible dependency chains reducing our ability to make atomic components**
We often find it hard to make truly atomic pieces of code as they have an inherent *need* for a piece of data or operation that is the concern of another piece of the code. This dependency will always exist in a complex system, but in the absence of a clear API for bridging these dependencies without creating a cohesive coupling between the two pieces of code, this can lead to dependency chains which are hard to reconcile.

**Trying to predict the future**
By far the biggest culprit for the dank code smell is a habit developers have of trying to predict how their code will be used instead of focusing on what is needed. This can lead to many problematic implementations, but most of all it leads to over engineering of solutions, which often leads to code that is very hard to *delete* later.
I'm a firm believer that the best code is code that can easily be deleted and over engineering often makes that much harder to do.

### Searching for answers
Having boiled down my problem to its root causes, the next step would be to figure out what I could do to reduce their impact on how I write my code.
When looking at the aforementioned points, I believe they can be reduces to one core issue, which is that my code would often end up with **High Efferent Coupling & Fragmented State**.

Which begged the question:
***How on earth do we reduce our efferent coupling & fragmented State?***

Searching high and low for an answer I hit the internet, the books, the tech talks, my dad (I didn't literally hit my dad, I just asked his opinion, as he's been writing code since the 70s, presumably with hippie hair and a spliff) and found that there are in fact many possible answers to this question.

I won't enumerate all of them, but one answer would show up repeatedly, and that was a quote which I'd heard so many times before I found it *eye-roll inducing*.

> **Favor 'object composition'**
> **over 'class inheritance'**







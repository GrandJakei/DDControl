# DDControl
DDControl, as Document Denpendence Control

Let's begin with a scene that I had headache about.
I'm a internship of a company, an internet one.
One day I want to search a internal concept of the company, for example, cola.
From the company document system, i get `cola doc`, then:
* `cola doc` tells me cola is a carbonated beverage, then I get a `carbonate doc`
* `carbonate doc` tells me carbonate is formed when carbon dioxide reacts with water, then i get `carben dioxide doc`
* finally i open `carben dioxide doc`, it says carben dioxide doesn't exist now, scientists have replaced this concept with "OCATO" half year ago, short for "One Carbon And Two Oxygens".

There are some dependences between these documents, but when the concept carben dioxide was abandoned, `carbonate doc` doesn't know this and changes nothing.
DDControl is what I suppose to help solving this problem.

There is my temporary design：

![Describe](https://user-images.githubusercontent.com/44257783/203105873-772651f3-2f1a-4341-b226-b1718d83c04d.png)

Like the image shows, when we write a new document, we can add some depends on it. When a document changes, it can set the following type of this change:
1. expand. Change won't change the meaning or usage of the original concept.
2. notice. Change may interfere with the original concept.
3. discard. Origin concept was discard or deleted.
4. passed discard. One or more documents were discard in upstream of the dependency chain.

The special design is, `discard` is transferable， when document `D` has a discard change, all documents depends on `D` will see `D` is `discarded`, let's say that the set of these documents is set `S`, then all downstream documents of `S` will see `passed discard`.

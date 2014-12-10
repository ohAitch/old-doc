Overview
===

Arvo is our operating system. 

[overview of how cards, etc get passed around]

Have you ever wondered what all these kernel modules are about?  What services
they provide?  What fundamental human desires they satisfy?  If so, this is the
doc for you!

The basic purpose of a vane is to present an interface to clients for some
well-defined, stable, and general-purpose piece of functionality.  There are
three types of clients:  Unix, apps, and other vanes.  They all communicate
using a message-passing system we call the "card" system, which you may or may
not have read about elsewhere in our docs.  Unix, apps, and vanes send cards to
each other in message-passing style to communicate.  All meaningful
communication happens through these messages.  Thus, anything you might want to
do with a vane is exposed through its definition of `++kiss`, which defines the
types of cards it accepts.

As of this writing, we have seven vanes:  `%ames`, `%clay`, `%dill`, `%eyre`,
`%ford`, `%gall`, and `%time`. 
---
layout:     post
title:      Notes and Quotes 1
date:       2014-11-25
categories: notes-and-quotes
---

A recurring column for those moments when I’m watching a conference talk (from <a href='http://confreaks.com/' target='_blank'>confreaks</a> or elsewhere) and enjoying / resonating with it so much I end up taking notes…

---

<a href='https://www.youtube.com/watch?v=FH-4AHAwp7w' target='_blank'>TDD for Your Soul: Virtue and Web Development with Abraham Sangha at Madison+ Ruby</a>

… more philosophy than tech, but thought-provoking.

~ ~

Alasdair McIntyre, “After Virtue”

“Who am I?  
Who ought I to become?  
How ought I to get there?”

~ ~

Ralph Ellison:

“The blues is an impulse to keep the painful details and episodes of a brutal experience alive in one’s aching consciousness, to finger its jagged grain, and to transcend it, not by the consolation of philosophy but by squeezing from it a near-tragic, near-comic lyricism.”

~ ~

“We’re inviting criticism of ourselves, we’re inviting evaluation of our weaknesses,  by TDDing our soul, by writing these tests, seeing where we fail, and trying to implement habits to address these failures: that can be a shameful process. … If you don’t believe you’re good enough, you’re stuck, then why would you invite more pain into your life through this process, so why not just skip it. … But there’s a possibility that pursuing this will actually give us a sense of buoyancy.”

---

<a href='https://www.youtube.com/watch?v=lZ0UYq2UJUw' target='_blank'>Alchemy and the Art of Software Development with Coraline Ada Ehmke at Madison+ Ruby</a>

Going back in pattern languages before Christopher Alexander to Gottfried Wilhelm von Leibniz (1646-1716): “every complex idea is composed of sets of simpler ideas”

“alchemy is about transforming base matter, like the stuff that we’re made of, into something more closely approaching divine perfection.  That ‘lead into gold’ nonsense was actually part of the pitch that alchemists made to the VCs of their era.  They called them royalty, I’m not quite sure why.  And this idea that ‘I can take base metal and transmute it into gold?  Here: I’ll give you all this money for your metaphysical experiments.  I don’t care.’  So they were pretty smart.”

“The Divine Pymander, ascribed to Hermes Mercurius Trismegistus. … It contains seventeen tracts, which talk about things like divinity, humanity, idealism, even monads.”

“we impose our will on the universe, we create a structure that we want to impose on chaos, and the manifestation of that begins in harmony, but slides towards disharmony, because every object in every system is corruptible. … the code is corruptible.”

“all that is apparent, is what was generated or made. … the system does not contain information about the ideals that led to its creation.  Unless we are very deliberate about recording our intention and our design, that information is lost, and all we are left with is a system that we don’t understand any more.”

“Christopher Alexander the architect said that a builder should start with the roughest sketch of a building, and by processes that are known to the brain through the pattern language, execute the construction of the building.  All things that are are but imitations of truth.  The systems we build are reflections of the world.  Software system is not and cannot be a single source of truth.”

“Really, alchemy and software development are about identifying ideals, identifying particulars, creating taxonomies, studying them, creating a system for classifying every single thing in a limited or expansive universe.”

“The Divine Pymander ends with this: ‘The Image shall become thy Guide, because Sight hath this peculiar charm, it holdeth fast and draweth unto it those who succeed in opening their eyes.’ I would translate this as ‘The metaphors guide us.  Information is there, and ideas want to be recognized.’  I think that the metaphor of alchemy holds true with what we do.  Just like alchemy, software development is an inquiry into the essential nature of reality.  We break it down, we salve it coagula, we break down complex things into simpler things, we recombine them in novel ways, and we produce an effect on the world, on ourselves.”

“Let’s … dive into disciplines that we have no idea what they even mean, explore them, mine them, find tenets and metaphors, tools that we can use in problem solving, that we can apply to enrich our art, our science, our own magnum opus.  Maybe when we do that, we can find that the raw stuff of digital creation can be transmuted into something that more closely approaches perfection.”

---

<a href='http://confreaks.com/videos/4662-nickelcityruby2014-aesthetics-and-the-evolution-of-code' target='_blank'>Aesthetics and the Evolution of Code: Coraline Ada Ehmke, Nickle City Ruby 2014</a>

Aesthetics of code: correctness, performance, conciseness, readability.

~ ~

So how do we measure elegance?  How about a graph with four lines/axes spreading from the origin, correctness “north”, performance “south”, conciseness “west”, readability “east”.  If you can measure and grade those four aesthetics on a numeric scale, then the most elegant code will cover the largest space on the graph

~ ~

Why does it matter?  Einstein said: “After a certain level of technological skill is achieved, science and art tend to coalesce in aesthetic plasticity and form.  There greater scientists are artists as well.”

---

<a href='http://confreaks.com/videos/4659-nickelcityruby2014-how-to-be-an-awesome-junior-developer-and-why-to-hire-them' target='_blank'>Eric Stiens’s Nickel City Ruby Conference 2014 talk “How to be an Awesome Junior Developer (and why to hire them)”</a>

~ ~ 

Mentoring

Don’t hire a junior developer you can’t mentor.  It’s not fair to them.  It’s not fair to your team.  Everybody loses.

---

<a href='http://confreaks.com/videos/4658-nickelcityruby2014-keynote-multitudes' target='_blank'>Sarah Mei’s Nickel City Ruby Conference 2014 talk “Keynote: Multitudes”</a>

Should you always use attr\_reader to access an instance variable rather than accessing it directly, as a good object-oriented principle, because by only accessing it by sending a message you have created a seam which makes it easier to change anything about the implementation later?  A good application developer (e.g. Sandi Metz) would very likely say yes.  A good library developer (e.g. Jim Weirich) might say no, because adding attr\_reader to a class makes data manipulation public, and once it’s public it has to be supported for ever, because people will use it.  (And if you do change it, and you’re using semantic versioning, you have to change the major version.)

“So people who write gems have developed a system where they have a very minimal interface, with a very rich set of internal abstractions, which they can use while providing this very minimal external interface.

“So these are just two different approaches to programming \[application style at one end, gem/library style at the other\], and what we’re starting to see here is there is a spectrum of rubyists, and there is a spectrum of projects: people will write different code at different points of the spectrum at different times, and what the spectrum is measuring is the surface area of our interface.  And it seems like a fairly simple distinction but it does produce a huge difference in code structure.  And what it means is that sometimes someone who is good at one side of this spectrum will not automatically be good at the other side, right away. … Why does this matter? … Having these endpoints helps us define what else there is.  For example, there’s a middle here, and that middle is suddenly quite obvious, actually, and that’s external APIs on Rails apps.  Many Rails apps now need some kind of programmatic interface that is versioned, and minimal, because once it’s out there, and it’s got users, you’re stuck supporting it, forever. … And the reason people struggle with external APIs for Rails apps is that it is partially application development and it is partially gem-style development, and there aren’t very many people that are good at both.”





Exciting that Sarah Mei and Sandi Metz are writing a book: <a href='http://lnc.hr/Fe9gV' target='_blank'>Practical Rails Programming</a>.

---


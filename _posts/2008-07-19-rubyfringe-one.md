---
layout:     post
title:      RubyFringe, day one
date:       2008-07-19
categories: conference
---
**Jay Phillips** talked about Adhearsion, his framework for integration VoIP building on top of and simplifying the use of Asterisk. He noted that it can be surprisingly profitable to find a pain point a bit off the beaten track and fix it. This chimed well with Zed Shaw’s remark from QCon London 2007 that if you want to succeed beyond your wildest dreams, you should find a problem and solve it in a way which is less painful than any of the competing alternatives.

**Dan Grigsby** noted that entrepreneurship was easier for a developer than perhaps it had ever been, because the sweet spot for team size was about 3. If you’re a really good programmer, all you need on the code side is one or two other really good programmers. This matches Pete McBreen’s point in _Software Craftsmanship_, that a smaller team of really good people will probably be better and more productive than a larger team. The trick that corporations don’t seem to have solved yet is finding that small great team in the first place.

Grigsby added that a more pragmatic test-driven approach to the developer’s dilemma of picking the winners among all the possible project ideas is to build a whole bunch of narrowly-focussed projects, send them out, measure them to within an inch of their lives, and quickly kill off the failing ones. For a similar amount of effort as honing one or two projects for a much longer period before sending them out, you’re left with a couple of projects that are less well developed but you already _know_ they are successful.

Grigsby’s engaging talk continued into more explicitly market-focused directions, discussing finding hacks in the market for the disproportionate reward, suggesting that there are marketing techniques that match Ruby’s better-known programming claim to 10x better productivity, and that exploiting non-obvious relationships was among them.

**Tobias Lütke** spoke about memcached.

**Yehuda Katz** spoke about several neat projects, from Merb and DataMapper (coming to 1.0 this summer so almost no longer Edge-y) to sake (for system-wide rather than project-specific rake tasks), thor (scripting in Ruby), YARD (a neat-looking better Ruby documentation tool), and johnson (a ruby-javascript bridge).

**Luke Francl** spoke on <a href='http://railspikes.com/2008/7/11/testing-is-overrated' target='_blank'>testing being over-rated</a>. He made clear that testing is great, it’s just that there are a lot of other things we need to do (code inspection, usability testing, manual testing), some of which will find different bugs and none of which will find all the bugs. As he pointed out, you can have the most complete set of unit tests imaginable, and it won’t tell you if your app sucks. Sitting and watching a user interacting with the app may be the only way of being sure of that. Francl also pointed out that in addition to writing code and writing tests, developers are good at criticizing the code of others, and the best measure of code quality may be not rcov stats but the number of WTFs per minute in a code review. And, as a side benefit, knowing that your code will be subject to a code review will probably make you tighten up your code in anticipation. (Francl’s paper was also notable for following the _Presentation Zen_ advice of having clear uncluttered slides and a handout that was an efficient text summary of the presentation that bore no relation to the slides at all.)

**Nick Sieger** spoke about <a href='http://blog.nicksieger.com/articles/2008/07/19/jazzers-and-programmers/' target='_blank'>Jazzers and Programmers</a>. Go read his summary and savour the quotations (from a different field but still deeply appropriate) from great jazz musicians. “Learn the changes, then forget them” (Charlie Parker). Or the idea of _The Real Book_ (the body of tunes that all jazz musicians learned and created a shared vocabulary that allowed musicians to play together on their first meeting) as the _GoF_ for jazzers in the 70s.

**Obie Fernandez** spoke about marketing and practical details of contracts. Not only about accepting contracts but about rejecting them, noting that a key acceptance criterion should be if you’re going to want to show off the project when it’s done and keep it in your portfolio. Following on from patterns and _The Real Book_, he noted the importance when setting up a consultancy of defining projects and of having names for them, and of writing down your client criteria and acceptance criteria and keeping them constant. Noted _Secrets of Power Negotiating_, _Predictably Irrational_, and Seth Godin’s _Purple Cow_ as books to check out.

**Matt Todd** spoke about the importance of just going ahead and making mistakes and learning from them. (Going back to one of Sieger’s quotations, as Ornette Coleman put it, “It was when I found out I could make mistakes I knew I was on to something.”)

**Jeremy McAnally** spoke of how we should resist the urge to make Rails do everything, even outside its comfort zone where it would be a lot simpler and more maintainable to, say, just write some Ruby code and hook it up to with Rack. How Rails is designed for database-backed web apps, and taking it outside of its 80% comfort zone, while perfectly possible, may not be the best solution, and if you find yourself in a place where the joy:pain ratio has flipped or where you find you’re writing more spaghetti code to fit the solution into Rails than you would be to write the solution on its own, it’s probably time to switch.

**Zed Shaw** briefly presented some dangerous ideas and then went on to an impromptu music-making session. He left us with the thought that while he was done with Ruby, he was never going to stop coding, because code was the only artform that you could create that other people could then play with.

Joey deVilla’s more expansive account: <a href='http://globalnerdy.com/2008/07/20/rubyfringe-day-1-notes-part-1/' target='_blank'>one</a>, <a href='http://globalnerdy.com/2008/07/20/rubyfringe-day-1-notes-part-2/' target='_blank'>two</a>.

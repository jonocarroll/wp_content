---
ID: 460
post_title: What are the odds?
author: Jonathan Carroll
post_date: 2015-03-10 08:00:20
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2015/03/10/what-are-the-odds/
published: true
tc-thumb-fld:
  - 'a:2:{s:9:"_thumb_id";s:3:"463";s:11:"_thumb_type";s:5:"thumb";}'
---
<em>[ Trigger warning: this post contains maths. Please don't be afraid, it probably won't bite. ]</em>

After posting this photo of our lottery ticket to Facebook[caption width="450" id="attachment_463" align="aligncenter"]<a href="http://jcarroll.com.au/wp-content/uploads/2015/03/soclose.jpg"><img src="http://jcarroll.com.au/wp-content/uploads/2015/03/soclose-300x166.jpg" alt="So close" width="300" height="166" class="size-medium wp-image-463"></a>So close[/caption]I thought more and more about random-event probabilities.

<!--more-->

I know my way around numbers just fine, so I know that the odds of winning Division 1 in the South Australian Saturday Night X-Lotto is 1 in <a href="https://tatts.com/salotteries/games/x-lotto" title="X-Lotto" target="_blank">8,145,060</a> (yes, that's one of the semi-useless numbers I have memorised).

[caption width="450" align="aligncenter"]<a href="http://www.dawgpoundnation.com/wp-content/uploads/2014/12/post-26236-Han-Solo-never-tell-me-the-odd-Xg7f.gif"><img src="http://www.dawgpoundnation.com/wp-content/uploads/2014/12/post-26236-Han-Solo-never-tell-me-the-odd-Xg7f.gif" width="750" height="318" alt="Sorry, Han." class=""></a>Sorry, Han.[/caption]
That's fairly improbable at face value, sure, but it's me, so I'm going deeper. Calculating odds of events with limited outcomes can be as easy as multiplying out individual probabilities. For example, the odds of 8 women in a mum's group all having the opposite-sex for their second child is just the product of 1 option from 2 choices, 8 times (multiplied);

\[ \left(\frac{1}{2}\right)^8 = \frac{1}{256}\ . \]

With things like drawing multiple numbered balls from a pool there are complications; it doesn't matter what order you take them out in, and you need to account for all the possible combinations. The odds are nonetheless fairly easy to calculate if you know/remember your combinatorics; If, from the initial pool of $$n$$ numbers, we need to choose $$r$$ without replacement, then the notation for this is "n choose r" and has the formula

\[ \displaystyle{{n \choose r} = \frac{n!}{r!(n-r)!}}\ , \]

where the exclamation mark denotes factorial ($$p! = p \times (p-1) \times (p-2) \times \ldots \times 1$$).

We are choosing 6 numbers from a pool of 45 without replacement, so the odds of any one exact choice coming up is

\[ \displaystyle{{45 \choose 6} = \frac{45!}{6!\ 39!}}\ . \]

We can make use of a little more math to simplify that;

\[ \frac{(a+b)!}{b!} = (a+b) \times (a+b-1) \times (a+b-2) \times \ldots \times (b+1)\ , \]

so we are left with

\[ \frac{45!}{6!\ 39!} = \frac{(6+39)!}{6!\ 39!} = \frac{45 \times 44 \times 43 \times 42 \times 41 \times 40}{6 \times 5 \times 4 \times 3 \times 2 \times 1} = \frac{5864443200}{720} = 8,145,060\ . \]

How about getting (any) 4 numbers? That's choosing 4 from a pool of 45;

\[ \displaystyle{{45 \choose 4} = 148,995}\ . \]

Games like Powerball have much worse odds; In that game Division 1 is won by selecting 6 numbers from a pool of 40 without replacement, but then also selecting the Powerball from a new pool of 20;

\[ \displaystyle{{40 \choose 6} \times {20 \choose 1} = 76,767,600}\ . \]

The point I was making with the photo was that it seemed somewhat cruel that the two missing numbers from our otherwise winning combination were both off by exactly 10, and thus only two little 1's stood between us and a decent $2 million. I know perfectly well that <em>any</em> two numbers qualified for those positions, but having the actual digits right there was just frustrating.

I know there are plenty of people who don't play the lottery because the odds are so bad. The problem I find with that thinking is two-fold; firstly, "<em>you gotta be in it to win it.</em>" A cliché, sure, but valid. If you don't have a ticket, your chances of winning are precisely zero. Secondly, while the odds of predicting the next random drawing of 6 numbers from a pool of 45 is 1 in 8,145,060, and thus the individual chances of winning are 'low', sure enough someone wins more or less every week. A scientific hero of mine, Richard Feynman puts it perfectly;
<blockquote>You know, the most amazing thing happened to me tonight. I was coming here, on the way to the lecture, and I came in through the parking lot. And you won't believe what happened. I saw a car with the license plate ARW 357. Can you imagine? Of all the millions of license plates in the state, what was the chance I would see that particular one tonight? Amazing!</blockquote>
The point is that every game (line on a ticket) has exactly the same chances of winning as any other. Sure, individually that's 'low' odds, but it's no lower for me than it is for you. Someone is quite likely going to be life-changingly wealthier each week, just as someone's car with some licence plate was going to be in the parking lot. It's easy to make the quote as above after the fact and state the odds of seeing that one, but that's applying an ex-post analysis to that particular event, confusing the matter somewhat.

There is of course some advantage in having more games available (buying more tickets), though it's no guarantee. You could buy 1,845,060 tickets and still not win; those calculated odds correspond to an infinite sample (you want an infinite sample simulator? <a href="http://gravy.azurewebsites.net/LotterySimulator/">Here you go</a>). If I buy a 20-game ticket then my chances of winning drop by a factor of 20 to 20/8,145,060, or 1 in 407,253. That's getting pretty reasonable; we're under the '1 in a million' line now.

Another way to think about this is that even 1 in 8 million isn't a terribly low probability in the grand scheme of things. Sure, things with that sort of probability aren't going to be showing up in your day-to-day life a lot, but there are interesting examples. There's apparently a <a href="http://theweek.com/articles/462449/odds-are-11-million-1-that-youll-die-plane-crash">1 in 11 million chance that you'll die in an plane accident</a>, which is hopefully reassuring. There's <a href="http://www.reddit.com/r/AskReddit/comments/2loor3/what_is_the_most_statistically_unlikely_thing/clxkdba" target="_blank">this family</a> who rented a car and travelled around the U.S.A., eventually parking next to another car with a consecutive number plate. The fact that it's the same model of car isn't terribly surprising; the plates were probably given in sequence to a dealer. The fact that the identifiable vehicles have been brought back together is the surprising part.

<a href="http://jcarroll.com.au/wp-content/uploads/2015/03/consecutive.jpg"><img src="http://jcarroll.com.au/wp-content/uploads/2015/03/consecutive-300x224.jpg" alt="That's weird" width="300" height="224" class="aligncenter size-medium wp-image-484"></a>

They claim the other was rented from a completely different state to where theirs was. I've seen a licence plate consecutive to ours on the road, but here in Adelaide that's probably not nearly so unlikely. I actually have a similar story; one Easter we went up the coast to Port Broughton, which was, to be honest, quite boring, so we got in the car and drove around to various towns, eventually stopping in for a snorkel at Moonta Bay. We pulled into the car park and I recognised the person getting out of their car in the bay across the road from ours. It was a visiting German post-doc from my research group who had decided to drive up from Adelaide on a whim, and who just happened to arrive at the same place as us at the same time and park a few meters from us. I digress.

What then, were the odds of getting those two 'off by 10' numbers on my game line? With 4 of the 6 numbers already correct, the pool was reduced by 4 numbers, and I needed to choose another 2, so the individual chances of any two remaining numbers being drawn were

\[ \displaystyle{{41 \choose 2} = 820}\ . \]

That applies whether we want the chances of specifically 13 and 16 being chosen or any other pair of numbers.

In large physics experiments such as the <a href="http://home.web.cern.ch/topics/large-hadron-collider">LHC</a>, statistics play a large role in determining when an event (e.g. observing a Nobel-prize winning particle) is 'likely' and when it isn't. Part of that includes taking into consideration the fact that <strong>lots</strong> of observations are made, making the distinction between rare events and random fluctuations a fine line, and so a 'look elsewhere effect' is included in the calculations. The analogy here is that I would have been just as upset with 23 and 26, or 33 and 36, so we should include those in our calculations of 'how likely'. This changes our calculations from the above, to choosing any of 6 numbers from the remaining 41, then any of 5 from the remaining 40;

\[ \frac{6}{41} \times \frac{5}{40} = \frac{30}{1640} = \frac{3}{164} \sim 1\ {\rm in}\ 55\ , \]

so I'd say not all that unlikely to happen.

This is why patterns show up so frequently from apparently random events; we focus on specific odds of unlikely events but fail to take in to account the other equally unlikely combinations. Bumping into a friend from a decade ago might seem unlikely, but you need to multiply those odds by the number of people who would have elicited the same response from you, had you bumped into them. In my earlier anecdote about bumping into a fellow researcher, I would have been just as surprised to see pretty much anyone I knew, so the probability of this 'event' is suddenly significantly higher, though possibly still 'low'. With the car example, this probably happens a lot and you don't notice it. I certainly don't read the licence plate of every vehicle I park near. Also, how close would the plates need to be to surprise you? Off by a digit? Just the last digit? A letter? The 'look elsewhere' effect really raises this one significantly.

Anyway, after all that, am I still going to buy a ticket sometime this month? Probably.
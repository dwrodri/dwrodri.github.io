# On the practicality of running an AI Gym over a network socket

A couple months ago I stumbled across 
[this paper](http://cs230.stanford.edu/files_winter_2018/projects/6940282.pdf) 
and thought it was pretty cool. "Deep Q-Learning looks cool, let's give it a 
go." I thought to myself. Then I remembered I don't have a colossal HPC cluster
 at my disposal to do things like [make a DoTA 2 AI that goes toe-to-toe with
the pros](https://blog.openai.com/openai-five/) and I got sad. "Well, maybe I 
can offload the simulation of the card game to that Raspberry Pi I have sitting 
around and do all the learning on my desktop. Thus, the idea of an AI Gym with 
 a socket interface was born. 

### That sounds like something OpenAI Gym already does by default. This isn't 
### new at all.

You're [right](https://stackoverflow.com/questions/40195740/how-to-run-openai-gym-render-over-a-server).
There is no such thing as originality, everything new is old, no one is special
 and art is a lie. Before we get ahead of ourselves, let's note that apparently
 in the age of smart thermostats, cloud-connected everything, and Docker 
witchcraft, OpenAI Gym instances _still run on locally on your machine_. In 
case you didn't know, it takes a **long**-ass time to send a packet over a 
network—in terms of CPU cycles, that is. 


_How_ long, you ask? If your CPU is ticking away at anywhere around 3GHz, and 
it's executing one instruction per tick, you'd be able to execute roughly 
**1.5 million** instructions before that packet could do a round trip around a
single data center. [Here are the numbers I used to do the 
math](https://people.eecs.berkeley.edu/~rcs/research/interactive_latency.html).
For something like blackjack, where each round of play isn't going to take more
than a couple thousand instructions, this meant I would need the hardware that 
would support several thousand threads of execution. Looks like were back at 
the DoTA-2-playing HPC mega-cluster. Well, it was worth a thought. 


That being said, since that calculation was essentially done on the back of a 
napkin, I could be very wrong. I've begun making [my own blackjack gym](https://github.com/dwrodri/blackjack_gym)
I've gotten hired to be a TA for a programming class at my university this 
semester, and I need to brush up on my C programming skills anyways.

---

If you'd like to send me a nice email with ideas of what to write about, feel 
free to do so with the email button above. If you feel a sudden urge to tell 
me that my writing was a waste of time and I should go die in a fire, that's 
fine as well, but constructive criticism would be appreciated. 

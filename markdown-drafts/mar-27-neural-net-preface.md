## Modern Neural Networks in C++ for a College Sophomore, Part One: The Preface

_Before I get started, I'd like to thank_ [_Grant Sanderson_](http://www.3blue1brown.com) _and_ [_Michael Neilsen_](http://michaelnielsen.org/) _for their work. They are the reason I was able to do any of this, so if you like what you see be sure to check them out._

_I'll be writing this over the course of several weeks. This installment focuses on the hands-off bits. If you're here to dive straight into code, skip the first two sections and go straight to part two._

### Introduction

Over the course of the past several months, I have been working on writing a neural network in C++. It is one of the simplest kinds, the [multi-layer perceptron](https://en.wikipedia.org/wiki/Multilayer_perceptron). I wrote this code to familiarize myself with neural nets, and I'd like to share it with others so they can do the same. This essay will dissect my code piece by piece, and convey the basics of a multi-layer perceptron along the way. According to my text editor, I've gotten my writing style down to an eighth grade level. That said, prepare yourself to learn quite a bit if  you're new to the world of deep learning. 

In my (brief) experience with NNs, it seems a lot more people care about conducting experiments with NNs than building them. I want to show how NNs can be as fascinating to software engineers as they are to data scientists. I started this project to become a better data scientist, but I ended up growing more as a software engineer. Over the course of development, I made a lot of design decisions which you wouldn't find in a typical class assignment. I want my code to highlight the importance of vector operations, but I don't want hide all the math in a CUDA kernel. I simplified my code for readability, but not so that it doesn't illustrate the complexity of designing modern NNs. 

You are in the right place if any of the following statements are true:

*   You're sick and tired of hearing the phrase "deep learning" and not knowing what it means.
*   You're a computer science student who has been searching for a NN tutorial that _doesn't_ use Python.
*   You've written some code in C++ before and won't melt at the sight of the STL.
*   You're not the best at calculus or linear algebra, but enjoy programming. 

### Outline:

1.  Rant for context
2.  Oh god, another MNIST tutorial?

### Rant for context

Research in neural networks has produced quite the razzle-dazzle over the course of the past twelve years or so. The emergence of the use of neural networks (abbreviated as NN hereon) has brought forth revolutions in several fields. NN research caught the world's attention when it [revolutionized the world of computer vision](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks). Since then, researchers have tried using NNs for everything from [generating photos of fake celebrities](https://www.youtube.com/watch?v=VrgYtFhVGmg) to [playing Go](https://www.youtube.com/watch?v=MgowR4pq3e8). Recently, there has been a notable increase in good educational resources that cover NNs. As happy as I am to know there are more learning resources out there, I have some bones to pick with the current educational landscape:

1.  Many learning resources like to drown you in dense formulas. Don't get me wrong, dense formulas are great at describing very complex relationships in a small amount of space on a sheet of paper. My problem with these formulas is that they are often too dense. They can be quite hard to decipher if you are not very familiar with calculus and linear algebra. I'd like to replace those formulas with animations. 
2.  I'm almost certain the most popular language for building NNs is [Python](https://github.com/search?utf8=%E2%9C%93&q=neural+network&type=). NNs built in Python often hide all the impressive feats of software engineering in a library. I want to show you those engineering bits and how I chose to write them.
3.  Everyone insists on starting with using a NN to classify handwritten digits in the MNIST dataset. I've dedicated an entire section to explaining the pros and cons of this approach.  

I should preface that my C++ experience is almost non-existent. Before this project, I was much more comfortable with Python, Java and C programming. I've done as much as I can to gravitate away from my C programming habits and let the advancements in modern C++ do their work. I plan to perform some extensive refactoring down the line, but to not let the perfect get in the way of the good I'm posting this now. If I can find the free time (read: motivation), I will translate this code to other languages as well. creating this neural network has been an amazing exercise for learning C++, and I've been meaning to learn Haskell and Golang. 

_TL;DR_: I wanted to learn a new programming language and there aren't many good tutorials on this stuff in C++, so I tried to make one. 

### Oh god, is this _another_ MNIST tutorial?

Every NN tutorial in the universe starts with the MNIST dataset. For the unitiated, the [MNIST dataset](http://yann.lecun.com/exdb/mnist/index.html) is a selection of uniquely compressed hand-drawn images of numbers. The dataset is provided and hosted by Dr. Yann LeCun, a notable figure in the deep learning industry. [Dr. LeCun was one of the first researchers to show the power of NNs in the field of optical character recognition (OCR)](http://www.ics.uci.edu/~welling/teaching/273ASpring09/lecun-89e.pdf). The dataset is labeled in its entirety, and also split into training and  test sets. At this point, I'd be surprised to find a data scientist who _hasn't_ touched the MNIST dataset. The dataset has acquired its fame not only by association with Dr. LeCun. It is also due to the fact that OCR is one of the most straightforward problems that illustrates the _necessity_ of something like a NN. People are entranced by the shiny reflective properties of a difficult and choose to look no further. But here's some food for thought—is a tutorial inherently _bad_ if it doesn't focus on why it's necessary 

My main reason for objecting to using MNIST as a first step is that it's not simple enough. It's pointless for a mere mortal to try picturing what a graph would look like in 784-dimensional space. 

Every tutorial that classifies MNIST isn't necessarily doomed for failure. In fact I credit [this video series](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) and [this website](http://neuralnetworksanddeeplearning.com/) for making this entire work a reality. All my code is a bastardized translation of Michael Neislen's original Python code, with the occasional tweak's here and there. My main issue with MNIST classifiers is that they are too complicated to dissect. There's a reason so many tutorials that use this dataset have the same feel. If I'm going to do this right, there will be no hand-waving in my explanations—no variable unexplained, no function undeciphered.
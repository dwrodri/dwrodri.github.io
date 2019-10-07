## R is a joy if you treat it like awk

During my undergrad I took a data science class. It was a great class where we
dove into topics such as EDA, lasso regression, SVMs, visualizations, and many
other good things that other people across the Internet love to blog about ad
nauseum. The one thing I had a terrible experience with was R. Let me clarify—R
is a fantastic envronment for statisticians to explore advanced computation
methods on cleaned data. It is also a great environment for developing great
insights on clean data using their DataFrame type. If you haven't caught the
hint yet, **R is only great if your data is already great**.

The sad reality of most exciting data science projects is that they more often
than not aren't based on a clean, well-studied dataset. Thank God Tensorflow
changed their default tutorial away from digit recognition, because MNIST has
quickly become the Wonderwall of computer vision. The reality is half of data
science is just cleaning data, and the other half is complaining about how much
of data science is just cleaning data. You can add another half's worth of time
for debugging your neural net, if you were coaxed into using one that isn't
off-the-shelf. 

In my experience, just about anything beats R when it comes to cleaning dirty 
data. You can literally go from zero awk experience to a clean CSV in less time
than it takes to write an R script that parses the same poorly-formatted
plaintext source. Python's scientific libraries have stolen R's DataFrame magic
and even allowed for it to scale to multi-node architectures. I used to resent
R, it was shoved upon me as a strange tool that promised to replace Python, but
failed miserably.

Then I finally came to an important realization. R is a Unix tool. That's all it
is. I started treating it like awk or sed and suddenly it's great. It blows my
mind that isn't R isn't shown in this context more often. If R is bad at
cleaning your data, you can just clean it in awk and then just pipe to R. I've
actualy reduced my R usage down to mostly just two aliases (written here in fish
syntax):

```
alias stats 'Rscript -e "summary(as.numeric(readLines(\"stdin\")))"'
alias boxplot 'Rscript -e "boxplot(as.numeric(readLines(\"stdin\")))"'
```

The first produces a quick numeric summary of a series of numbers on stdin. The
second produces a boxplot with that same data in PDF format. For example, let's
say I've just bought a new server and I want to see how long it takes to spin up
a webapp after a crash. I would write a script that simulates a crash, and then
logs the recovery time after each crash and saves it in a file called
output.log. If I wanted a boxplot of the total recovery times, all I would have
to do is:
```
grep "Recovery time:" output.log | awk '{print $2}' | boxplot
```

No spinning up Rstudio. No finnicking with ggplot settings. No more
oh-my-god-why-how-do-I-just-get-this-into-a-list. Have you tried doing advanced
text file in work in R? Yeah, no. Just results that help you
figure stuff out. Just do all the cleaning and OS stuff in awk or Python. 

Now R is great! I'd love it if people e-mail me some R snippets like the one I
shared here so I can add them to my running list.

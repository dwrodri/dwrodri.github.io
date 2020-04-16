# Pathfinding in RPD, Part 1: Linear Quadtrees with Level Differences
### by Derek Rodriguez

This is a blog post documenting an interesting data structure I implemented a
couple years ago, which I'm now using as the backbone for a path-finding library
which you will be able to incorporate into your own games.  The system I
implemented comes from this paper published a couple years ago by Dr. Aizawa and
Dr. Tanaka.  As far as I can tell, there is no open source library offering this
data structure, so I'm creating an implementation myself and sharing it with the
world. In the follow-up blogpost, I'll be showing how we can 

Let's say you're building an RPG, and you want to fill it with NPCs who are
capable of getting from point A to point B without hard-coding every path that
very NPC has to travel. To save yourself some time, you'd like to have access
to a `walkToPoint(Point destination)` function when programming the behavior for
a given NPC. If the space between the NPC and the goal is empty, then the
obvious choice is for the NPC to just walk in a straight line towards the goal.
But what if this is a long journey, and there are buildings placed right along
that straight line which the NPC can't go through? We'll have to build a path
around the obstacles to get to the goal. 

In order to build a path across the space, we can represent our space as an
undirected cyclical graph, and use a graph search algorithm to build the path
from A to B. Quadtrees are a very efficient way of representing a 2D space
where regions of that space clearly fall into two categories. For our example,
our game map would be classified into space where NPCs can walk, and space where
NPCs can't walk. 

To build our quadtree, we would take the entire space, and separate it into four
equally sized cells.  Each of those cells would have one of three values:

- FREE: The NPC will not collide with anything in this cell
- TAKEN: The NPC will collide with everything in this cell 
- MIXED: The NPC will collide with at least something in this cell

Now that the cells have been classified, we break each MIXED cell into four more
cells for the second time and assign _those_ cells their corresponding values.
We repeat this process of dividing up cells until there are no MIXED cells left,
only TAKEN and FREE. We can then quickly build paths from A to B through the 
centroids of each cell. The video below demonstrates this in action:


Each of these cells has an address. Since we produced these cells in fours, it
makes the most sense to use a base-4 counting system for addressing.  Base-4 is
also very easy to translate to binary because 4 is a power of 2. This addressing
scheme is convenient because it allows for us to query neighboring cells of any
given cell and check their contents in constant time.



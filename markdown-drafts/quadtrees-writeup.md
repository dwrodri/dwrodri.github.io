# Pathfinding in RPD, Part 1: Using quadtrees to represent space
### by Derek Rodriguez

This is a blog post documenting an interesting data structure I implemented a
couple years ago, which I'm now using as the backbone for a path-finding library
which you will be able to incorporate into your own games.  The system I
implemented comes from this paper published a couple years ago by Dr. Aizawa and
Dr. Tanaka.  As far as I can tell, there is no open source library offering this
data structure, so I'm creating an implementation myself and sharing it with the
world. 

Let's say you're building an RPG, and you want to fill it with NPCs who are
capable of getting from point A to point B without hard-coding every path that
every NPC has to travel. To save yourself some time, you'd like to have access
to a `walkToPoint(Point destination)` function when scripting the behavior for
a given NPC. If the space between the NPC and the goal is empty, then the
obvious choice is for the NPC to just walk in a straight line towards the goal.
But what if this is a long journey, and there are buildings placed right along
that straight line which the NPC can't go through? We'll have to biuld a path
around the obstacles to get to the goal. 

In order to build a path across the space, we'll use a __quadtree__ to represent
the space and we'll build a path through space using the A\* algorithm.
Quadtrees are a very efficient way of representing a 2D space where regions of
that space clearly fall into two categories. For our example, our game map would
be classified into space where NPCs can walk, and space where NPCs can't walk. 

To build our tree, we would take the entire space, and separate it into four
equally sized cells.  Each of those cells would have one of three values:

- WHITE: The NPC will not collide with anything in this cell
- BLACK: The NPC will collide with everything in this cell 
- GRAY: The NPC will collide with at least something in this cell

Now that the cells have been classified, we break each GRAY cell into cells for
the second time and assign _those_ cells their corresponding values. We repeat
this process of dividing up cells until there are no GRAY cells left, only BLACK
and WHITE. 

Each of these cells has an address. Since we produced these cells in fours, it
makes the most sense to use a base-4 counting system for addressing.  Base-4 is
also very easy to translate to binary because 4 is a power of 2. We 



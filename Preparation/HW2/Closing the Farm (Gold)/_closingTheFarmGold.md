---
markdown:
    path: "Closing the Farm (Gold).md"
export_on_save:
    markdown: true
---

# Closing the Farm (Gold)

## US Open 2016

### Gold

#### Problem 2

>**Note**: If you haven't already, I recommend reading my solution for the Silver Version of the Problem First to understand the naive approach to solving this problem.

For the Silver Version of the Problem, we took the naive approach of retesting the validity of retesting the connectivity after each and every removal. While this worked when the limit for $N$ was $3000$, with the new constraints of $200000$ in the gold problem, we have to be a bit creative.

The biggest bottleneck of the previous solution is testing to see if the graph is connected after each removal, which would lead to an $O(N^2)$ algorithm. However, this can be avoided if we, instead of decunstructing the graph, reconstruct it backwards.

We can add each barn back one by one from the end state and see if it is connected at that point. This way, we only need to check the connectivity of the current barn and the barns that were disconnected before.

Here is how it would be done:

1. Calculate an Adjecency List.
2. Store the order that the cows are removed. Choose the last cow to be removed as the root.
3. Iterate through each node, starting from the very last node to be added:
   1. Check if any of the node's neighbors have already been added. If so, unite it with that node.
   2. Check each node that is added but was not previously connected to the root to see if it is connected to the root. If it is, you can remove it from the list of nodes not included. This can be stored as a Set, Queue, or Deque. (I used a set, but all of the options work).
   3. For the current node, check if it connected to the root. If it is not, add it to the list of disconnected nodes.
   4. If any node remained disconnected, store the situation of that as "NO", otherwise keep it as "YES".
4. Print out (making sure to do it in the correct direction) the unity of the graph at the instance.

Here is my (C++) code:

@import "closingTheFarmGold.cpp"

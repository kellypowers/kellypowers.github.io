---
layout: post
title:      "Binary Search Trees"
date:       2020-09-04 17:55:59 +0000
permalink:  binary_search_trees
---


As I was studying for my Mock Technical interview, I spent a lot of time on a subject I knew next to nothing about: Binary Search Trees (BST).  As it turns out, this was not part of my mock technical interview, but I am still glad I took the time to learn it and code it out for myself.  

BSTs binary trees that can hold a lot of information.  While binary trees are a data structure, binary search trees are an abstract data type.  They have keys that have data stored to them, and the trees follow a certain order.  They are in the form of a tree, only an upside-down tree, with the root starting at the top.  And that is what the top node is called: a root.  In a Binary Search Tree, each node has at MOST two child nodes.  The root has can have two nodes, the left node has keys that are lower in value than the keys at the right node.  Each node that has children has to follow this rule, where the left side has lower value keys and the right side has higher value keys than the node.  So each node with children are their own sub-tree.  


       8
		   /\
	  2      21
		/\      /
	1	 5   13
	    /
		3
A Perfect BST is one where each node has two children nodes, and the lengths of the branches are the same on both sides.

A Balanced BST has the same length on both sides of the root node.

There is a lot of information out there on BSTs.  After studying some of the theory, rules, and basics, I followed a code along on youtube with @beiatrix https://www.youtube.com/watch?v=6JeuJRqKJrI in javascript:

First define a class Node:

```class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}```

Next, we will define our class BST which will have several different methods you can call on it.  
We have size, which will give the size of the tree.  
Insert, which increases the count, then creates a new Node class instance based on the value.  Inside the insert() function we have created a recursive function searchTree, which says if the value we are inserting is less than node.value, go left, if it is greater than node.value, go right.  If there is no left child after going left, append a new node, if there is a child after going left, recursively do it all over again by calling searchTree(node.left).  The same works for the right side of the tree, if the value is greater than node.value.  
BST.min()  returns the minimum value, which is found by going left at every node.
In the same reasoning, BST.max() returns the maximum value, which is found by going right at every node.
BST.contains() returns true if the value is in the tree and false if it is not.  It finds the value by going left for lower values and right for higher values at each node.

```
class BST {
    constructor(value) {
        this.root = new Node(value);
        this.count = 1;
    }

    size() {
        return this.count;
    }

    insert(){
        this.count++;

        let newNode = new Node(value);

        const searchTree = (node) => {
            if (value < node.value)  {
                if (!node.left)  {
                    node.left = newNode;
                } else {
                    searchTree(node.left);
                }
            }
            else if (value > node.value)  {
                if (!node.right)  {
                    node.right = newNode;
                } else {
                    searchTree(node.right);
                }

            }
            searchTree(this.root);
        }
    }

    min()  {
        let currentNode = this.root;
        while (currentNode.left)  {
            currentNode = currentNode.left;
        }
        return currentNode.value;
    }

    max() {
        let currentNode = this.root;
        while (currentNode.right)  {
            currentNode = currentNode.right;
        }
        return currentNode.value;
    }

    contains(value) {
        let currentNode = this.root;
        while (currentNode)  {
            if (value === currentNode.value)  {
                return true;
            }
            if (value < currentNode.value)  {
                currentNode = currentNode.left;
            } else {
                currentNode = currentNode.right;
            }
        }
        return false;
    }
		
    dfsInOrder() {
        let result = [];

        const traverse = node => {
            if (node.left) traverse(node.left);


            result.push(node.value);

            if (node.right) traverse(node.right);
        }
        traverse(this.root);
        return result;
    }

    dfsPreOrder()  {
        let result = [];

        const traverse = node => {
            result.push(node.value);
            if (node.left) traverse(node.left);

            if (node.right) traverse(node.right);
        }
        traverse(this.root);
        return result;

    }

    dfsPostOrder() {
        let result = [];

        const traverse = node => {
            if (node.left) traverse(node.left);
            if (node.right) traverse(node.right);
            result.push(node.value);
        }
        traverse(this.root);
        return result;

    }


    bfs() {
        let result = [];
        let queue = [];

        queue.push(this.root);
        while (queue.length)  {
            let currentNode = queue.shift();

            result.push(currentNode.value);

            if (currentNode.left) {
                queue.push(currentNode.left);
            }
            if (currentNode.right)  {
                queue.push(currentNode.right)
            }
        }

        return result;
    }
}```


Next, an important part of BSTs, are the search functions that go along with it.

Depth-First-Searches go branch-by-branch.  
In @beiatrix's example, her BST looks like this:
           15
					 / \
				3      36
			/  \      /   \
		2  12.  28. 39
		
		In an In-Order Depth First Search, the search starts at the left branch, then goes to the root, then goes to the right, so it will search the above tree in the following order:
		2, 3, 12, 15, 28, 36, 39
		As you can see, in-order DFS searches in order of the values of the nodes from lowest to highest.
		
		A Pre-Order BFS starts at the root, then Left, then Right, so the above tree will be searched in this order:
		15, 3, 2, 12, 36, 28, 39
		
		In a post-order DFS the search foes Left, Right, then Root, so the search of the above tree will go in this order:
		2, 12, 3, 28, 39, 36, 15
		
		
		A Breadth First Search is a beast of it's own, and I spent a lot of time logging and tring to figure out exactly how it works.  Rather than branch-by-branch, it searches level-by-level and uses a queue to hold values.  A BFS of the above tree will search in the following order:
		15, 3, 36, 2, 12, 28, 39
		
		
		These are all searches that are good to be familiar with, and I recommend doing some research and code alongs to better help understand the code, the structure and the common searches.  I definitely recommend beiatrix's channel https://www.youtube.com/channel/UC2P4AleInJhfr73UMgr7Atg and her code along of binary search trees. 

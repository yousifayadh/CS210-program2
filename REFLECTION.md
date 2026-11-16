# REFLECTION

1. For every function you wrote (TODO 1 to 19), explain in your own words what it does and
   give its time complexity in terms of n, the number of scenes. One short paragraph each.
   
TODO 1 constructs a single Scene.  TODO 1 is O(1) as it only runs to a specific number that stays the same (3). That isn't O(n) or even O(log n) as the number of choices isn't related to the number of scenes. That only leaves O(1) to be the answer. 

TODO 2 is the destructor. It is used to clean up anything allocated to memory using the new keyword. It runs to O(n) as calling delete choices_[i] causes the scenes that are children of the scene that is at choices_[i], which is eventually causes all of the scenes to be deleted.

TODO 3 is the boolean for if the scene is an ending scene. This is O(1) as it's a single condition and a couple of return statements.

TODO 4 returns the child scene that comes with selecting a specific choice. This is O(1) as it is a conditional and a couple of returns too.

TODO 5 puts the scene passed as an argument in the next open index (if the index isn't < 0 or bigger than or equal to the number of choices ). This is also O(1) as it's a conditional and return statements.

TODO 6 counts the number of scenes that start from the scene passed in the argument (when it is called). This, worst case, is O(n) since it will return 15, the total number of the scenes in my story.

TODO 7 counts the number of endings in the story from a specified scene (passed in as an argument). That's also O(n) as it would need to go through every scene to find all the endings.

TODO 8 returns the height of the tree starting from a specific scene (also passed in as argument). This, worst case, is O(n) as it would need to visit all of the scenes to find the longest path from the specified scene to a leaf.

TODO 9 clears all of the scenes in the tree. This is O(n) as well since it would need to visit every scene to delete each scene.

TODO 10 builds the tree. This is O(n) as it would need to visit all of the scenes in order to build the tree.

TODO 11 reads all of the scenes through recursion. This is O(n) as it needs to visit all of the scenes.

TODO 12 is where the player picks the specific choice they want. Because this has nothing to do with the number of scenes (n), this is technically O(1).

TODO 13 is the actual playing of the game. This is O(n) because, if the tree consisted of 1 child per parent, getting to the end would be going through all of the scenes. That isn't the usual tree, but it is the worst case.

TODO 14 prints the # of scenes, # of endings, and the longest playthrough (which is just basically the height). This is O(n) as, although printing is O(1), it calls methods that are O(n). That isn't greater than O(n) as the methods are called sequentially rather than being dependent on one another.

TODO 15 prints all of the endings. This is also O(n) because it needs to go through all of the scenes in order to find all the endings.

TODO 16 prints the endings found starting from a specific scene (which is passed in as an argument). This is O(n) if the root is passed.

TODO 17 gives the choices, loot, and the result, for the greedy run (going for the choices with the most loot from a scene). This is also O(n) if the path is a straight line since it would go through all of the scenes.

TODO 18 is the path that gives the most loot. This is done recursively, and is O(n) because it would need to look at all of the scenes to find the best path for getting the most loot.

TODO 19 is the path that's most optimal (gives most loot but also survives). Because it calls bestLoot, this is O(n) as well.
2. Why does each scene allocate exactly numChoices slots instead of declaring Scene<T>*
   choices[3]? What does an ending hold in choices_, and why?

Each scene allocates exactly numChoices as always declaring choices[3] would often cause a waste of memory as, in my story for example, a scene usually has less than 3 choices, so allocating 3 every time would waste a lot of space. Only one scene (the first one) has 3 choices. In an ending, choices_ holds nullptr as choices_ is a pointer to an array of pointers. 
3. Walk through your Scene destructor. What gets deleted, and in what order? What would
   go wrong if choices_ were deleted first?

It first deletes whatever the pointers in the array point to (that's the loop part). Then it deletes the array, then it deletes the T type object that data_ points to. If choices_ is deleted first, there would be memory leak due to the objects inside the array being inaccessible.
4. Show the path greedy took and the path optimal took on your story, with the loot for each.
   Explain why greedy lost. If greedy did not lose, change your story until it does, and explain
   what you changed.

Originally, The path greedy took was 2 - 1, which is going to watch the Hulk movie (loot = 40) and running towards Hulk (loot is still 40). Optimal took 3-2-2-1-2-1-1 which is watching spider-man, then pressing the button (webshooter) (loot = 40), then listening to the sensation (spidey-sense) (loot = 60), then winning the fight (loot = 110), then paying for the soda (loot = 110), then protecting the cashier (loot = 140), then eating the soda and chips (loot = 240). Greedy lost because, from the first scene, moving to the Hulk movie gave 10 while the other two scenes gave no loot. However, going for the Hulk would basically lead to sudden death. That was after I fixed my story as before, I had the loot messed up. To fix it, I changed it so the Hulk option gave more loot than the other 2 options.
5. bestLoot tries every path, yet it runs in O(n) time. Explain why it is not exponential, using
   what you know about paths and leaves in a tree.

Based on the idea that n is the number of scenes, then bestLoot would look at every scene once(and not more) because a leaf has no children and each child has a unique parent. There isn't any mixing where multiple choices can lead to the same ending. Each child has a unique parent. That would make each path not cross into each other, meaning no scene is checked more than once.
6. Which List methods does your game use, and why? What does one search cost as the bag
   grows?

It uses search, addFront, size, print, and the destructor of List. It uses search to look for the items in the bag, addFront to add the item to the "bag", size when printing how many items are in the bag, print to print what's in the bag, and the destructor to prevent memory leak. Each search costs O(n).  
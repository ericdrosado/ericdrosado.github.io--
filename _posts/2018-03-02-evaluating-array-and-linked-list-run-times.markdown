<h2> Intro </h2> 
As I continue to learn about Big O notation, I wanted to explore run times as it applies to linked lists and arrays. With that we have to explore the differences when it comes to how an array works in comparison to a linked list. We also should have a sense of how memory applies to these data structures. 

<h2> Memory </h2> 
When we think about memory we can visualize a locker room. Each locker is a place for storage, but lets say that each locker can hold one item. Now, if you have "locker experience," you have probably noticed that each locker is numbered to allow patrons the ability to find their locker. So, each locker has a place, in the locker room. 

Now, lets say we want to store something in our "locker memory." You ask memory if you have available space to store an item and if there is space, that item will be stored. Well, locker 420 has space so you have the ability to place that item in memory. Now, this is an incredibly simplistic view on memory. There are many other things at play, but let's use this simple example to discuss how arrays and linked lists interact with memory. 
 
<h2> Arrays </h2> 
As you may already know, arrays are data structures of a fixed amount of items. When you declare an array you declare the amount of items that will be in the array. This is by design as arrays store data contiguously, which means the data is stored next to each other. This makes it easy access data quickly, but you can run into certain issues down the line. 

Revisiting our locker room example, lets say you and your buddies enter the locker room and you want to make sure you all have a locker right next to each other. You find an area where there are enough lockers for each of you, but lets say you run into another friend in the locker room that wants to join you and the lockers around the lockers that you have already chosen are already taken. At this point everyone takes everything out of their lockers looking for enough lockers for all of you. Arrays work the same way, if you want to add a new item you will need to remove every item from their current place in memory and find a new place in memory to accomodate the new size of your array. You may think this is not a big deal, but if you wanted to increase an array in size you will have to traverse through the array every time and remove the items that are in it and put it into a new array, which can affect performance.  

<h2> Linked Lists </h2>
In contrast to arrays, linked lists only concern themselves with finding an available space in memory. In this case, looking at our last example, if you are in the locker room with your friends you all find an empty locker without concerning yourself with the idea with being right next to each other. 

In a linked list each item in memory points to the next item on the list. You'll realize that this is incredibly conveient. I should also note that you do not need to declare the size of a linked list like an array. You can continue to add items to a linked list without concerning yourself with moving items in memory. But, with ever benefit comes a tradeoff. 

<h2> Performance </h2>
When it comes to accessing information in these data structures you can probably deduce, which might be easier. Let's think of our locker example. If you and your buddies use the linked list model, how would you find one of your buddies in the locker room if you are not next to each other. Well, you would have to rely on your friends to know where the next person is in the locker room since in a linked list each item points to the next item. So you have to go through the linked list until you find what you are looking for. In contrast, the array allows you to find an item quickly because each item is right next to each other in memory. So when it comes to reading data, it is much faster in an array, O(1), versus a linked list of O(n).

What about inserting data? Well, we know that in a linked list it is very easy to add data since the items do not need to be next to each other. In this case a linked list would have O(1) time and an array would have O(n) time since you would have to move the data to a new spot in memory and it is dependent on how many items you have in the array.

<h2> Conclusion </h2>
With anything you use there will always be tradeoffs. For smaller projects it might not matter that you consider these things, but on larger projects it could play a huge role in how you design your project. I feel it is always best to be cognizant of these things when you are working on a project. 

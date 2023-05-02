#Recursion




## Tail recursive function
If you’re a programmer, you’re likely familiar with recursion and recursive functions. But do you know about Tail Recursion?

If you aren’t aware, a recursive function is a function that calls itself. While it can be complicated to understand, it often leads to simple and readable code (checkout screenshots below).

However, recursive functions are inefficient. Recursive functions depend on the result of each successive function call. Meaning that it has to wait for each recursive call to finish before returning a result.

This requires keeping track of each function on the Call Stack which is stored in memory. Each recursive call adds another layer to the stack, taking up more and more space.

Take up too much space and you get a Stack Overflow.

Tail recursive functions avoid this wasted space by maintaining the state/result as an extra parameter. Each recursive call updates the state, avoiding a dependency on the Call Stack.

Many programming languages are able to recognize tail-recursion and optimize for it. Avoiding the dreaded Stack Overflow.

Check out the images below for more information (and before anyone says it, yes I know one of my code snippets has a small bug :P)


Sun-Li Beatteay at LinkedIn
 

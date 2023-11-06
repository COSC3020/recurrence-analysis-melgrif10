[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12561883&assignment_repo_type=AssignmentRepo)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

In order to find a tight $O$ bound for this program we must evaluate the recurrence relation. This program has three loops which represent the work done outside of the recursion. The mystery function has 3 recursive calls and divides n by 3 at each call. It is also known that if n<=1 nothing needs to be done and we can just stop and return. To find the runtime of this program lets first analyze the complexity of the loops. 

The first loop runs from 0 to $n*n$ and therefore takes $O(n^2)$ iterations. The second loop runs from 0 to n and therefore takes $O(n)$ iterations. Finally the third loop runs from 0 to $n*n$ just like in loop one. Simarlily it takes $O(n^2)$ iterations. Combining this information we can now calculate the time complexity outside of the recursion: $O(n^2*n*n^2) = O(n^5)$ 

For the recursion complexity it is known that there are 3 calls and at each call n is divided by 3. However, if n<=1 then no additional analysis is needed. This can be formatted like: 
$T(n)=\begin{cases}
        1 \quad &\text{if } n\leq 1\\
        3T(\frac{n}{3}) \quad &\text{if } n>1 \end{cases}$

If we add the complexity from outside the recursion the recurrence relation looks like this: 
$T(n)=\begin{cases}
        1 \quad &\text{if } n\leq 1\\
        3T(\frac{n}{3})+n^5 \quad &\text{if } n>1 \end{cases}$

Now that everything is formatted we can use the master theorem to solve this recurrance relation. The master theorem has the form of $T(n)=aT(n/b)+f(n)$, which is the form that our recurrence relation is already in. The master theorem states that we can compare f(n) (The time complexity from outside the recursion calls) to $n^{log_b(a)}$. 

$n^{log_b(a)}=n^{log_3(3)}=n$ vs $n^5$ 

This comparison shows how $n^5 > n$, which means that the complexity from outside the recursion is growing at a faster rate and therefore $T(n)=f(n)$. 

In summary, the time complexity for this program is $T(n)=O(n^5)$. 




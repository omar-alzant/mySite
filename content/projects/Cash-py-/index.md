---
title: "Cash"
date: 2022-06-08
draft: false
blog_tags: ["python"]
status: "python"
weight: 1
summary: "Implement a program that calculates the minimum number of coins required to give a user change.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://cs50.harvard.edu/x/2022/psets/6/cash/"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant"
        weight: 2
---


</br>

Code:

```python
from cs50 import get_float, get_int

while True:
    nbr = get_float("Change owed: ")
    if nbr >= 0:
        break
        
cent = int((nbr*100)+0.5)
total = 0

for coin in [25, 10, 5, 1]:
    total += cent // coin  #total = total + cent /int(coin)
    cent %= coin           #cent = cent % coin  
    
print(total)
```

</br>
</br>


In the final, To test this code:

```markdown
$ python cash.py
Change owed: 0.41
4
```

<img src="./featured.png" loading="lazy" style="max-width: 600px;" />

</br>
</br>

## Specification:

1- Write, in a file called cash.py, a program that first asks the user how much change is owed and then spits out the minimum number of coins with which said change can be made.You should assume that the user will input their change in dollars (e.g., 0.50 dollars instead of 50 cents).

2- Use get_float from the CS50 Library to get the user’s input and print to output your answer. Assume that the only coins available are quarters (25¢), dimes (10¢), nickels (5¢), and pennies (1¢).

- We ask that you use get_float so that you can handle dollars and cents, albeit sans dollar sign. In other words, if some customer is owed $9.75 (as in the case where a newspaper costs 25¢ but the customer pays with a $10 bill), assume that your program’s input will be 9.75 and not $9.75 or 975. However, if some customer is owed $9 exactly, assume that your program’s input will be 9.00 or just 9 but, again, not $9 or 900. Of course, by nature of floating-point values, your program will likely work with inputs like 9.0 and 9.000 as well; you need not worry about checking whether the user’s input is “formatted” like money should be.

3- If the user fails to provide a non-negative value, your program should re-prompt the user for a valid amount again and again until the user complies.

4- Incidentally, so that we can automate some tests of your code, we ask that your program’s last line of output be only the minimum number of coins possible: an integer followed by a newline.


***

</br>
</br>

<strong>
     You’re encouraged to first test your code on your own for each of the following.
</strong>


1- Run your program as python cash.py, and wait for a prompt for input. Type in 0.41 and press enter. Your program should output 4.

2- Run your program as python cash.py, and wait for a prompt for input. Type in 0.01 and press enter. Your program should output 1.

3- Run your program as python cash.py, and wait for a prompt for input. Type in 0.15 and press enter. Your program should output 2.

4- Run your program as python cash.py, and wait for a prompt for input. Type in 1.60 and press enter. Your program should output 7.

5- Run your program as python cash.py, and wait for a prompt for input. Type in 23 and press enter. Your program should output 92.

6- Run your program as python cash.py, and wait for a prompt for input. Type in 4.2 and press enter. Your program should output 18.

7- Run your program as python cash.py, and wait for a prompt for input. Type in -1 and press enter. Your program should reject this input as invalid, as by re-prompting the user to type in another number.

8- Run your program as python cash.py, and wait for a prompt for input. Type in foo and press enter. Your program should reject this input as invalid, as by re-prompting the user to type in another number.

9- Run your program as python cash.py, and wait for a prompt for input. Do not type anything, and press enter. Your program should reject this input as invalid, as by re-prompting the user to type in another number.

***

</br>
</br>



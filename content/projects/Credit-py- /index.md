---
title: "Credit"
date: 2022-06-08
draft: false
garden_tags: ["python"]
status: "python"
weight: 2
summary: "Implement a program that determines whether a provided credit card number is valid according to Luhn’s algorithm.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://cs50.harvard.edu/x/2022/psets/6/credit/"
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
from cs50 import get_int

nbr = get_int("Number :  ")
nbrs = str(nbr)

l = len(nbrs)

if nbrs[0] == '3' and (nbrs[1] == '7' or '4') and l == 15:
    print("AMEX")
elif nbrs[0] == '5' and (nbrs[1] == '1' or '2' or '3' or '4' or '5') and l == 16:
    print("MASTERCARD")
else:
    if nbrs[0] == '4' and l == 13 or l == 16:
        print("VISA")
    else:
        print("INVALID")
```

</br>
</br>


In the final, To test this code:

```markdown
$ python credit.py
Number: 378282246310005
AMEX
```


<!-- <img src="./featured.png" style="max-width: 600px;" /> -->

</br>
</br>
***
<strong>
     You’re encouraged to first test your code on your own for each of the following.
</strong>

1-Run your program as python credit.py, and wait for a prompt for input. Type in 378282246310005 and press enter. Your program should output AMEX.

2-Run your program as python credit.py, and wait for a prompt for input. Type in 371449635398431 and press enter. Your program should output AMEX.

3-Run your program as python credit.py, and wait for a prompt for input. Type in 5555555555554444 and press enter. Your program should output MASTERCARD.

4-Run your program as python credit.py, and wait for a prompt for input. Type in 5105105105105100 and press enter. Your program should output MASTERCARD.

5-Run your program as python credit.py, and wait for a prompt for input. Type in 4111111111111111 and press enter. Your program should output VISA.

6-Run your program as python credit.py, and wait for a prompt for input. Type in 4012888888881881 and press enter. Your program should output VISA.

7-Run your program as python credit.py, and wait for a prompt for input. Type in 1234567890 and press enter. Your program should output INVALID.
***
</br>
</br>



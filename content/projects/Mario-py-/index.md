---
title: "Mario Pyramid"
date: 2022-06-08
draft: false
project_tags: ["python"]
status: "python"
weight: 5
summary: "Implement a program that prints out a double half-pyramid of a specified height, per the below.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://cs50.harvard.edu/x/2022/psets/6/mario/more/"
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


def get_post_int():

    while True:
        nbr = get_int("Height: ")
        if nbr > 0 and nbr < 9:
            break
    return nbr


nbr = get_post_int()

for i in range(1, nbr+1):
    print(' ' * (nbr - i) + '#' * i + ' ' * 2 + '#' * i)
```

</br>
</br>


In the final, To test this code:

```markdown
$ ./mario
Height: 4
   #  #
  ##  ##
 ###  ###
####  ####
```

</br>
</br>


<img src="./featured.png" style="max-width: 600px;" />

</br>
</br>



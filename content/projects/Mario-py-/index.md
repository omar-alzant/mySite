---
title: "Mario Pyramid"
date: 2022-06-08
draft: false
blog_tags: ["python","cpp"]
status: "python cpp"
weight: 6
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

Code -Py- :

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

***

Code -C- :

```c
#include <stdio.h>
#include <cs50.h>

int main(void)
{

    int n;
//do
    do
    {
        n = get_int("enter  the heigth of pyram : ");
        for (int i = 1 ; i <= n ; i++)
        {
            for (int j = 1 ; j <= n - i ; j++)
            {
                printf(" ");
            }
            for (int k = n - i ; k < n  ; k++)
            {
                printf("#");
            }
                printf(" ");
                printf(" ");
        for (int k = n - i ; k < n  ; k++)
            {
                printf("#");
            }
            printf("\n");
        }
    }
    while (n < 1 || n > 8);
}

```

***

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



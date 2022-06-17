---
title: "Readability"
date: 2022-06-08
draft: false
garden_tags: ["python","cpp"]
status: "python cpp"
weight: 8
summary: "Implement a program that computes the approximate grade level needed to comprehend some text, per the below."
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://cs50.harvard.edu/x/2022/psets/6/readability/"
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
from cs50 import get_string


text = get_string("enter the phrase to verify your grade : ")

let = sent = wor = 0

for char in text:
    if char.isspace():
        wor += 1
    if char.isalpha():
        let += 1
    if char in ['!', '?', '.']:
        sent += 1
wor += 1

L = (let * 100) / wor
S = (sent * 100) / wor
res = int((0.0588 * L - 0.296 * S - 15.8) + 0.5)
if res < 1:
    print("Before Grade 1")
elif res >= 16:
    print("Grade 16+")
else:
    print(f"Grade: {res}")   
```
***


Code -C- :

```c
#include <stdio.h>
#include <cs50.h>
#include <ctype.h>
#include <string.h>
#include <math.h>

// index = 0.0588 * L - 0.296 * S - 15.8
// L :  the average number of letters per 100 words in the text
// S : the average number of sentences per 100 words in the text
// grade < 1 : before grade 1
// grade > 16 : grade 16+

// #include <ctype.h>
// isalpha - check whether a character is alphabetical
//  isdigit - check whether a character is a digit
// islower - check whether a character is lowercase
//  isspace - check whether a character is whitespace
// isupper - check whether a character is uppercase
// strlen - calculate the length of a string

int letter(string s);
int world(string s);
int sentence(string s);




int main(void)
{
    string s = get_string("enter the phrase to verify your grade : ");

    int W = world(s);
    int L = letter(s)  ;
    int S = sentence(s) ;

    float index =  0.0588 * L * 100 / W - 0.296 * S * 100 / W - 15.8;

    int grade = (int)round(index) ;

    if (grade < 1)
    {
        printf("Before Grade 1\n");

    }
    else
    {

        if (grade > 16)
        {
            printf("Grade 16+\n");
        }
        else
        {
            if (grade > 1 | grade < 16)
            {
                printf("Grade %i\n", grade);
            }
        }
    }

//printf("let : %i , sent: %i , wor : %i", L,S,W);
}


// nbr of world

int world(string s)
{
    int count = 1;

    for (int i = 0, n = strlen(s); i < n ; i++)
    {
        if (isspace(s[i]))
        {
            count ++;
        }
    }
    return count;
}


// nbr of letter

int letter(string s)
{
    int count = 0  ;
    for (int i = 0, n = strlen(s); i < n ; i++)
    {
        if (s[i] == '.')
        {
            continue;
        }
        if (islower(s[i]) || isupper(s[i]))
        {
            count ++;
        }
    }

    return count ;

}

// nbr of sentence

int sentence(string s)
{
    int count = 0  ;

    for (int i = 0, n = strlen(s); i < n ; i++)
    {
        if (s[i] == '!' || s[i] == '?' || s[i] == '.')
        {
            count ++ ;
        }
    }
    return count ;
}

```

</br>
</br>


In the final, To test this code:

```markdown

$ python readability.py
Text: Congratulations! Today is your day. You're off to Great Places! You're off and away!
Grade 3

```
</br>

<img src="./featured.png" style="max-width: 600px;" />

</br>
</br>


*** 

## Specification : 

1- Write, in a file called readability.py, a program that first asks the user to type in some text, and then outputs the grade level for the text, according to the Coleman-Liau formula.
- Recall that the Coleman-Liau index is computed as 0.0588 * L - 0.296 * S - 15.8, where L is the average number of letters per 100 words in the text, and S is the average number of sentences per 100 words in the text.



2- Use get_string from the CS50 Library to get the user’s input, and print to output your answer.

3- Your program should count the number of letters, words, and sentences in the text. You may assume that a letter is any lowercase character from `a` to `z` or any uppercase character from `A` to `Z`, any sequence of characters separated by spaces should count as a word, and that any occurrence of a period, exclamation point, or question mark indicates the end of a sentence.

4- Your program should print as output `"Grade X"` where `X` is the grade level computed by the Coleman-Liau formula, rounded to the nearest integer.

5- If the resulting index number is 16 or higher (equivalent to or greater than a senior undergraduate reading level), your program should output `"Grade 16+"` instead of giving the exact index number. If the index number is less than 1, your program should output `"Before Grade 1"`.



</br>


*** 
<strong> 
You’re encouraged to first test your code on your own for each of the following.
</strong>



1- Run your program as python readability.py, and wait for a prompt for input. Type in One fish. Two fish. Red fish. Blue fish. and press enter. Your program should output Before Grade 1.

2- Run your program as python readability.py, and wait for a prompt for input. Type in Would you like them here or there? I would not like them here or there. I would not like them anywhere. and press enter. Your program should output Grade 2.

3- Run your program as python readability.py, and wait for a prompt for input. Type in Congratulations! Today is your day. You're off to Great Places! You're off and away! and press enter. Your program should output Grade 3.

4- Run your program as python readability.py, and wait for a prompt for input. Type in Harry Potter was a highly unusual boy in many ways. For one thing, he hated the summer holidays more than any other time of year. For another, he really wanted to do his homework, but was forced to do it in secret, in the dead of the night. And he also happened to be a wizard. and press enter. Your program should output Grade 5.

5- Run your program as python readability.py, and wait for a prompt for input. Type in In my younger and more vulnerable years my father gave me some advice that I've been turning over in my mind ever since. and press enter. Your program should output Grade 7.

6- Run your program as python readability.py, and wait for a prompt for input. Type in Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, "and what is the use of a book," thought Alice "without pictures or conversation?" and press enter. Your program should output Grade 8.

7- Run your program as python readability.py, and wait for a prompt for input. Type in When he was nearly thirteen, my brother Jem got his arm badly broken at the elbow. When it healed, and Jem's fears of never being able to play football were assuaged, he was seldom self-conscious about his injury. His left arm was somewhat shorter than his right; when he stood or walked, the back of his hand was at right angles to his body, his thumb parallel to his thigh. and press enter. Your program should output Grade 8.

8- Run your program as python readability.py, and wait for a prompt for input. Type in There are more things in Heaven and Earth, Horatio, than are dreamt of in your philosophy. and press enter. Your program should output Grade 9.

9- Run your program as python readability.py, and wait for a prompt for input. Type in It was a bright cold day in April, and the clocks were striking thirteen. Winston Smith, his chin nuzzled into his breast in an effort to escape the vile wind, slipped quickly through the glass doors of Victory Mansions, though not quickly enough to prevent a swirl of gritty dust from entering along with him. and press enter. Your program should output Grade 10.

10- Run your program as python readability.py, and wait for a prompt for input. Type in A large class of computational problems involve the determination of properties of graphs, digraphs, integers, arrays of integers, finite families of finite sets, boolean formulas and elements of other countable domains. and press enter. Your program should output Grade 16+.


</br>
</br>

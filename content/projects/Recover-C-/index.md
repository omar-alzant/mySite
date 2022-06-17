---
title: "Recover"
date: 2022-06-08
draft: false
blog_tags: ["cpp"]
status: "cpp"
weight: 9
summary: "Implement a program that recovers JPEGs from a forensic image.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://cs50.harvard.edu/x/2022/psets/4/recover/"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant"
        weight: 2
---


</br>
</br>

<strong>
    All files included in 
    <a href="https://github.com/omar-alzant/files-for-mySite/tree/main" >this</a>
     github page.
</strong>


</br>
</br>

***

Code -C- :

```c
#include <stdint.h>
#include <stdio.h>
#include <stdbool.h>
#define Buffer_size 512

typedef uint8_t BYTE;

int main(int argc, char *argv[])
{

    FILE *f = fopen(argv[1], "r");
    if (f == NULL)
    {
        printf("error occured openiing the row file \n");
    }
    BYTE buffer[Buffer_size];
    size_t bytes_read;
    bool is_first_jpeg = false;
    FILE *current_file;
    char filename[100];
    int current_filenbr = 0;
    bool found_jpeg = false;

    if (argc  != 2)
    {
        printf("Usage: ./recover image");
        return 1;
    }
    /*
     // PseudoCode : //

    Repeat until end of card :     
       
             ...
    Close any remaining file
    */

//    open memory card

    while (true)
    {
//        Read 512 Bytes into a buffer

        bytes_read = fread(buffer, sizeof(BYTE), Buffer_size, f);
        
             
        if (bytes_read == 0)
        {
            break; // ennd of file
        }
//        If start of new JPEG

        if (buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff && (buffer[3] & 0xf0) == 0xe0)
        {      
            found_jpeg = true;
        
            if (!is_first_jpeg)
            {
                is_first_jpeg = true;
            }
            else 
            {
                // close the current file being written to, open new file 
                fclose(current_file); // previose file 000.jpg
            }
            sprintf(filename, "%03i.jpg", current_filenbr); // 000.jpg
            current_file =   fopen(filename, "w");
            fwrite(buffer, sizeof(BYTE), Buffer_size, current_file);
            current_filenbr ++; // filenbr = 1...        
        }
        else
        {
            if (found_jpeg)
            {
                fwrite(buffer, sizeof(BYTE), Buffer_size, current_file);
            }
        }
    }
    fclose(f); // close my raw file 
    fclose(current_file);
    return 0 ;
}
```
</br>

***

The result : 

<img src="./result.png" alt="result-icon">

***

## Background :

In anticipation of this problem, we spent the past several days taking photos of people we know, all of which were saved on a digital camera as JPEGs on a memory card. (Okay, it’s possible we actually spent the past several days on Facebook instead.) Unfortunately, we somehow deleted them all! Thankfully, in the computer world, “deleted” tends not to mean “deleted” so much as “forgotten.” Even though the camera insists that the card is now blank, we’re pretty sure that’s not quite true. Indeed, we’re hoping (er, expecting!) you can write a program that recovers the photos for us!

Even though JPEGs are more complicated than BMPs, JPEGs have “signatures,” patterns of bytes that can distinguish them from other file formats. Specifically, the first three bytes of JPEGs are

`0xff 0xd8 0xff`

from first byte to third byte, left to right. The fourth byte, meanwhile, is either `0xe0`, `0xe1`, `0xe2`, `0xe3`, `0xe4`, `0xe5`, `0xe6`, `0xe7`, `0xe8`, `0xe9`, `0xea`, `0xeb`, `0xec`, `0xed`, `0xee`, or `0xef`. Put another way, the fourth byte’s first four bits are `1110`.

Odds are, if you find this pattern of four bytes on media known to store photos (e.g., my memory card), they demarcate the start of a JPEG. To be fair, you might encounter these patterns on some disk purely by chance, so data recovery isn’t an exact science.

Fortunately, digital cameras tend to store photographs contiguously on memory cards, whereby each photo is stored immediately after the previously taken photo. Accordingly, the start of a JPEG usually demarks the end of another. However, digital cameras often initialize cards with a FAT file system whose “block size” is 512 bytes (B). The implication is that these cameras only write to those cards in units of 512 B. A photo that’s 1 MB (i.e., 1,048,576 B) thus takes up 1048576 ÷ 512 = 2048 “blocks” on a memory card. But so does a photo that’s, say, one byte smaller (i.e., 1,048,575 B)! The wasted space on disk is called “slack space.” Forensic investigators often look at slack space for remnants of suspicious data.


The implication of all these details is that you, the investigator, can probably write a program that iterates over a copy of my memory card, looking for JPEGs’ signatures. Each time you find a signature, you can open a new file for writing and start filling that file with bytes from my memory card, closing that file only once you encounter another signature. Moreover, rather than read my memory card’s bytes one at a time, you can read 512 of them at a time into a buffer for efficiency’s sake. Thanks to FAT, you can trust that JPEGs’ signatures will be “block-aligned.” That is, you need only look for those signatures in a block’s first four bytes.

Realize, of course, that JPEGs can span contiguous blocks. Otherwise, no JPEG could be larger than 512 B. But the last byte of a JPEG might not fall at the very end of a block. Recall the possibility of slack space. But not to worry. Because this memory card was brand-new when I started snapping photos, odds are it’d been “zeroed” (i.e., filled with 0s) by the manufacturer, in which case any slack space will be filled with 0s. It’s okay if those trailing 0s end up in the JPEGs you recover; they should still be viewable.

Now, I only have one memory card, but there are a lot of you! And so I’ve gone ahead and created a “forensic image” of the card, storing its contents, byte after byte, in a file called card.raw. So that you don’t waste time iterating over millions of 0s unnecessarily, I’ve only imaged the first few megabytes of the memory card. But you should ultimately find that the image contains 50 JPEGs.


***

</br>
</br>

## Specification : 

Implement a program called recover that recovers JPEGs from a forensic image.

1- Implement your program in a file called recover.c in a directory called recover.

2- Your program should accept exactly one command-line argument, the name of a forensic image from which to recover JPEGs.

3- If your program is not executed with exactly one command-line argument, it should remind the user of correct usage, and main should return 1.

4- If the forensic image cannot be opened for reading, your program should inform the user as much, and main should return 1.

5- The files you generate should each be named ###.jpg, where ### is a three-digit decimal number, starting with 000 for the first image and counting up.

6- Your program, if it uses malloc, must not leak any memory.


***

</br>
</br>

{{<youtube ooL0r_8N9ms>}}

***

</br>
</br>

## Usage :

Your program should behave per the examples below.

```markdown
$ ./recover
Usage: ./recover IMAGE

```

where IMAGE is the name of the forensic image. For example:

```markdown
$ ./recover card.raw
```

***

</br>
</br>

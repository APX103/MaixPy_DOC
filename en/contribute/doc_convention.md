Document specification
=======

Documents are built using gitbook and written in simple and efficient Markdown

The documentation source is hosted on [github](https://github.com/sipeed/MaixPy_DOC)

## Markdown syntax

If you never touched the basic syntax of Markdown, please take half an hour to learn, recommend the github tutorial: [github Markdown tutorial](https://guides.github.com/features/mastering-markdown/)

In this article, we need to pay attention to the following points:

### The syntax tags of the title class must be separated by spaces. A blank line is required between the headline and the body, such as:

```markdown
## This is a secondary title

* This is list item 1
* This is list item 2

```
And the following is not correct, it may cause the parser to parse the error format, etc.

```markdown
##This is a secondary title
*This is list item 1
*This is list item 2
```

### All pages have only one top level title

Because the need to automatically generate a directory, mainly to ensure that the automatically generated directory is correct.
Write each page like this
```
Page title/top level title
=======                          (There is at least three equals here)
                                 (At least one more blank line is required, 2 lines are recommended)

## Secondary title 1             (You cannot use a first-level title here, and you cannot use a ##. You don't need to write a serial number, it will automatically generate a serial number.)
                                 ( Skip a line )
text
                                 (at least one line)
### Three-level title            (similar to the second-level title, it does not need to be written, it will be generated automatically)

text

## Secondary title 2

text


```


### Link

Due to the large number of pages and the need to link resources such as images, relative paths are used when writing links.
Such as the directory structure is as follows
```
Assets/                                     (put public resource files)
       |
       ----pic000.png
En/
    |
    ----- get_started/
                   |
                   ---- assets/            (put the resource file common to the md file in the get_started directory)
                              |
                              ------ pic.png
                   |
                   ---- get_hardware.md
                   |
                   ---- how_to_read.md
Zh/
```

If you want to show the images in `get_hardware.md`, put the image into the `assets` folder, use the following code to reference the image.
```
![pic](assets/pic.png)
![pic](../../assets/pic000.png)
```

### Chinese and English mixed

When writing Chinese documents, the Chinese characters should be separated by spaces as much as possible. Punctuation should use full-width symbols as much as possible.
Mainly to make it stand out and make the document more elegant.
For example, the following comparison:

---------

```markdown
In Micropython, we often use `deinit` to represent the destructor instead of setting the default value like STM32.
```
In Micropython, we often use `deinit` to represent the destructor instead of setting the default value like STM32.

----------

```markdown
In Micropython, we often use deinit to represent the destructor, instead of setting the default value like STM32.
```

In Micropython, we often use deinit to represent the destructor, instead of setting the default value like STM32.

---------


## Directory and file name

* The generated document directory is edited in the corresponding language folder `SUMMARY.md`

* The source document folder should be a function module corresponding to a folder, and the resource file (picture) is placed in the `assets` folder directory of the current path of the corresponding md document, which is more convenient when adding, deleting, and modifying.

```
Assets/                                 (put public resource files)
En/
   |
   ----- get_started/
                  |
                  ---- assets/          (put the resource file common to the md file in the get_started directory)
                  |
                  ---- get_hardware.md
                  |
                  ---- how_to_read.md
Zh/
```

* The file name is not limited to `README.md`, other file names are named with lowercase + underscore, such as `get_hardware.md`



## Chinese and English (multi-language) page file directory structure and file name are the same

Since there are multiple language switching options in the last generated page, clicking the switch will directly access the same path of the corresponding language, so the Chinese and English directory structure and file name must be the same.

For example, English is accessing `en/get_started/how_to_read.md`. After clicking the button for language switching, it will automatically access `zh/get_started/how_to_read.md`. If this file does not exist, it will report a `404` error!



## Module Document Content

* Need to include a module introduction in the file header
* Need to explain the constructor, function, constant, etc.
* **Explain that you can't be lazy. Simply translate the function name again. You need to explain the function of the function, the range of parameters, and the point of attention**



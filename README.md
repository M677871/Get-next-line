*This project has been created as part of the 42 curriculum by miissa.*

# get_next_line

## Description

get_next_line is a C function that reads a file one line at a time.
Each time the function is called, it returns the next line from a file descriptor.

The goal of this project is to learn:
- How file descriptors work
- How to use the read() function
- How to manage memory
- How buffers and static variables work

This function is useful for reading large files without loading the whole file at once.

## Instructions

Compilation:

gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c

Usage:

1. Open a file with open()
2. Call get_next_line(fd)
3. Each call returns one line
4. When there is no more data, the function returns NULL

Example:

#include <fcntl.h>    // open
#include <unistd.h>   // close
#include <stdio.h>    // printf
#include <sys/stat.h> //O_RDONLY
#include <stdlib.h>   // free

int fd = open("file.txt", O_RDONLY);
char *line;

while ((line = get_next_line(fd)) != NULL)
{
    printf("%s", line);
    free(line);
}
close(fd);

## Algorithm Explanation

The algorithm works in simple steps:

1. Read data from the file using a buffer
   The data is saved in a static variable called stash
   Reading stops when a newline is found or the file ends

2. Extract one line
   Everything up to the first newline is returned as a line

3. Save the remaining data
   The part after the newline is saved for the next call

4. Repeat until the file is fully read

Why this algorithm:
- It does not read the whole file at once
- It works with any buffer size
- It supports very long lines
- It respects 42 memory rules

## Technical Choices

- A static variable is used to keep data between calls
- Custom string functions are used
- Memory is always freed correctly
- Errors are handled safely

## Resources

References:
- man read
- man open
- man malloc
- 42 get_next_line subject

AI Usage:

AI was used to:
- understand deeply how the functions open(), read(), memory leaks,
  and timeouts work....
- improve this README

AI was not used to write the project code.

## Notes

- The project follows the 42 Norm
- Works with files and standard input
- Simple, safe, and efficient

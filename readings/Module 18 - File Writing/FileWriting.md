# File Writing

## Introduction

In order to save information between program runs, data must be written to disk. “Disk” refers to the hard drive on your computer - while they aren’t usually actual spinning disks anymore (modern computers will use Solid State Drives, or SSDs), “disk” is still a common term to refer to this type of storage. Data that’s written to the hard drive is physically stored in a way that doesn’t require constant electricity or a running program to preserve - anything that doesn’t disappear when you reboot your computer is **written to disk**. This is in contrast to **volatile storage**, which does require constant electricity - RAM (random access memory) is the most common type. “Memory” vs “disk” is how this split is often expressed.

It’s worth noting that the only data your program can interact with directly must be in memory - that means that data must be read from (or “loaded from’) disk before it can be used, and similarly, data must be explicitly written to disk to be saved somewhere.

## Classes

Much like with file reading, there are many ways to write data in Java. For our purposes, we’ll be using a class called BufferedWriter, and it behaves very similarly to its counterpart, BufferedReader.

Constructor:

`public BufferedWriter(FileWriter output)`

Much like a BufferedReader takes in a FileReader, BufferedWriter takes in a FileWriter:

```
BufferedWriter exampleWriter = new BufferedWriter(new 
    FileWriter(“outputFile.txt”));
```

The three methods we’ll be using from this class are:

`public void write(String str)` 
This method writes out the provided String to the file. Unlike readLine or println, though, this **does not include a line break** - calling write multiple times will put all the text on one line

`public void newLine()`
This method adds an actual line break to the output file. Often, it’s paired with a single call to write

`public void close()`
While it’s technically a good idea to call `close` on BufferedReaders as well, for BufferedWriter it’s a bit more critical. The “buffer” part of the name builds up the data to be written in memory, and only writes it once either: enough data is there, or someone calls close() to deliberately request that data be written. If your data isn’t showing up in the files you’re writing, double-check that close() is being called.

## Buffering

Physically writing data to a hard drive has (relatively speaking) a lot of slow overhead. Having a task have some fixed-cost overhead is a fairly common problem in both programming and the real world, and the solution is the same: combine many small pieces of work into one single larger piece of work. For example, if you were ordering lunch for a group of people at a deli, you would order all the sandwiches in one order, and then pay for it in one go - ordering and paying for each sandwich individually would involve the overhead of “paying” being repeated more often than necessary.

Any sort of batching or buffering solution will have a similar structure: build up some amount of work (for BufferedWriter, that’s roughly 8 kb of data), process it all at once, and repeat. Then, at the end, always process the remaining partial batch. That last step is what close() on a BufferedWriter does, and it’s something that any program involving buffering or batching needs to handle.

## Append vs Overwrite

When writing to a file, the default behavior is to delete any existing file with that name, and overwrite the file with new data. This isn’t quite as odd as it sounds - for everything except plain-text documents, being able to “just add data to the end” generally doesn’t work. For example, a .docx file, a .pdf, or a .jpg are not formats that work well with appending data (trying to do so is a good way to corrupt the entire file).

However, plain text documents aren’t exactly unusual, so you can choose to append to a file if you want: the FileWriter constructor is overloaded, which means there’s a second version. That second version takes an additional boolean parameter to decide if the file should be appended to or not - true means the writer will append to the file, false means it will overwrite the file (the default is false).

So

`BufferedWriter appendToFile = new BufferedWriter(new FileWriter(fileName, true));`

will append to the file represented by `fileName`, while

`BufferedWriter overwriteFile = new BufferedWriter(new FileWriter(fileName));`

will overwrite any existing contents. If the file doesn't exist, both versions will create a new file.

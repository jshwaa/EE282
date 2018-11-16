_Ask a question that requires a student to understand navigation and manipulation of directories in a filesystem. Your question should require an answer using at least the following commands/concepts: cd, ../, mkdir, rmdir_

__1. In a Unix environment/filesystem, what commands (and arguments) would you use to create, in your home directory, an "analyses" directory that contains "data" and "scripts" subdirectories? How would you move into the "/analyses/data" directory, move back into its parent directory, and subsequently remove the "data" directory?__ 

_A:_ You can use the command `mkdir ~/analyses` to create an "analyses" subdirectory in your home directory from wherever you currently are in the filesystem due to the `~/` part of the argument.  Next, you would use `mkdir ~/analyses/data ~/analyses/scripts`, with each argument telling the program to create a "data" and "scripts" subdirectory within this "analyses" directory. You would then use `cd` to _change directories_ to `/data` with `cd ~/analyses/data`, and `cd ../` to move back out and into the new folder's parent directory, where "../" serves as a relative path to the current parent directory. Finally, you would remove `./data` with `rmdir ./data', with "./" serving here as a relative path to the directory you are currently in and sidestepping the need to type the absolute path out.

### Question 1 Comments:
Very nicely done! Great job.

_Ask a question that requires a student to understand the difference between accessing a column in a matrix with numeric indices versus accessing a column in a data frame with numeric indices. Your question should require an answer comparing the following: mymatrix[,1] vs. mydf[,1] vs. mydf[1] vs. mydf[[1]]._

__2. While matrices and data frames in R are both two-dimensional data structures, data frames act as spreadsheets that blend aspects of both matrices and lists. For instance, all elements within a matrix are of the same data type, whereas columns in a data frame act like lists that can contain different data types from each other as long as they are the same length. This introduces subtle differences in index subsetting/accessing values between the two structures. To investigate this, create and examine a matrix and data frame containing the same row-by-column arrangement of elements and compare the output of subsetting your matrix with [,1] to subsetting your data frame with [,1], [1], and [[1]].__

_A:_ To create the matrix and data frame I ran the code:

    mymatrix <- matrix(data = 1:12, nrow=4, ncol=3)
    mydf <- data.frame(mymatrix)
    mymatrix
    mydf

Subsetting my matrix and my data frame with [,1], and my data frame with [[1]] all returned the entire first column of the matrix/data frame as a vector: `[1] 1 2 3 4`, whereas subsetting my data frame with [1] returned these values as a data frame with a single column (a.k.a. a list):

     X1
    1 1
    2 2
    3 3
    4 4

This shows that matrices and data frames can return the same column vector by indexing with a comma or double brackets, but using single brackets will return the corresponding data frame column with its column header (rather than a vector).


_Ask a question that requires a student to understand how to create a simple script and make it usable by everyone, but only writeable by its creator. Your question should require an answer using chmod NNN (using octal permissions).
Hint 1: in order for a script to be executable, it must be readable and executable
Hint 2: in order for a script to be executable, all of its parent directories must be executable_

__3. You are the head TA of a class on Unix with multiple discussion sections. To make things easier, you want all TAs to keep their students' grades in a single file with the same Unix path from their home directory, _i.e._ `~/class/sections/discussion/grades`. Make a script that you can distribute to your TAs that builds this path and grades file, and that is usable by everyone but only writeable by you.__

__A.__ First, you would use the module `vim` as a simple text editor to create a script named "discgrades.sh" in your folder `~/TAscript` with `vim ~/TAscript/discgrades.sh` that contains:

    #!/bin/sh
    echo What is your class discussion section?
    read SEC
    mkdir -p  ~/class/sections/$SEC
    touch ~/class/sections/$SEC/grades
    echo Your grades folder for discussion section $SEC has been created.

Then, to change access permissions for this file, you would use `chmod nnn path` where nnn indicates the octal values for permission bitmasks for __u__ser, __g__roup, __o__thers (__ugo__) in that order:

    chmod 755 ~/TAscript/discgrades.sh
    chmod 711 ~/TAscript
    chmod 711 ~/

These octal permissions make the script readable/writeable/executable/ for the user (7 = 111 bitmask = __r__(ead)__w__(rite)(e)__x__(ecute)) but only readable/executable by others (5 = 101 = r-x) and the parent directories executable by others so that the script can be accessed. The absolute path `~/TAscript/discgrades.sh` can then be shared with other TAs, allowing them to run the script that will create the directory structure for grading this class in their filesystems.

### Queston 3 Comments:
This was very well done, but there are a few things I would like to mention. The first being that the '~' is specific to each user and is the same as doing $HOME. with this case each user would have a different set of files. Also I was wondering what the purpose of read SEC was. The last thing is that inorder for users to read the discgrades.sh file the parent directories should also be readable by all users. i.e. ~/ and ~/TAscript so instead of 711, it should be 755 for all 3. Other than that, question 3 was very well done.

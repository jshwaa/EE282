Ask a question that requires a student to understand navigation and manipulation of directories in a filesystem. Your question should require an answer using at least the following commands/concepts: cd, ../, mkdir, rmdir

__1. In a Unix environment/filesystem, what commands (and arguments) would you use to create, in your home directory, an "analyses" directory that contains "data" and "scripts" subdirectories? How would you move into the "/analyses/data" directory, move back into its parent directory, and subsequently remove the "data" directory?__ 

_A:_ You can use the command `mkdir ~/analyses` to create an "analyses" subdirectory in your home directory from wherever you currently are in the filesystem due to the `~/` part of the argument.  Next, you would use `mkdir ~/analyses/data ~/analyses/scripts`, with each argument telling the program to create a "data" and "scripts" subdirectory within this "analyses" directory. You would then use `cd` to _change directories_ to `/data` with `cd ~/analyses/data`, and `cd ../` to move back out and into the new folder's parent directory, where "../" serves as a relative path to the current parent directory. Finally, you would remove `/data` with `rmdir ./data', with "./" serving here as a relative path to the directory you are currently in and sidestepping the need to type the absolute path out.

Ask a question that requires a student to understand the difference between accessing a column in a matrix with numeric indices versus accessing a column in a data frame with numeric indices. Your question should require an answer comparing the following: mymatrix[,1] vs. mydf[,1] vs. mydf[1] vs. mydf[[1]].

__2. While matrices and data frames in R are both two-dimensional data structures, data frames act as spreadsheets that blends aspects of both matrices and lists. For instance, all elements within a matrix are of the same data type, whereas columns in a data frame act like lists that can contain different data types from each other as long as they are the same length. This introduces subtle differences in index subsetting/accessing values between the two structures. To investigate this, create and examine a matrix and data frame containing the same row-by-column arrangement of elements and compare the output of subsetting your matrix with [,1] to subsetting your data frame with [,1], [1], and [[1]].__

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

This shows that matrices and data frames can return the same column vector by indexing with a comma or double brackets, but using single brackets will return the corresponding data frame column with its column header (i.e. a list rather than a vector).

Ask a question that requires a student to understand how to share access to a directory and a file in that directory on a Unix/Linux filesystem from their home directory with a colleague without exposing the user's entire directory. Your question should require an answer using chmod {u,g,o}{+,-}{r,w,x} (not using octal permissions).
Hint 1: in order to view a file, all of its parent directories must be executable
Hint 2: in order to view a file, the file itself must be readable

# cd Command Line
1. ![CSE15Lab1pic1](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/9ea08a38-4a61-48c0-8837-eaa352750bd6)

   When the command is run, we are in the home directory. Since there is no argument passed, we only change to the home directory which is the directory we're currently in. No matter where we are in the system, using the cd command line without any arguments brings us back to the home directory. There is no output because cd does not give outputs. Instead, it is for changing directories. The output is not an error because cd returns you to the home directory when you don't pass any arguments.

2. ![CSE15Lab1pic2](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/7035bce5-fd34-4ea5-bdb4-19151acb724a)

  When the command was run, I wasn't in any current working directory. However, since there was an argument this time with a path to directory lecture1, I was able to change to directory lecture1 as seen in the next line ~/lecture1. This was no error because the cd line allows us to change to a directory, in this case, lecture1.

3. ![CSE15Lab1pic3](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/996ff18c-3f26-40f4-90dd-bc133abc59ed)

   When the command was run, there was an error stating that vi.txt is not a directory. Using cd with a path to a file as an argument results in an error because the command cd is used to change directories and not to access files.

# ls Command Line
![CSE15Lab1pic4](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/78121ea0-c0a7-424c-9848-03a151373b07)

1. In the first line where I use the ls command with no arguments, the output was lecture1 which shows the current file in the the home directory. lecture1 was the only current output because it was the only folder in the working directory. The output is not an error because ls command shows the names of the files and folders inside the current working directory.
2. In the third line where I use the ls command with a path to a directory, the working directory is now lecture1 and the output displayed are the folders, classes, and README within the lecture1 directory. This output is not an error.
3. In the fifth line where I use the ls command with a path to a file, there is an error because the ls command only shows the names of files and folders. The command line cannot access the file itself because that is not the purpose of the ls command.

# cat Command Line
1. ![CSE15Lab1pic5](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/3961a0f2-7375-471f-9ef1-629dbcc7566c)

   When the command was run and there were no arguments, the output would repeat whatever was typed and the line was never prompted to end. Since cat stands for concatenate, the line reads data from the file and gives its content as output. Since there is no file, the output just repeats the input but this is not an error since there was no file as an argument.

2.![CSE15Lab1pic6](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/6f9c7597-51a9-4dd8-8249-02cac2602f75)

  When the command was run with a path to a directory, the output just states that the argument is a directory. This is not an error but the cat command line works for files and not directories.

3. ![CSE15Lab1pic7](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/d2c5229b-3e91-4de1-9b5c-dc30f9cf4d23)

  When the command was run with a path to a file, the line reads data from the file and gives its content as output so this is not an error. 

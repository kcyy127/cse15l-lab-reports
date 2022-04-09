# How to log into a course-specific account on `ieng6`

## Step 1: Installing VScode

[Download](https://code.visualstudio.com/download) and [set up](https://code.visualstudio.com/learn/get-started/basics) Visual Studio Code on your computer. You should be able to open a VScode window like this:

![Image](/images/vscode.png)

Since we will be creating Java files later on in this tutorial, it would also be helpful to [set up Java](https://code.visualstudio.com/docs/languages/java) on VScode.


## Step 2: Remotely Connecting

Windows users need to install [OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) for this step.

Use the [Account Lookup tool](https://sdacs.ucsd.edu/~icc/index.php) to retrieve your course-specific account and change your password if necessary.

Open a terminal in VScode with the shortcut Ctrl + ` (backtick) and type in the command 
```bash
$ ssh [account]@ieng6.ucsd.edu
```
and type in your password when prompted. 

Say yes to the following message if this is the first time you are logging on.
```
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't
be established.
RSA key fingerprint is
SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting
(yes/no/[fingerprint])?
```
You should see something similar to the screenshot below on your terminal

![Image](/images/log-on-screen.png)

To terminate the connection, type `exit` in the command line.

## Step 3: Trying Some Commands

We can try some commands on the remote server:

| Command | Usage |
| --- | --- |
| cd \<directory\> | change directory |
| ls | list files (of current directory) |
| ls -a | list all files, including ones that start with a dot|
| ls -l | list files in long format |
| ls -t | list files by date | 
| cp \<source\> \<destination\> | copy source file to destination file | 
| cat \<file\> | shows the contents of the file |

The results of these commands can be seen here:

![Image](/images/commands1.png)

![Image](/images/commands2.png)

## Step 4: Moving Files with `scp`

On your computer's terminal, create an edit a Java file
```bash
$ touch WhereAmI.java
$ vim WhereAmI.java
```
and change its contents to the information below 
```Java
class WhereAmI {
    public static void main(String[] args) {
        System.out.println(System.getProperty("os.name"));
        System.out.println(System.getProperty("user.name"));
        System.out.println(System.getProperty("user.home"));
        System.out.println(System.getProperty("user.dir"));
    }
}
```

Type the following to copy the file over to the remote server's home directory
```bash
$ scp WhereAmI.java cs15lsp22zz@ieng6.ucsd.edu:~/
```

Then log onto the remote server and check if the file's been successfully copied with the command to list files `ls`.

![Image](/images/scp.png)

## Step 5: Setting an SSH Key

To quicken the process of logging onto a remote server, we will create `ssh` keys.

Type the command `ssh-keygen` on your computer's terminal. Press Enter to save the keys in the default folder. 

If you already have a key pair, you may choose to not overwrite it and skip to copying the public key to the server. If you do not have a key pair, you will be prompted to enter a passphrase. Do not add one by pressing Enter twice.

Having generated the public/private keys, we must now copy the public key to the remote server. First, log on to your remote server and create the `.ssh` folder
```bash
$ mkdir .ssh
```
Terminate the connection after this step.

On your computer, type in the terminal
```bash
$ scp ～/.ssh/id_rsa.pub cs15lsp22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys
```

You should now be able to log on or copy files to the remote server without a password:

![Image](/images/ssh-keygen.png)

## Step 6: Optimizing Remote Running

Suppose we now have edited `WhereAmI.java` on our computer to look like the following
```Java
class WhereAmI {
    public static void main(String[] args) {
        System.out.println(System.getProperty("os.name"));
        System.out.println(System.getProperty("user.name"));
        System.out.println(System.getProperty("user.home"));
        System.out.println(System.getProperty("user.dir"));
        System.out.println("This is an updated file");
    }
}
```
 and would like to both upload and run the file on the remote server.

 The steps required would then be to 
 1. `scp` the file to the remote server,
 2. compile the Java file with `javac WhereAmI.java` on the remote server, and
 3. run the Java class with `java WhereAmI` on the remote server

The consolidated command to run all three steps would be
```bash
$ scp WhereAmI.java cs15lsp22avs@ieng6.ucsd.edu:~/; ssh cs15lsp22avs@ieng6.ucsd.edu "javac WhereAmI.java; java WhereAmI"
```
which would yield the following output:

![Image](/images/optimization.png)

The arguments after `ssh [account]@ieng6.ucsd.edu` are commands that would run on the remote server, and the semicolons separate individual commands that need to be run.
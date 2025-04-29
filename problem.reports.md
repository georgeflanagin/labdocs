# How to report problems with workstations

## With calculations ...

There are pieces of information we need to solve almost every problem.

- Your name, as it appears in UR's documentation. 
- Your `netid`. It can be difficult to figure out when it is something
    like `ae9qg`.
- Time the problem happened. Use "15:40, April 29", not "Yesterday afternoon 
    just before I left.
- Name of the workstation, or if the problem involved interaction between
    workstations, the names of all the workstations involved.
- Explain what you were doing. 
    - Which program you were running, including the full version. Ex: "Columbus 7.2.2"
    - The complete names of the input files and result files. Hint: 
        You can get the complete name of a file with `realpath {filename}`.
    - Where were you logged in? Ex: "I was logged in at Erica's console," or 
        "I was ssh-ed into Kevin from my laptop."
    - Was your program being run interactively or from a script? What script?
    - If you were running the program interactively, please send along the last few 
        commands by using `history > {filename}`, and attach the file to your email.

## With connectivity ...

These are the "*I cannot SSH to Fred*" problems. You can do a bit of
diagnosis that is helpful, and that will reduce the time it takes to
solve the problem. Let's pretend that `fred` is the name of a workstation.

### Can the computer in question be seen by you on the network?

Type `host fred`. You should see something like this.

`fred.richmond.edu has address 141.166.220.100`

If you get an error, `fred` is either the wrong name or the workstation
is incorrectly entered in UR's DNS system.

### Can you ping it?

Type `ping -c 4 fred`. This will send `fred` four packets at one second
intervals to echo back to you. If you get them all back, then fred has
an network card that is correctly attached to the network.

### Can you reach SSH's port on the other end?

Type `nc -zv fred 22`. SSH's port is `22`, and `nc` is the most general
network connectivity program extant. `-zv` asks if port 22 is even open
(accepting network traffic) at all.

If you cannot reach port 22 on fred, it could be a problem with "network
routing" of SSH. If this is the case, you *may* be able to find out more
information with `traceroute fred`. If `traceroute` hangs and cannot
continue, save the output for diagnosis.

### Is SSH listening on port 22? 

Type `nc fred 22`. You should get back the version of SSH that is
listening. For example, `SSH-2.0-OpenSSH_8.7`.

### What happens when SSH tries to connect and authenticate?

Type `ssh -v fred` (assuming you are using your current `netid`).
Because you are having problems connecting, the command will still fail,
but the `-v` will tell you more about how and why. Save the (rather large)
output to the screen, and attach it to an email.



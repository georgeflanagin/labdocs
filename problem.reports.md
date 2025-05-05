# How to report problems with workstation connectivity.

Let's pretend that `fred` is the name of a workstation.
These are the "*I cannot SSH to Fred*" problems. You can do a bit of
diagnosis that is helpful, and that will reduce the time it takes to
solve the problem. 


### Can the computer in question be seen by you on the network?

Type `host fred`. You should see something like this.

`fred.richmond.edu has address 141.166.220.100`

If you get an error, `fred` is either the wrong name or the workstation
is incorrectly entered in UR's DNS system.

As strange as it sounds, we sometimes see problems where a workstation
has more than one name, or the names and IP addresses are not 
correctly paired. Make sure that this command tells you the 
address belongs to `fred` or `fred.richmond.edu`!

`host 141.166.220.100`

### Can you ping it?

Type `ping -c 6 fred`. This will send `fred` six packets at one second
intervals to echo back to you. If you get them all back, then fred has
an network card that is correctly attached to the network. If you get
some but not all back, then it is time to check `fred` for a loose
network cable.

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



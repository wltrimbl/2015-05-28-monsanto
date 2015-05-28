---
layout: page
title: Extra Unix Shell Material
subtitle: Connecting to remote machines
minutes: 5
---
> ## Learning Objectives {.objectives}
>
> * Learners should be able to explain the relationship between public and private keys.
> * Learners should be able to explain why passphrases are such a good idea
> * Learners should know that passwordless authentication is available using the clients ssh (for shell access and command execution) and scp (for file transfer).
 
> ## Passwordless login is possible and can be made safe.
The owners (or lessors) of computers have the right to control 
who uses their computers, and you won't be able to find a 
computer that allows you to run shell commands without 
establishing a relationship in advance with the computer's 
operator.  Unguarded computers that will do anything one asks
of them can do bad things very quickly.

So everyone in the lab has a username and password.  

The now-universal protocol for remote access to machines running
unix/linux/mac os is SSH.  How many people use SSH?  And how many
of you type your password every time you use SSH?

Password authentication is when the server compares your username
and a scrambled version of your password to a database of 
usernames and scrambled passwords.

xkcd password security

Public-key authorization is a different approach, in which you 
(or a server acting on your behalf) generates a pair of keys, 
called the **private key** and the **public key**.

The private key is aptly named--it is kept secret, because possession
of the private key is what is tested for in authentication.

The public key, by contrast, can be shared openly and can be distributed over non-secure channels.

To set up passwordless login, you must 
* generate a public / private key pair
* put the public key in the special file `~/.ssh/authorized_keys` on the host
* put the private key on the client (usually in `~/.ssh`)
* ensure that the private key can't be read by other users (this is required, ssh will not use your key unless the permissions are 700)
* associate the key with the host (on the client) (usually in '~/.ssh/config`)

You can find instructions on how to do this online.

The big caveat: once you've set up passwordless login in this 
way, anyone who has your private key can log in as you.  
Should your server be hacked, or should a malicious sysadmin 
want to frame you for something, your keys are there, on the
filesystem, and everyone knows where they're kept.

The solution to the leaving-the-keys-under-the-doormat problem is
the passphrase.  It's called a passphrase to encourage you to 
make a long one.  If you use a passphrase when you create your
keys, your enemies will have to guess your passphrase before they
can log in as you.  (They can guess your passphrase in private,
which is why it needs to be more than 8 characters long!)

And finally, ssh-keyagent remembers your passphrase on your 
computer while it's running, so you should only have to type your
passphrase once every time you boot your laptop.





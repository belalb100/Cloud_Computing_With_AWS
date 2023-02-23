# Using the SSH protocol to clone into our GitHub repo:

SSH keys are cryptographic keys that are used for authentication when connecting to a remote server using SSH. They are similar to passwords in that they are used to verify the identity of the user, but they offer several advantages over passwords in terms of security and convenience.

One of the main advantages of SSH keys is that they are much more difficult to crack than passwords, as they are typically much longer and more complex. Additionally, SSH keys are not vulnerable to brute-force attacks, as each key is unique and cannot be easily guessed.

Another advantage of SSH keys is that they can be used to automate the login process, which can save time and reduce the risk of errors. This is especially useful for system administrators who need to log in to multiple servers on a regular basis.

Overall, SSH keys provide a more secure and efficient way to access remote servers than traditional password-based authentication.

![Alt text](../images/SSH%20RSA%20key.png)



Firstly we open our gitbash to start the process of producing an RSA key which consists of a Private key and a public key.

We then `cd .ssh` into our SSH folder then we enter `ssh-keygen -t rsa -b 4096 -C "emailaddress` and then press enter. `b` means bytes here and `C` is us specifying the owner of the key.
Next we name our RSA key for example`github-key` then it will ask us for a passphrase we can leave this blank by pressing enter twice.

Next we go to our github account and go to settings and then click on `SSH and GPG keys` then we select new `SSH keys` then we give it a `Title` this title should refer to what the key is going to be used for for example Jenkins etc. Next we go back to Git Bash and git the public part of our key and copy and paste in into the key area of GitHub and then we select `Add SSH key` and we should see it added to our SSH keys.

Now in our Gitbash we are going to add a private key to our ssh by using the following command in the same Git Bash terminal with have been using. ``eval `ssh-agent -s`` we do this to install an agent you must use the little quote like symbol, we will then get a process I.D then we enter `ssh-add keyname` and it should tell us identity added then we enter `ssh -T git@github.com` to make sure it was successful.

Next in GitHub we will make a repo without a README for example called `demo-test`

then we go back into our same Git Bash terminal and go to where we usually store our repo i.e. `cd` command into there.
Here we make a new folder here with the same name as our repo using `mkdir foldername` and the cd into there and then we use `touch filname.md` to make a readme file then `nano` command to our  README.md and write something in it so that way we can see if it worked. We can use `cat filename` to see if the Readme.md has been edited.
next we use `git init` then `git add .` which will add everything then `git status` to track it and see if it worked then `git commit -m "added readme.md"` then we enter `git branch -M main` to move to main branch as we are currently in the master branch as git init creates this by default. Then `git remote add origin copy_here_ssh_from_github` this specifies the remote we would like to use and where it is that we will push and pull changes the remote here is the one in the cloud.
then we use `git push -u origin main` and the we should be done.
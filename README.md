# Cyberpanel-fixperms
A script to fix permissions and ownership, on files and directories, for Cyberpanel accounts.

This script is modified from https://github.com/whattheserver/cyberpanel-fixperms 

THIS SCRIPT WILL BASICALLY CHOWN THE WHOLE DOMAIN FOLDER INSTEAD OF PUBLIC_HTML OR SUB DIRECTORIES. 

If you have messed with cyberpanel migration, you'll know why you need this script. 


## More Info
Ever needed just to quickly 'fix' the permissions or ownership for your files in a regular Cyberpanel account? This is the script for you. There is a staggering number of people using Cyberpanel out there, and this script will help every Cyberpanel user quickly recover from self-made permission mistakes or allow you to be lazy when setting permissions when uploading new scripts (ex: Wordpress).

It safely steps through the file structure only in a particular user, and sets folders to be owned by the user, and files to have Cyberpanel-recommended permissions.

It is safe to run, and I would run it in a heart-beat as a general 'fix my errors' fix.

The script is also compatible with multiple attached volumes on their servers, such as multiple home directories with Cyberpanel (eg., /home, /home2, /home3, etc).

Note: This is intended for **non-DSO** servers (Meaning, it will run just fine for: FastCGI, suPHP, etc...). You _can_ run this on a DSO box, but just know that things such as Wordpress uploads won't work. You'll have to manually set some folders to be owned by the user "nobody".

## Instructions

### Fixperms - for one single user

To get the `fixperms` script, simply wget the file from Gitlab and make sure it's executable:

```bash
wget https://raw.githubusercontent.com/sweezie/cyberpanel-fixperms/master/fixperms.sh
chmod +x fixperms.sh
```

Then, run it (with ROOT permissions) while using the 'a' flag to specify a particular Cyberpanel user:
```bash
sudo sh ./fixperms.sh -a USER-NAME
```
It does not matter which directory you are in when you run fixperms. You can be in the user’s home directory, the server root, etc... The script will not affect anything outside of the particular user’s home folder.

### Fixperms - for all of the users:
If you would like fix the permissions for every user on your Cyberpanel server, simply use the '-all' option:

```bash
sudo sh ./fixperms.sh -all
```

### Verbosity of Fixperms
By default, the script runs in a 'quiet' mode with minimal display. However, if you’re like me, you may want to see everything that is happening. You can turn on verbosity and have the script print to the screen everything that is being changed. I find this extremely useful when fixing large accounts that have many files. You can watch the changes as a sort of 'progress bar' of completion. The '-v' option can be used per account or with all accounts.

#### For one single account ####
```bash
sudo sh ./fixperms.sh -v -a USER-NAME
```

#### For all accounts ####
```bash
sudo sh ./fixperms.sh -v -all
```

### Getting Help
You can run `fixperms` with the '-h' or '--help' flags in order to see a help menu.

You can also open an issue here on GitHub if you see any problems.

### Adding Fixperms to your bin
I host numerous websites for friends and family, who will routinely make mistakes in regards to file permissions. It's understandable; they're not tech people. I will need to fix their permissions for them pretty frequently on my servers so I opted to put the `fixperms` script in all my servers' bin folders.

```bash
sudo mv fixperms.sh /usr/bin/fixperms
```

## History: Originally forked from https://github.com/PeachFlame/cPanel-fixperms
Now that `fixperms` is in Github, all contributors will have proper credit. However, before the move to Github, there were a 2 inidividuals that were crucial to the scripts existence:

- Dean Freeman
- Colin R.

## Contributing
If you would like to contribute, simply create a new feature branch, named for the fix, and submit a merge request.

CloudMake
==============================================

CloudMake is a Scalable Cyber Cloud (TM) script that will send a compilation
job of your choice to a remote machine accessable via SSH. 

Dependencies
----------------------------------------------

This needs `rsync` and `sh` to run on the host. If you lack either of these, the 
script will yell at you and/or not function as expected. 

On the remote host, you need `make` installed, as well as `ssh` and potentially
`rsync`. `sshd` needs to be running on the remote box

Installation
----------------------------------------------

Installation is simple, because this is a shell script; just place this in 
`~/bin` (or some system path if you prefer) and ensure wherever you place it 
is in your `PATH`.

Step-by-step instructions:

1. Clone this to your home directory using git
2. Execute:
    
    mkdir -p ~/bin; cp ~/cloudmake/cloudmake ~/bin; export PATH=$PATH:~/bin

(Please note you will have to make ~/bin persist in your PATH if it does not 
already. So you will need to go into either `.bashrc` or `.zshrc` (or your 
shell of choice's init script) and add `export PATH=$PATH:~/bin`.)
 
Usage
----------------------------------------------

For best results, set up your remote host to do passwordless logins 
([see here](http://macnugget.org/projects/publickeys/) for how to do that).

Generic usage from the help context:

    -h            -- Show help
    -u username   -- Use the given username instead of the default 
    -s servername -- Use the given server instead of the default 
    -r path       -- Remote path to do the compilation on 
                     (default ./cloudbuild)
    -n            -- Do not clean the remote path before building
    -j jobs       -- Use 'jobs' jobs when compiling (default 4)
    -d            -- Delete any files on remote host that don't exist on local
                     host in the build directory. (Same as rsync's --delete)
    -l path       -- Local path to build. (default .)
    -f            -- On build failure, give a shell on the remote host
    -t makeTarget -- Target for the makefile to make
    -p port       -- SSH Port to use (default 22)
    -v            -- Give more verbose output


Troubleshooting
----------------------------------------------

**If you're getting asked for your password 30,000 times**:

- See [here](http://macnugget.org/projects/publickeys/) for how to set up 
    passwordless logins on a remote server

If you get an error from ssh, be sure:

- You have the correct host and username
- The server is available at port 22. Otherwise, use the -p option detailed 
    above.

If you get an error from rsync, be sure:

- You have write permissions in the remote directory
- You have read permissions form the local directory

If you get a build error:

- I feel your pain. :)


# ore-ssh-config
Common configurations and public keys for our SSH services

## Making Changes to This Repository
It is **highly recommended** that you learn how to use the Github repository in order to update keys instead of
editing the files directly on the servers. Doing so helps us keep track of who made what changes, and makes it
easier to ensure that all server configurations remain synchronized. Here is the general process for making
such changes:

1. **Fork this repository** (using the button at the top of the page) to a place where you can make changes
to the files.

2. **Edit the [config](https://github.com/OpenRedstoneEngineers/ssh-config/edit/master/config) and [authorized_keys](https://github.com/OpenRedstoneEngineers/ssh-config/edit/master/authorized_keys) files** and make the changes that you need to make. When you
finish, scroll to the bottom, and select the option to "Create a **new branch**" before committing.

3. **Fill out the pull request** submission form that you are directed to. Give it a **meaningful title and 
description** that summarizes the changes you made. This will make it easier for admins to review the changes.
When you are done, click "Submit."

## Installing on a Server

### New Servers
If you are creating a new server, you will need to install packages `git openssh-client openssh-server` from your
package manager. After these are installed, log in as a superuser and follow these instructions:

1. **Create a user account** for the ORE services. The standard name for this user account is `mcadmin`. The command
should look like this: `# useradd mcadmin`

2. Switch to that user and go to its home directory using `# su mcadmin` and `$ cd`.

3. **Clone this ssh config** by executing `$ git clone https://github.com/OpenRedstoneEngineers/ssh-config.git .ssh`.

4. Run `$ ssh-keygen` to **generate an SSH keypair** for the new account. It will prompt you for a destination
file and passphrase. The default destination and no passphrase is recommended.

5. Read the user's public key by executing `$ cat .ssh/id_rsa.pub` and share it with an ORE developer. *Do not
publicize your private key!* The contents of `.ssh/id_rsa` should be kept secret and should *never* be transferred
over unencrypted connections.

### Existing Servers
If your server already has an `mcadmin` account with ssh keys, these directions will make the process much easier.

1. **Log in** to your `mcadmin` account and `$ cd .ssh/`.

2. **Backup any previous configuration file** to avoid conflicts: `$ mv config config.bak && mv authorized_keys authorized_keys.bak`.

3. **Initialize a new Git repository** in the SSH config directory with `$ git init`.

4. **Add a new remote** pointing to this GitHub repository and pull its changes:
`$ git remote add origin https://github.com/OpenRedstoneEngineers/ssh-config.git && git pull origin master`

## Updating on a Server
The updating process is relatively simple. Users can create pull requests to this repository on GitHub for config or
key modifications. These pull requests will be reviewed by the active admins and will be merged if approved. However,
changes to the repository on GitHub are *not* automatically pulled to the other servers. Server owners must occasionally
run `$ git pull origin master` in the account's `.ssh/` folder in order for changes to be applied.

This process can be automated by putting the above command in a `cron` job; however, this is **not advised**
as file conflicts can and will occur that must be resolved by the user.

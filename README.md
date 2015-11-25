# ore-ssh-config
Common configurations and public keys for our SSH services

## Installation

### New Servers
If you are creating a new server, you will need to install packages `git openssh-client openssh-server` from your
package manager. After these are installed, log in as a superuser and follow these instructions:

1. Create a dedicated account for the ORE services. The standard name for this user account is `mcadmin`. The command
should look like this: `# useradd mcadmin`

2. Switch to that user and go to its home directory using `# su mcadmin` and `$ cd`.

3. Clone this ssh config by executing `$ git clone https://github.com/OpenRedstoneEngineers/ssh-config.git .ssh`.

4. Run `$ ssh-keygen` to generate a keypair for the new account. It will prompt you for a destination file and
passphrase. The default destination and no passphrase is recommended.

5. Grab the user's public key by executing `$ cat .ssh/id_rsa.pub` and share it with an ORE developer. *Do not
publicize your private key!* The contents of `.ssh/id_rsa` should be kept secret and should *never* be transferred
over unencrypted connections.

### Existing Servers
If your server already has an `mcadmin` account with ssh keys, these directions will make the process much easier.

1. Log in to your `mcadmin` account and `$ cd .ssh/`.

2. Remove any previous configuration file to avoid conflicts: `$ rm config`

3. Initialize a new Git repository with `$ git init`.

4. Add a new remote pointing to this GitHub repository and pull its changes:
`$ git remote add origin https://github.com/OpenRedstoneEngineers/ssh-config.git && git pull origin master`

## Updating
The updating process is relatively simple. Users can create pull requests to this repository on GitHub for config or
key modifications. These pull requests will be reviewed by the active admins and will be merged if approved. However,
changes to the repository on GitHub are not automatically pulled to the other servers. Server owners must occasionally
run `$ git pull origin master` in the account's `.ssh/` folder in order for changes to be applied.

This process can be automated by putting the above command in a `cron` job; however, this is not advised as file
conflicts can and will occur that must be resolved by the user.

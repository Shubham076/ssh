
# SSH and SCP Configuration Guide

This README provides a comprehensive guide on SSH (Secure Shell) configurations, key management, SCP (Secure Copy Protocol) commands, and port forwarding techniques.

## Table of Contents



## Default SSH Key Configuration

To set a default SSH key, edit or create your `~/.ssh/config` file and add the following:

`IdentityFile /home/myuser/.ssh/keyhello` 

## Generating SSH Keys

To generate a new SSH key:


`ssh-keygen -t rsa` 

## Copying SSH Keys to Server

To copy your SSH key to a remote server:

`ssh-copy-id -i [path to public key] user@server` 

This step add you public key to server `authorized_hosts` file

### Connect using a specific key:

`ssh -i [path to key] user@server` 

## SSH Config File Examples

### Host Configuration


```
Host tabs
     HostName tabs.com
     User     me
     IdentityFile ~/.ssh/new_rsa

Host scm.company.com
     User       cap
     IdentityFile ~/.ssh/git_rsa

Host project-staging
     HostName 50.56.101.167
     User     me
     IdentityFile ~/.ssh/new_rsa` 
```

Instead of typing long SSH commands with usernames, IP addresses, and key file paths, you can connect to your server with a simple, memorable alias. For example, `ssh myserver` instead of `ssh -i ~/.ssh/my_key.pem user@192.168.1.1`.

## Using SCP Command

To securely copy files from local to remote or vice versa:

### Copying from Local to Remote

```scp -i [path-to-key] [path-to-local-file] user@host:[path_on_host]
scp localfile.txt user@example.com:/path/to/remote/directory/
``` 

### Copying from Remote to Local

`scp user@example.com:/path/to/remote/file.txt /path/to/local/directory/` 

## Port Forwarding

### Local Port Forwarding

`ssh -L local_port:remote_host:remote_port user@example.com` 

### Using a Jump Host


`ssh -L 8888:rds-instance.example.com:5432 user@jumphost.example.com` 


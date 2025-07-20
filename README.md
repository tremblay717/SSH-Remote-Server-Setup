# SSH-Remote-Server-Setup
This is a very simple project where the goal is to demonstrate how to add public SSH keys to a remote server. Project Link: [Here](https://roadmap.sh/projects/ssh-remote-server-setup)

For this project, I am using a droplet on [Digital Ocean](digitalocean.com).

The cost of this project should not exceed a few bucks. I rented the cheapest option on Digital Ocean.

# Connecting to server
When creating a droplet, you will be asked to provide your public key:

![alt text](image.png)

If you don't have one yet, keep reading.

Go to your project droplet and access the console, this will open a new browser window.

![alt text](image-1.png)

![alt text](image-2.png)

You are now connected to your server. Now we need to generate a SSH key pair.

Open a terminal on your local host and type the following command:

```
ssh-keygen
```

You can press `Enter` to accept the default path (`~/.ssh/id_rsa`), or you can specify a custom path like `~/.ssh/user1` if you're managing multiple keys.

Once you hit enter, the keys will be generated.

With the example above, the command will save a pair of public and private keys.

The private key would be saved as `user1` and the public key as `user1.pub`.

![alt text](image-3.png)

We need to add the public key to the droplet. To do so, start by displaying the public key. 

```
cat ~/.ssh/user1.pub
```

Switch back to the remote server and access the authorized key file.
```
nano ~/.ssh/authorized_keys
```

Copy paste the public key, save and quit (ctrl-x, Y, Enter)

You should now be able to connect remotely.

Two requirements:
* Private key path. Ex. `~/.ssh/user1`
* Droplet IP Address

```
// ssh -i [private_key_path] root@[ip_address]

// Example
ssh -i ~/.ssh/user1 root@123.123.123.123
```

Press enter and you should be now connected.

Repeat steps to add another key pair.

# Fail2Ban
Fail2Ban is a daemon protecting your system from bruteforce attacks. I recommend following this guide for quick setup. 

Guide : [Using Fail2Ban for SSH Brute-force Protection](https://www.linode.com/docs/guides/how-to-use-fail2ban-for-ssh-brute-force-protection/)
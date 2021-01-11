# How to create a SSH key and access to remove server without password

Generate a key

    ssh-keygen

Now we can transfer the key to remote server

    ssh-copy-id -i ~/.ssh/id_rsa user@remotehost

This should be enough for basic installation.

The default name is `id_rsa` but we can use another name. In case we use, for ex, `~/.ssh/mykey` as filename, the following configuration is necessary

    nano ~/.ssh/config

    #My custom conf for server X
    Host remote.server.com
    RSAAuthentication yes
    IdentityFile ~/.ssh/mykey

    ssh-add ~/.ssh/mykey


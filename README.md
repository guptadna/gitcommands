Git commands
=====

****Check if ssh is already available***
```
ls -al ~/.ssh
```

***Generating the SSH keys***
```
ssh-keygen -t rsa  // will generate ~/.ssh/id_rsa.pub and linked with already

ssh-keygen -t rsa -C "workmail@gmail.com" -f "id_rsa_work"

```

**Make sure ssh agent is running**
```
eval "$(ssh-agent -s)
```

***Register the new ssh key***
```
ssh-add ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa_work
```


***Config***
```
cd ~/.ssh/
touch config           // Creates the file if not exists
code config            // Opens the file in VS code, use any editor
```
```
Personal account - the default config
Host github.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa

Work account-1
Host github.com-work_user1
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_work
```

***One active SSH key in the ssh-agent at a time***

ssh-add -l will list all the SSH keys attached to the ssh-agent
```
ssh-add -D            //removes all ssh entries from the ssh-agent
ssh-add ~/.ssh/id_rsa                 // Adds the relevant ssh key

ssh-add -D
ssh-add ~/.ssh/id_rsa_work
```

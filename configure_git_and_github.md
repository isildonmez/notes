### 1. Setup Git

```
git config --global user.name "Your Name"
git config --global user.email "yourname@example.com"

git config --global color.ui auto
```

To verify:

```
git config --get user.name
git config --get user.email
```

### 2. Create an acoount or Sign in

### 3. Create an SSH Key

Check if you have an SSH key already installed:

```
ls ~/.ssh/id_rsa.pub
```

If you see `No such file or directory`, create a new SSH key:

```
ssh-keygen -C yourname@example.com
```

> if you don't want to specify location or password, just press `enter`

### 4. Link your SSH key with Github

- Copy the output of `cat ~/.ssh/id_rsa.pub` (starts with `ssh-rsa` ends with your email address)
- Navigate to your Github account > Settings
- Click `SSH and GPG keys` > `New SSH Key`
- Paste the key > click `Add SSH key`

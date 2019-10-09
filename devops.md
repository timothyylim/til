# dev ops 

Quit hanging ssh session

```
$ ~. 
```

List all local users

```
awk -F'[/:]' '{if ($3 >= 1000 && $3 != 65534) print $1}' /etc/passwd
```

- [src](https://askubuntu.com/questions/410244/a-command-to-list-all-users-and-how-to-add-delete-modify-users)

Change user password

```
$ passwd user
```

Give user sudo access

```
$ usermod -aG sudo username
```


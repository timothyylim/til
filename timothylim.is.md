# Notes on our server

IP: 159.65.22.120

Users:

- root
- tim
- wolfie

Apps are stored at ```/var/company_name/```

## Handling routes

We use nginx. Expose localhost ports by editing the current config file:

```vim /etc/nginx/sites-enabled/```		

You may have to be a root user.

Then restart:

```sudo service nginx restart```	


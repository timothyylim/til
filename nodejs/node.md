# node 

Change node version:

```
$ n 11
```

https://github.com/tj/n

Access command line arguments 

```
const args = process.argv;
```

```
$ node server.js one two=three four
['node', '/home/server.js', 'one', 'two=three', 'four']
```

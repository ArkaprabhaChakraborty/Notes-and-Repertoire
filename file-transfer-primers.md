# File Transfer Primers

## Using HTTP servers&#x20;

### Python

```
python3 -m http.server
```

## Using netcat

On the receiving end running,

```
nc -l -p 1234 > out.file
```

will begin listening on port 1234.

On the sending end running,

```
nc -w 3 [destination] 1234 < out.file
```

will connect to the receiver and begin sending file.

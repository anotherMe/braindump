
# rm

## Remove files/folder older than

Remove files:

```bash
find /tmp -name "*.pdf" -type f -mtime +6 -exec rm -f {} \;
```

Where:

- type d --> directory
- type f -->  file
- mtime +16 --> just files older than 16 days


Remove folders (recursively):

```bash
$ find /PATH/DELLA/CARTELLA -type d -mtime +16 -exec rm -R {} \;
```
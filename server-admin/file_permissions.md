# File Permissions

## Change Permissions

```bash
chmod
```

### Make Script Executable

```bash
chmod +x script.sh
```

### Common Permission Modes

| Mode | Meaning |
|---|---|
| 755 | Owner full access, others read/execute |
| 644 | Owner read/write, others read-only |
| 700 | Owner only access |

---

# File Ownership

## Change Ownership

```bash
chown
```

### Change File Owner

```bash
sudo chown anthony file.txt
```

### Change Owner and Group

```bash
sudo chown anthony:developers file.txt
```

### Recursive Ownership

```bash
sudo chown -R anthony:developers myfolder
```
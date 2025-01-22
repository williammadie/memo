# GPG

## Commands

### Delete GPG keys

**Warning**: Normally, you should revocate the key before deleting it.

Delete a private key
```bash
gpg --batch --yes --delete-secret-keys private_key_id_1 ... private_key_id_n
```

Delete a public key
```bash
gpg --batch --yes --delete-keys public_key_id_1 ... public_key_id_n
```

### Ownertrust

List trust levels for all GPG keys in keyring
```bash
gpg --export-ownertrust
```

Clear all trust levels 
```bash
# Remove the file
cd ~/.gnupg
rm trustdb.gpg

# Recreate the file
gpg -k
```
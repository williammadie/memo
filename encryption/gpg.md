# GPG

## Commands

**Warning**: Normally, you should revocate the key before deleting it.

Delete a private key
```bash
gpg --batch --yes --delete-secret-keys private_key_id
```

Delete a public key
```bash
gpg --batch --yes --delete-keys public_key_id
```
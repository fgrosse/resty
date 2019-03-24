<h1 align="center">Resty</h1>

This helper script fetches the password and AWS credentials for a restic backup
that is stored in an Amazon AWS bucket from the GNU password manager [pass][1].

The first argument must be the name of the repo within pass assuming the
following password layout:

```
…
├── restic
│   ├── <repo-name>
│   …
…
```

The encrypted value of `restic/<repo-name>` should contain the environment variables
that are recognized by restic on the last four lines:

```
$ pass show restic/my-database
zahzaingohy7oozu1evoh6xeik6Zae9w

RESTIC_REPOSITORY=s3:s3.amazonaws.com/my-database-backup
RESTIC_PASSWORD=zahzaingohy7oozu1evoh6xeik6Zae9w
AWS_ACCESS_KEY_ID=…
AWS_SECRET_ACCESS_KEY=…
```

### Example usage

```
# Usage with single argument runs \"restic snapshots\" automatically
resty my-database

# List all snapshots explicitly
resty my-database snapshots

# Check the repository for errors
resty my-database check
```

[1]: https://www.passwordstore.org/

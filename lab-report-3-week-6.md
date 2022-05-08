# Lab Report 3

## Streamlining ssh Configuration

Editing `.ssh/config` with Nano

![ssh-config](/images/report-3/ssh-config-nano.png)

Logging into ieng6 with alias

![ssh-log-on](/images/report-3/ssh-log-in.png)

`scp` with alias

![ssh](/images/report-3/ssh-scp.png)

---

## Setting up Github Access from ieng6

Public key on github

![github-pub-key](/images/report-3/github-ssh-key.png)

Private (`id _ed25519`) and public (`id _ed25519.pub`) keys on ieng6 server

![ieng6-keys](/images/report-3/ieng6-ssh-keys.png)

Commiting on ieng6 server 

![git-commit](/images/report-3/ieng6-commit.png)

Pushing to Github from ieng6 server

![git-push](/images/report-3/ieng6-push.png)

[The commit](https://github.com/kcyy127/cse15l-lab-reports/commit/7157e937be1a729f49c678ecd48c30a365845a20)

---

## Copying whole directories with `scp -r`

Copying directory to ieng6

![Copying to ieng6](/images/report-3/scp-dir.png)

On ieng6 server

![Dir on ieng6](/images/report-3/dir-on-ieng6.png)


Compiling and running tests on ieng6

![Tests on ieng6](/images/report-3/ieng6-make-test.png)

Unable to `ssh ieng6 "cd markdown-parse;make test`. Error message

![Error](/images/report-3/error.png)
---
title: "GitHub suddenly rejected my SSH key (the fix was a .pub file?!)"
---

Today, `git pull` stopped working on my main laptop. `Permission denied (publickey)`, out of nowhere. I had changed
nothing, the key was still registered on GitHub, and pulling the same repository from another laptop (with another key)
worked fine.

## The rabbit hole

I'll spare you the full troubleshooting session[^session]. The key was mathematically sound (`openssl rsa
-check` said `RSA key ok`), the signature algorithm was the modern `rsa-sha2-512`, my `~/.ssh/config` was clean, and
GitHub's status page was all green. Still: `Permission denied`.

The fix turned out to be embarrassingly small. My `~/.ssh/github_rsa` has lived without a companion `.pub` file since I
re-installed my laptop. Generating one made authentication work again:

```console
$> ssh-keygen -y -f ~/.ssh/github_rsa > ~/.ssh/github_rsa.pub
```

I did not believe it either, so I tested it six times with the `.pub` file and six times without. Twelve out of twelve:
no `.pub` -- rejected, `.pub` -- accepted.

## Why on earth would that matter?

Because the `.pub` file changes *which authentication flow* OpenSSH uses. With a `.pub` file present, the client first
*probes* (offers the public key, waits for the server's OK) and only then signs. With only a private key, OpenSSH skips
the probe and sends a fully signed authentication request directly. Both flows are perfectly legal according to RFC
4252, and a stock `sshd` accepts both.

GitHub, as of today, apparently does not.

## Did something change on GitHub's side?

My money says yes. The server banner in my debug logs reads `6a2c000`, where GitHub's SSH frontend has historically
identified itself as `babeld-<hash>`. That smells like new server software -- one that rejects direct-signed publickey
requests. It would explain perfectly why everything worked in the morning and nothing worked an hour later, on a machine
where nothing changed.

Has anyone else hit this? Do you know what `6a2c000` is? Let me know -- and in the meantime: make sure your private keys
have their `.pub` siblings.

[^session]: Everything from `ssh -vvv` archaeology, via `openssl` key validation, to a controlled 12-trial experiment.

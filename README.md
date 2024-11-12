# How to automatically sign your commits to GitHub

It is necessary to configure Git with a GPG or SSH key to sign your commits and set Git to sign all commits by default. Here are the steps:

**Step 1: Generate a GPG Key (or Use an Existing One)**

If you don't already have a GPG key, create one with:
```bash
gpg --full-generate-key
```
Choose the default options, then enter your name and email (the same one you use for GitHub).

- To list your keys and find the key ID:
```bash
gpg --list-secret-keys --keyid-format LONG
```

- Output like this:
```
/Users/username/.gnupg/secring.gpg
-------------------------------
sec   4096R/ABCDEF1234567890 2023-09-22 [expires: 2025-09-22]
uid                          Your Name <your_email@example.com>
```

The `ABCDEF1234567890` part is your GPG key ID.

**Step 2: Configure Git to Use Your GPG Key**

Once you have your key ID, configure Git to use it by running:

```bash
git config --global user.signingkey ABCDEF1234567890
```

This command sets your signing key globally for Git. If you want to set it only for a specific repository, omit `--global`.

**Step 3: Set Git to Sign Commits by Default**

Enable automatic signing of your commits:

```bash
git config --global commit.gpgSign true
```

Now, every commit you make will be signed with your GPG key.

**Step 4: Export Your GPG Public Key and Add It to GitHub**

Export your GPG public key:
```bash
gpg --armor --export ABCDEF1234567890
```

Copy the output, go to [GitHub GPG keys settings](https://github.com/settings/keys), and add your GPG key.

**Step 5: Confirm Signing Works**

Make a test commit in a repository and check that it’s signed:
```bash
git commit -m "Test signed commit"
```

You can confirm the signature by running:
```bash
git log --show-signature
```

GitHub will display a "Verified" badge next to your commits if they are properly signed.

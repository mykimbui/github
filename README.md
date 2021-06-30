

## SSH Key

### Generation

We need to generate SSH keys which are going to be used by GitHub to authenticate you. You can think of it as a way to log in, but different from the well known username/password pair.

If you already generated keys that you already use with other services, you can skip this step.

Open a terminal and copy-paste this command, replacing the email with **yours** (the same one you used to create your GitHub account).

```bash
mkdir -p ~/.ssh && ssh-keygen -t ed25519 -o -a 100 -f ~/.ssh/id_ed25519 -C "TYPE_YOUR_EMAIL@HERE.com"
```

It will prompt for information. Just press enter until it asks for a **passphrase**.

:warning: When asked for a passphrase, put something you want and that you'll remember. It's a password to protect your private key stored on your hard drive.

:warning: When you you type your passphrase, nothing will show up on the screen, **that's normal**. This is a security feature to mask not only your passphrase as a whole but also its length. Just type your passphrase and when you're done, press `ENTER`.

### Giving your public key to GitHub

Now, you will give your **public** key to GitHub.

In your terminal copy-paste the following command:

```bash
cat ~/.ssh/id_ed25519.pub
```

It will prompt on the screen the content of the `id_ed25519.pub` file.

- Copy that text from `ssh` to the end of your email address
- Go to [github.com/settings/ssh](https://github.com/settings/keys)
- Click on the green button `New SSH key`
- Fill in the Title with your computer name (`Macbook Pro` for instance)
- Paste the **key**
- Finish by clicking on the **Add SSH key** green button.

To check that this step is completed, in the terminal run this.

```bash
ssh -T git@github.com
```

:warning: You will be prompted a warning, type `yes` then `ENTER`.

This is the expected result:

```
# Hi --------! You've successfully authenticated, but GitHub does not provide shell access
```

:heavy_check_mark: If you got this message, the key was added to GitHub successfully :+1:

:x: If you encountered an error, you will have to try again. Do not hesitate to **contact a teacher**.

<details>
  <summary>If <code>ssh -T git@github.com</code> does not work</summary>

  Try running this command before trying again:

  ```bash
  ssh-add ~/.ssh/id_ed25519
  ```
</details>


## GitHub CLI

CLI is the acronym of [Command-line Interface](https://en.wikipedia.org/wiki/Command-line_interface).

In this section, we will install [GitHub CLI](https://cli.github.com/) to perform useful actions with GitHub data directly from the terminal.

It should already be installed on your computer from the previous commands.

First in order to **login**, copy-paste the following command in your terminal:

:warning: **DO NOT edit the `email`**

```bash
gh auth login -s 'user:email' -w
```

You will get the following output:

```bash
! First copy your one-time code: 0EF9-D015
- Press Enter to open github.com in your browser...
```

Select and copy the code (`0EF9-D015` in the example), then press `ENTER`.

Your browser will open and ask you to authorize GitHub CLI to use your GitHub account. Accept and wait a bit.

Come back to the terminal, press `ENTER` again, and that's it.

To check that you are properly connected, type:

```bash
gh auth status
```

:heavy_check_mark: If you get `Logged in to github.com as <YOUR USERNAME> `, then all good :+1:

:x: If not, **contact a teacher**.

Then run the following configuration line:

```bash
gh config set git_protocol ssh
```

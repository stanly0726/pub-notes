# Github ssh key setup

## Generating a new ssh key

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

or, if your system doesn’t support Ed25519

```shell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

## Adding your ssh key to the ssh-agent

1. start the ssh-agent in the backgroun

    ```shell
    eval "$(ssh-agent -s)"
    ```

2. add your ssh **private key** to the ssh-agent If you created your key with a different name, replace _id_ed25519_ in the command with the name of your private key file.

    ```shell
    ssh-add ~/.ssh/id_ed25519
    ```

3. [add the ssh **public key** to your github account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

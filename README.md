# AElf DevContainer (BETA)

To use this devcontainer, click "Use this template" > "Create a new repository".

## Pre-requisites

- Docker: https://www.docker.com/
- VS Code: https://code.visualstudio.com/

## Create a new project

Ensure that you have Docker installed and running.

Clone your new repository to your local, then open the folder in VS Code.

Press `F1` in VS Code and type/choose `Dev Containers: Reopen in Container`.

## Scaffolding a new project

To scaffold a new project, use:

```bash
dotnet new aelf -n HelloWorld
```

Note that if you change `HelloWorld` to some other name, you will need to amend your `.github/workflows/main.yml`:

```yml
- name: Deploy to testnet
  uses: yongenaelf/aelf-testnet-deploy-action@v1.4.2
  id: deploy
  with:
    private-key: ${{ secrets.PRIVATEKEY }}
    wallet-address: ${{ secrets.WALLET_ADDRESS }}
    dll-filename: src/bin/Debug/net6.0/HelloWorld.dll.patched # add this and rename accordingly
```

## Automatic deployment with GitHub Actions

Firstly, create a wallet using aelf-command, then take note of the privatekey and the address and save them in GitHub secrets:

Link: https://github.com/YOUR_USERNAME/YOUR_REPO/settings/secrets/actions

Create repository secrets and amend `.github/workflows/main.yml`:

```yml
- name: Deploy to testnet
  uses: yongenaelf/aelf-testnet-deploy-action@v1.4.2
  id: deploy
  with:
    private-key: ${{ secrets.PRIVATEKEY }}
    wallet-address: ${{ secrets.WALLET_ADDRESS }}
```

Next, sign up for Portkey wallet and switch to testnet.

Claim some testnet tokens from the faucet at https://testnet-faucet.aelf.io/ by copy+pasting your Portkey wallet address.

Finally, using Portkey, send testnet tokens to the sidechain of your wallet (ELF_YOURWALLETADDRESS_tDVW).

Now, every time you push changes to the `src` folder, you can view your repository's Actions tab to see the deployment, view the transaction id, and proposal id.

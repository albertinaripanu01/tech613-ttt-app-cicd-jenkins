# tech613-ttt-app-cicd-jenkins

## 1. create an  in instance that runs tic tac toe app.
## 2. Create the SSH Key Pair

Open **Git Bash**.

Check whether the `.ssh` directory already exists:

```bash
ls -la
```

If the `.ssh` directory does not exist, create it:

```bash
mkdir ~/.ssh
```

Navigate into the `.ssh` directory:

```bash
cd ~/.ssh
```

Generate the SSH key pair:

```bash
ssh-keygen -t rsa -b 4096 -C "<your-email>"
```

This generates two keys:

- `<key-name>` — **Private key**
- `<key-name>.pub` — **Public key**

The key ending in `.pub` is the **public key**.

The other key is the **private key**.

To view and copy the public key:

```bash
cat <key-name>.pub
```

The public key should start with:

```text
ssh-rsa ...
```

> **Security:** Never share or commit the private key to GitHub. Only the public key should be added to the repository.

---

## 3. Add the Deploy Key to GitHub

Go to the GitHub repository and navigate to:

**Settings → Security → Deploy keys → Add deploy key**

Then:

1. Add a descriptive **Title** for the deploy key.
2. Copy the contents of the **public key** (`.pub` file).
3. Paste the public key into the **Key** field.
4. Select **Allow write access** if the CI pipeline needs to push changes to the repository.
5. Click **Add key**.

> **Security:** `Allow write access` should only be enabled when the pipeline needs to push changes to the repository. If only read access is required, it should remain disabled.

### How the Authentication Works

```text
CI / Jenkins Server
        |
        | Uses Private Key
        v
SSH Authentication
        |
        | GitHub checks corresponding Public Key
        v
GitHub Repository
        |
        | Public Key stored as Deploy Key
        v
Access Granted
```

The **private key** is kept securely on the CI/Jenkins side, while the **public key** is stored in the GitHub repository as a Deploy Key.

This allows the CI pipeline to securely authenticate with the GitHub repository without storing a GitHub password in the pipeline.

---

# GitHub Webhook Setup

A GitHub webhook was configured to automatically notify Jenkins when new code is pushed to the repository.

## Creating the Webhook

1. Open the GitHub repository.
2. Go to **Settings**.
3. Select **Webhooks**.
4. Click **Add webhook**.
5. Enter the Jenkins webhook URL as the **Payload URL**:

```text
http://52.31.15.176:8080/github-webhook/
```

6. Configure the webhook to trigger on **push events**.
7. Click **Add webhook** to save it.

In Jenkins Job 1, the following build trigger was also enabled:

```text
GitHub hook trigger for GITScm polling
```
## 4. JOBS 
### job 1 
<img width="2376" height="5329" alt="image" src="https://github.com/user-attachments/assets/d188adde-6987-4a7e-a5cb-2d2a75e7777a" />
### job 2 
<img width="2376" height="6121" alt="image" src="https://github.com/user-attachments/assets/84e2efa6-3d2b-4617-bcf6-a631af3999fb" />
### job 3 
<img width="2376" height="6208" alt="image" src="https://github.com/user-attachments/assets/ccb3421a-c4d2-40bc-b615-4a035ecbcb30" />


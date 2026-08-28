# 🚀 Ansible Automated Web Application Deployment

<p align="center">
  <img src="https://img.shields.io/badge/Ansible-Automation-red?style=for-the-badge&logo=ansible" alt="Ansible">
  <img src="https://img.shields.io/badge/AWS-Secrets%20Manager-orange?style=for-the-badge&logo=amazonaws" alt="AWS">
  <img src="https://img.shields.io/badge/GitHub-Actions-black?style=for-the-badge&logo=githubactions" alt="GitHub Actions">
  <img src="https://img.shields.io/badge/Apache-HTTPD-red?style=for-the-badge&logo=apache" alt="Apache">
  <img src="https://img.shields.io/badge/PHP-FPM-777BB4?style=for-the-badge&logo=php" alt="PHP">
</p>

<p align="center">
  <b>Automated • Secure • Repeatable • Version Controlled Deployment</b>
</p>

---

## 📌 Overview

This project provides a **secure and automated web application deployment solution** using **Ansible, GitHub Actions, AWS Secrets Manager, and Ansible Vault**.

The infrastructure and application deployment are automated through Ansible, while sensitive configuration values are protected using **Ansible Vault**.

The Ansible Vault password is securely retrieved from **AWS Secrets Manager** during deployment, preventing sensitive credentials from being stored directly inside the Git repository.

### 🎯 What this project achieves

```text
Developer
    │
    │ Git Push
    ▼
┌─────────────────────┐
│   GitHub Repository │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   GitHub Actions    │
│      CI/CD          │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Ansible Control Node│
└──────────┬──────────┘
           │
     ┌─────┴─────┐
     │           │
     ▼           ▼
┌─────────┐ ┌──────────────┐
│ AWS     │ │ Web Server   │
│ Secrets │ │              │
│ Manager │ │ Apache       │
└─────────┘ │ PHP-FPM      │
            │ Application  │
            └──────────────┘
```

---

# ✨ Features

| Feature                    | Description                                            |
| -------------------------- | ------------------------------------------------------ |
| 🤖 **Ansible Automation**  | Automates server configuration and deployment          |
| 🌐 **Apache HTTPD**        | Installs and configures Apache                         |
| 🐘 **PHP-FPM**             | Installs and configures PHP-FPM                        |
| 📦 **Git Deployment**      | Fetches the required application version from Git      |
| 🔐 **Ansible Vault**       | Encrypts sensitive configuration                       |
| ☁️ **AWS Secrets Manager** | Securely stores the Vault password                     |
| 🔄 **GitHub Actions**      | Automates deployment through CI/CD                     |
| 🔁 **Idempotent**          | Can be executed repeatedly without unnecessary changes |
| 🛡️ **Secure**             | Credentials are not stored in plain text               |
| ⚡ **Fast Deployment**      | New application versions can be deployed automatically |

---

# 🏗️ Architecture

```text
                         ┌──────────────────────┐
                         │      Developer       │
                         └──────────┬───────────┘
                                    │
                              git push
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   GitHub Repository  │
                         │                      │
                         │  Application Code    │
                         │  Ansible Playbooks   │
                         │  Roles               │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   GitHub Actions     │
                         │                      │
                         │  CI/CD Pipeline      │
                         └──────────┬───────────┘
                                    │
                                    ▼
                     ┌────────────────────────────┐
                     │    Ansible Control Node    │
                     │                            │
                     │    ansible-playbook        │
                     └─────────────┬──────────────┘
                                   │
                    ┌──────────────┴──────────────┐
                    │                             │
                    ▼                             ▼
          ┌──────────────────┐          ┌──────────────────┐
          │ AWS Secrets      │          │ Remote Web Server│
          │ Manager          │          │                  │
          │                  │          │ Apache HTTPD     │
          │ Vault Password   │          │ PHP-FPM           │
          └──────────────────┘          │ Application      │
                                        └──────────────────┘
```

---

# 📂 Project Structure

```text
ansible-deployment/
│
├── 📁 .github/
│   └── 📁 workflows/
│       └── 🚀 deploy.yml
│
├── 📁 inventory/
│   └── 🖥️ hosts
│
├── 📁 group_vars/
│   └── 📁 all/
│       ├── ⚙️ variables.yml
│       └── 🔐 vault.yml
│
├── 📁 roles/
│   │
│   ├── 📁 apache/
│   │   ├── 📁 tasks/
│   │   │   └── main.yml
│   │   ├── 📁 templates/
│   │   │   └── vhost.conf.j2
│   │   └── 📁 handlers/
│   │       └── main.yml
│   │
│   ├── 📁 php/
│   │   ├── 📁 tasks/
│   │   │   └── main.yml
│   │   └── 📁 templates/
│   │       └── www.conf.j2
│   │
│   └── 📁 application/
│       ├── 📁 tasks/
│       │   └── main.yml
│       └── 📁 templates/
│
├── 📄 playbook.yml
├── 📄 requirements.yml
└── 📖 README.md
```

---

# ⚙️ Deployment Process

The deployment follows this flow:

```text
1️⃣ Developer pushes code
          ↓
2️⃣ GitHub Actions starts
          ↓
3️⃣ Ansible environment is prepared
          ↓
4️⃣ AWS Secrets Manager is queried
          ↓
5️⃣ Ansible Vault password is retrieved
          ↓
6️⃣ Ansible Playbook starts
          ↓
7️⃣ Apache HTTPD is installed/configured
          ↓
8️⃣ PHP-FPM is installed/configured
          ↓
9️⃣ Application source is fetched from Git
          ↓
🔟 Permissions/configuration are applied
          ↓
🚀 Application deployment completed
```

---

# 🧰 Technology Stack

```text
┌─────────────────────────────────────┐
│           DevOps Stack              │
├─────────────────────────────────────┤
│                                     │
│  🐧 Linux                           │
│  🔴 Ansible                         │
│  🌐 Apache HTTPD                    │
│  🐘 PHP-FPM                         │
│  🐙 Git                             │
│  ☁️ AWS Secrets Manager             │
│  🔐 Ansible Vault                   │
│  ⚙️ GitHub Actions                  │
│                                     │
└─────────────────────────────────────┘
```

---

# 🔴 Ansible

Ansible is responsible for the complete server configuration and application deployment.

Example:

```yaml
---
- name: Deploy Web Application
  hosts: webservers
  become: true

  roles:
    - apache
    - php
    - application
```

Run manually:

```bash
ansible-playbook \
  -i inventory/hosts \
  playbook.yml
```

---

# 🌐 Apache HTTPD

The Apache role performs:

```text
✔ Install Apache
✔ Enable Apache
✔ Start Apache
✔ Configure VirtualHost
✔ Configure DocumentRoot
✔ Configure PHP-FPM integration
✔ Configure access/error logs
✔ Restart Apache when configuration changes
```

Example:

```yaml
- name: Install Apache
  package:
    name: httpd
    state: present

- name: Enable and start Apache
  service:
    name: httpd
    state: started
    enabled: true
```

---

# 🐘 PHP-FPM

PHP-FPM is installed and enabled automatically.

Example packages:

```yaml
php
php-fpm
php-cli
php-mysqlnd
php-json
php-mbstring
php-xml
```

The Apache configuration connects PHP requests to PHP-FPM through the configured FPM socket.

---

# 📦 Application Deployment

The application source is fetched from Git using Ansible's `git` module.

Example:

```yaml
- name: Fetch application source
  git:
    repo: "{{ git_repository }}"
    dest: "{{ app_root }}"
    version: "{{ git_branch }}"
    update: true
    force: true
```

Variables:

```yaml
app_name: myapp
app_root: /var/www/myapp

git_repository: "git@github.com:organization/application.git"
git_branch: main

app_domain: example.com
```

### 🔄 New Deployment

When a new version is pushed to the application repository:

```text
Git Push
   ↓
GitHub Actions
   ↓
Ansible
   ↓
Git Update
   ↓
Application Updated
```

This allows the same deployment process to be executed consistently every time.

---

# 🔐 Security

Security is an important part of this project.

Sensitive values are **never stored as plain text** in the Git repository.

### ❌ Avoid

```yaml
db_password: MyPassword123
api_key: abc123
```

### ✅ Use Ansible Vault

```bash
ansible-vault create group_vars/all/vault.yml
```

Sensitive variables can then be stored inside the encrypted file.

Example:

```yaml
db_username: application_user
db_password: very-secret-password
api_key: very-secret-api-key
```

The resulting file is encrypted and can safely be committed to the repository.

---

# ☁️ AWS Secrets Manager

The **Ansible Vault password** is stored in AWS Secrets Manager.

Example secret:

```text
ansible/vault/password
```

Retrieve the secret:

```bash
aws secretsmanager get-secret-value \
  --secret-id ansible/vault/password \
  --query SecretString \
  --output text
```

The deployment IAM identity requires permission similar to:

```json
{
  "Effect": "Allow",
  "Action": [
    "secretsmanager:GetSecretValue"
  ],
  "Resource": "arn:aws:secretsmanager:REGION:ACCOUNT_ID:secret:ansible/vault/password-*"
}
```

---

# 🔒 Vault Password Handling

During deployment:

```text
AWS Secrets Manager
        │
        │ GetSecretValue
        ▼
Vault Password
        │
        ▼
Temporary secure file
        │
        ▼
ansible-playbook
        │
        ▼
Encrypted vault.yml
```

Example:

```bash
aws secretsmanager get-secret-value \
  --secret-id ansible/vault/password \
  --query SecretString \
  --output text > /tmp/ansible-vault-password

chmod 600 /tmp/ansible-vault-password
```

Run:

```bash
ansible-playbook \
  -i inventory/hosts \
  playbook.yml \
  --vault-password-file /tmp/ansible-vault-password
```

Clean up:

```bash
rm -f /tmp/ansible-vault-password
```

---

# 🚀 GitHub Actions CI/CD

GitHub Actions can automatically trigger the deployment.

Example workflow:

```yaml
name: 🚀 Ansible Deployment

on:
  push:
    branches:
      - main

  workflow_dispatch:

jobs:

  deploy:

    runs-on: ubuntu-latest

    steps:

      - name: 📥 Checkout Repository
        uses: actions/checkout@v4

      - name: 🔴 Install Ansible
        run: |
          sudo apt update
          sudo apt install -y ansible

      - name: 🔑 Configure SSH
        run: |
          mkdir -p ~/.ssh
          echo "${{ secrets.SSH_PRIVATE_KEY }}" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa

      - name: ☁️ Retrieve Vault Password
        run: |
          aws secretsmanager get-secret-value \
            --secret-id ansible/vault/password \
            --query SecretString \
            --output text > /tmp/vault-password

          chmod 600 /tmp/vault-password

      - name: 🚀 Run Ansible Deployment
        run: |
          ansible-playbook \
            -i inventory/hosts \
            playbook.yml \
            --vault-password-file /tmp/vault-password

      - name: 🧹 Cleanup
        if: always()
        run: |
          rm -f /tmp/vault-password
          rm -f ~/.ssh/id_rsa
```

> **Note:** Configure AWS authentication for GitHub Actions using **OIDC/IAM role assumption** rather than long-lived AWS access keys whenever possible.

---

# 🔄 Continuous Deployment

Once integrated with GitHub Actions:

```text
             Developer
                 │
                 │ git push
                 ▼
        ┌─────────────────┐
        │ GitHub Repository│
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ GitHub Actions  │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │     Ansible     │
        └────────┬────────┘
                 │
          ┌──────┴──────┐
          ▼             ▼
     AWS Secret     Web Server
       Manager          │
                        ▼
                 Apache + PHP-FPM
                        │
                        ▼
                   Application
```

---

# 🧪 Testing

Before deployment, test Ansible connectivity:

```bash
ansible all \
  -i inventory/hosts \
  -m ping
```

Check playbook syntax:

```bash
ansible-playbook \
  -i inventory/hosts \
  playbook.yml \
  --syntax-check
```

Run in check mode:

```bash
ansible-playbook \
  -i inventory/hosts \
  playbook.yml \
  --check
```

Run with verbose output:

```bash
ansible-playbook \
  -i inventory/hosts \
  playbook.yml \
  -vv
```

---

# 🛡️ Security Best Practices

### 🔐 Secrets

* Never commit plaintext passwords.
* Use Ansible Vault for sensitive variables.
* Store the Vault password in AWS Secrets Manager.
* Use IAM roles instead of long-lived AWS credentials.
* Restrict Secrets Manager access using least privilege.

### 🔑 SSH

* Use SSH keys instead of passwords.
* Store private keys in GitHub Secrets.
* Never commit private keys.
* Restrict SSH access using security groups/firewalls.

### 📁 File Permissions

Sensitive files should have restrictive permissions:

```bash
chmod 600 /tmp/vault-password
```

Application ownership should be explicitly configured:

```yaml
owner: "{{ app_user }}"
group: "{{ app_group }}"
```

---

# 📊 Deployment Benefits

| Traditional Deployment          | Automated Deployment    |
| ------------------------------- | ----------------------- |
| ❌ Manual server configuration   | ✅ Automated             |
| ❌ Manual package installation   | ✅ Ansible               |
| ❌ Manual application updates    | ✅ Git deployment        |
| ❌ Passwords in configuration    | ✅ Ansible Vault         |
| ❌ Vault password stored locally | ✅ AWS Secrets Manager   |
| ❌ Manual deployment process     | ✅ GitHub Actions        |
| ❌ Configuration drift           | ✅ Idempotent automation |
| ❌ Difficult to reproduce        | ✅ Repeatable            |

---

# 🚦 Deployment Status

```text
🟢 Infrastructure Automation
🟢 Apache Installation
🟢 PHP-FPM Installation
🟢 Git Application Deployment
🟢 Ansible Vault
🟢 AWS Secrets Manager
🟢 GitHub Actions Integration
🟢 Automated Deployment
```

---

# 👨‍💻 Author

**DevOps / Linux Administration Automation Project**

Built using:

```text
🐧 Linux
🔴 Ansible
☁️ AWS
🐙 Git
⚙️ GitHub Actions
🌐 Apache
🐘 PHP-FPM
```

---

# ⭐ Contributing

Contributions, improvements, and suggestions are welcome.

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test the Ansible playbook
5. Create a Pull Request

---

# 📜 License

This project is intended for learning, automation, DevOps practice, and production deployment workflows.

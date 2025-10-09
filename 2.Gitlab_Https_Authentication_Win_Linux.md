# **GitLab HTTPS authentication** on both **Windows** and **Linux**

## ⚙️ Overview

When using **HTTPS authentication** with GitLab, you authenticate via:

* **Personal Access Token (PAT)** instead of your password (since GitLab deprecated password auth for Git over HTTPS).
* The token acts as your “password” when you clone, pull, or push repositories.

---

## 🪟 1️⃣ Windows: HTTPS Authentication Setup

### **Step 1: Generate a Personal Access Token (PAT)**

1. Log in to your GitLab account.
2. Go to **User Profile → Preferences → Access Tokens** or visit
   👉 `https://gitlab.com/-/user_settings/personal_access_tokens`
3. Give it a **name**, **expiry date**, and **select scopes**:

   * ✅ `read_repository`
   * ✅ `write_repository`
4. Click **Create personal access token**.
5. Copy the token — you’ll only see it once!

---

### **Step 2: Configure Git**

Open **Git Bash** or **PowerShell** and run:

```bash
git config --global user.name "Deepak"
git config --global user.email "your_email@example.com"
```

---

### **Step 3: Clone Repository Using HTTPS**

Example:

```bash
git clone https://gitlab.com/username/repository.git
```

When prompted for credentials:

* **Username:** your GitLab username or email
* **Password:** your Personal Access Token (PAT)

---

### **Step 4: Save Credentials Securely**

To avoid entering credentials every time:

```bash
git config --global credential.helper manager
```

This uses the **Windows Credential Manager** to store them securely.

---

### **Step 5: Verify Authentication**

You can test by pushing:

```bash
cd repository
git push origin main
```

If no prompt appears → authentication is cached successfully.

---

### 🔍 Optional: Check or Remove Saved Credentials

To view stored credentials:

* Open **Windows Search → Credential Manager → Windows Credentials**
* Look for entries like `git:https://gitlab.com`
* You can **edit** or **remove** them if needed.

---

## 🐧 2️⃣ Linux: HTTPS Authentication Setup

### **Step 1: Generate PAT**

Same steps as above (use GitLab UI).

---

### **Step 2: Configure Git**

```bash
git config --global user.name "Deepak"
git config --global user.email "your_email@example.com"
```

---

### **Step 3: Clone Using HTTPS**

```bash
git clone https://gitlab.com/username/repository.git
```

When asked:

* **Username:** GitLab username or email
* **Password:** Personal Access Token

---

### **Step 4: Store Credentials Securely**

Option 1️⃣ – Store Temporarily (memory cache)

```bash
git config --global credential.helper cache
```

By default, it caches for 15 minutes.
To increase timeout (e.g., 1 hour):

```bash
git config --global credential.helper 'cache --timeout=3600'
```

Option 2️⃣ – Store Permanently (plain text)

```bash
git config --global credential.helper store
```

Credentials will be saved in `~/.git-credentials` — **not recommended for shared systems**.

Option 3️⃣ – Use Gnome Keyring or libsecret (Recommended for desktops)
Install:

```bash
sudo apt install libsecret-1-0 libsecret-1-dev
cd /usr/share/doc/git/contrib/credential/libsecret
sudo make
git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```

---

### **Step 5: Verify**

Run:

```bash
git pull
git push
```

If it doesn’t ask for a password, credentials are cached/stored correctly.

---

## ✅ 3️⃣ Verify Global Config

To confirm settings on either OS:

```bash
git config --global --list
```

You should see:

```
user.name=Deepak
user.email=your_email@example.com
credential.helper=manager   # (Windows)
credential.helper=libsecret # (Linux)
```

---

## ⚠️ Common Issues & Fixes

| Issue                        | Cause                               | Fix                                 |
| ---------------------------- | ----------------------------------- | ----------------------------------- |
| `Authentication failed`      | Using old password instead of token | Use PAT as password                 |
| Keeps asking for credentials | Credential helper not set           | Set helper (`manager` or `cache`)   |
| Wrong token scope            | Missing `write_repository`          | Regenerate token with proper scopes |
| Token expired                | Expiry date reached                 | Generate new PAT                    |

---

Would you like me to also include **how to update an existing Git remote URL** from SSH → HTTPS or from one GitLab server to another (e.g., `jfrog` → `harbor`)?

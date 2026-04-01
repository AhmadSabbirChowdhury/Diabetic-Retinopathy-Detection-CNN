# 🚀 Complete Guide: Uploading Your Project to GitHub

> A step-by-step guide for Ahmad — from zero to a live GitHub repo.

---

## Before You Start — What You Need

- A GitHub account (yours: https://github.com/AhmadSabbirChowdhury)
- Git installed on your computer ([download here](https://git-scm.com/downloads))
- Your project files ready on your computer

---

## STEP 1: Create the Repository on GitHub

1. Go to **https://github.com/new**
2. Fill in the details:
   - **Repository name:** `Diabetic-Retinopathy-Detection-CNN`
   - **Description:** `Automated Diabetic Retinopathy detection from fundus images using custom-built CNN — Multiclass (74% acc) & Binary (95% acc) classification on APTOS 2019 dataset`
   - **Visibility:** Public
   - **Do NOT** check "Add a README file" (we already have one)
   - **Do NOT** check "Add .gitignore" (we already have one)
   - Optionally select **MIT License**
3. Click **"Create repository"**

> After creation, GitHub will show you instructions — keep that page open.

---

## STEP 2: Organize Your Project Folder Locally

On your computer, create a folder structure like this. You can do it manually or use the terminal commands below:

```
Diabetic-Retinopathy-Detection-CNN/
│
├── README.md                                ← (the file I created for you)
├── requirements.txt                         ← (the file I created for you)
├── .gitignore                               ← (the file I created for you)
│
├── notebooks/
│   └── DR_Detection.ipynb                   ← YOUR Jupyter notebook
│
├── docs/
│   ├── PaperSubmission_Ahmad.doc            ← YOUR research paper
│   └── Ahmad_ProjectPresentationPPT.pptx    ← YOUR presentation
│
├── images/                                  ← (the images folder I created)
│   ├── fundus_samples_unscaled.png
│   ├── fundus_samples_rescaled.png
│   ├── image_augmentation.png
│   ├── project_flowchart.jpg
│   ├── cnn_architecture.jpg
│   ├── model_summary.jpg
│   ├── multiclass_accuracy_plot.png
│   ├── multiclass_loss_plot.png
│   ├── multiclass_confusion_matrix.png
│   ├── binary_accuracy_plot.png
│   ├── binary_loss_plot.png
│   └── binary_confusion_matrix.png
│
└── models/                                  ← (optional: saved .h5 model files)
    └── best_model.h5
```

### Terminal commands to set this up:

```bash
# Create the project folder
mkdir Diabetic-Retinopathy-Detection-CNN
cd Diabetic-Retinopathy-Detection-CNN

# Create subdirectories
mkdir notebooks docs images models
```

Then copy/move the files I gave you (README.md, requirements.txt, .gitignore, and the images/ folder) into this directory. Also copy your own notebook, paper, and PPT into the appropriate subfolders.

---

## STEP 3: Initialize Git and Make Your First Commit

Open a terminal/command prompt, navigate to your project folder, and run:

```bash
# Navigate to your project folder
cd Diabetic-Retinopathy-Detection-CNN

# Initialize a new Git repository
git init

# Add ALL files to staging
git add .

# Check what's being tracked (optional but recommended)
git status

# Make your first commit
git commit -m "Initial commit: DR Detection CNN with multiclass and binary classification"
```

---

## STEP 4: Connect to GitHub and Push

```bash
# Set the main branch name
git branch -M main

# Connect your local repo to the GitHub remote
git remote add origin https://github.com/AhmadSabbirChowdhury/Diabetic-Retinopathy-Detection-CNN.git

# Push your code to GitHub
git push -u origin main
```

> **First time pushing?** Git will ask you to authenticate. You can use:
> - **GitHub CLI:** Run `gh auth login` and follow the prompts
> - **Personal Access Token:** Go to GitHub → Settings → Developer Settings → Personal Access Tokens → Generate New Token. Use this token as your password when Git asks.
> - **SSH Key** (recommended for long-term): See the SSH setup section below.

---

## STEP 5: Verify on GitHub

1. Go to `https://github.com/AhmadSabbirChowdhury/Diabetic-Retinopathy-Detection-CNN`
2. You should see all your files and folders
3. Scroll down — your README.md should render beautifully with all images, tables, and badges
4. Click through the folders to make sure everything is there

---

## 🔐 Setting Up SSH (One-Time Setup — Recommended)

SSH keys let you push/pull without entering your password every time.

```bash
# 1. Generate an SSH key
ssh-keygen -t ed25519 -C "0304974c@acadiau.ca"
# Press Enter to accept default file location, then set a passphrase (or leave blank)

# 2. Start the SSH agent
eval "$(ssh-agent -s)"

# 3. Add your key
ssh-add ~/.ssh/id_ed25519

# 4. Copy the public key to clipboard
#    On Mac:
cat ~/.ssh/id_ed25519.pub | pbcopy
#    On Windows (Git Bash):
cat ~/.ssh/id_ed25519.pub | clip
#    On Linux:
cat ~/.ssh/id_ed25519.pub
# (then manually copy the output)

# 5. Add to GitHub:
#    Go to GitHub → Settings → SSH and GPG Keys → New SSH Key
#    Paste your key and save

# 6. Test the connection
ssh -T git@github.com
# You should see: "Hi AhmadSabbirChowdhury! You've successfully authenticated..."

# 7. Switch your repo remote to SSH (optional, for future pushes)
git remote set-url origin git@github.com:AhmadSabbirChowdhury/Diabetic-Retinopathy-Detection-CNN.git
```

---

## 📝 Making Future Updates

Whenever you update your code, notebook, or any file:

```bash
# See what changed
git status

# Stage specific files
git add notebooks/DR_Detection.ipynb
# Or stage everything
git add .

# Commit with a descriptive message
git commit -m "Updated model: added dropout layer to reduce overfitting"

# Push to GitHub
git push
```

### Writing Good Commit Messages

Good commit messages help you (and others) understand your project history:

```
✅ "Add binary classification confusion matrix to results"
✅ "Fix image augmentation parameters for better generalization"
✅ "Update README with AUC-ROC score for binary model"

❌ "update"
❌ "fix stuff"
❌ "asdfgh"
```

---

## ⚠️ Common Issues and Fixes

### "File too large" error
GitHub has a 100MB file size limit. If your .h5 model file or dataset is too large:
```bash
# Option 1: Add it to .gitignore
echo "models/best_model.h5" >> .gitignore

# Option 2: Use Git LFS (Large File Storage)
git lfs install
git lfs track "*.h5"
git add .gitattributes
```

### "Permission denied" error
This usually means authentication isn't set up:
```bash
# Check your remote URL
git remote -v

# If using HTTPS, switch to SSH
git remote set-url origin git@github.com:AhmadSabbirChowdhury/Diabetic-Retinopathy-Detection-CNN.git
```

### "Updates were rejected" error
Someone (or you from the web) pushed changes you don't have locally:
```bash
git pull --rebase origin main
git push
```

### Accidentally committed the wrong file
```bash
# Remove from Git but keep locally
git rm --cached path/to/file
git commit -m "Remove accidentally committed file"
git push
```

---

## 🎯 Quick Reference Cheat Sheet

| Action | Command |
|:---|:---|
| Initialize repo | `git init` |
| Check status | `git status` |
| Stage all files | `git add .` |
| Stage specific file | `git add filename` |
| Commit | `git commit -m "message"` |
| Push to GitHub | `git push` |
| Pull latest changes | `git pull` |
| View commit history | `git log --oneline` |
| Create a branch | `git checkout -b branch-name` |
| Switch branch | `git checkout branch-name` |
| Merge branch | `git merge branch-name` |

---

**You're all set! Once you push, your project will be live at:**
**https://github.com/AhmadSabbirChowdhury/Diabetic-Retinopathy-Detection-CNN** 🎉

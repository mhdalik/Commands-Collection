# Commands-Collection


## Python

Create virtual environment (run inside project root directory)(in windows git bash)

    python -m venv venv

Activate venv (in windows git bash)

    source venv/Scripts/activate

Generate requirements.tx

    pip freeze > requirements.txt

Install requirements.tx

    pip install -r requirements.txt




## Linux    

Remove all directories and files excluding hidden items

    rm -rf *
Remove all directories and files including hidden items

    rm -rf ./* .[^.] .??*

Unzip

    unzip dist.zip -d .

Move

    mv dist/* .


Git: Unlink remote repository from local project, also can use this command as undo of `git init` command

    rm -rf .git


Git: reset all changes in local

    git reset --hard 


Open current directory in VSCode when click on .bat fil in windows

save the below code ad .bat file extension in directory that need to open

    @echo off
    code . 








# Steps To Add Private Git repository to hostinger server

### Step 1: Generate an SSH Key Pair for Each Project

1. SSH into your Hostinger server:

    ```ssh username@your-hostinger-domain```
   
   Replace username and your-hostinger-domain with your actual SSH username and server address.
3. Navigate to the specific project folder:

    ```cd ~/domains/abc.com```
   (Adjust the folder path accordingly.)
   
5. Create a new SSH key pair for the project:

   ```ssh-keygen -t rsa -b 4096 -C "your-email@example.com"```

   When prompted for a location, save the key inside your project folder:

   ```Enter file in which to save the key (/home/username/.ssh/id_rsa): /home/username/domains/abc.com/deploy_key```

   When asked for a passphrase, leave it empty (so automated deploys won’t need manual password input).
7. This generates two files:
   - deploy_key: The private key.
   - deploy_key.pub: The public key.

### Step 2: Add the Deploy Key to Your GitHub Repository

1. Open the deploy_key.pub file and copy its contents:

    ```cat ~/domains/abc.com/deploy_key.pub```
3. In your GitHub repository, go to Settings > Deploy Keys > Add Deploy Key, paste the contents of deploy_key.pub into the Key field, check Allow write access if needed, and click Add Key.


### Step 3: Configure the Git Repository on Hostinger
1. Navigate to your project’s public_html folder:

    ```cd ~/domains/abc.com/public_html```
3. Initialize a Git repository if it isn’t already:

    ```git init```
4. Add your private key to SSH for Git access:

    ```eval $(ssh-agent -s)```

    ```ssh-add ~/domains/abc.com/deploy_key```
5. Clone your private repository:

   ```git clone git@github.com:your-username/your-private-repo.git .```

   Or

   ```git pull```
   
    The . ensures the contents are directly placed inside public_html instead of creating an additional folder.

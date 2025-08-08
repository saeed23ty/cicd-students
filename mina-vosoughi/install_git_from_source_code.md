## Install a Specific Git Version from Source Code
This guide shows how to install **a specific Git version** from **source code** on **Rocky Linux** step-by-step.

### Step 1: Update the DNF package information index
This ensures all package metadata is up-to-date and avoids version mismatches:
```bash
sudo dnf update
```

### Step 2: Install required packages
Install build tools and libraries needed to compile Git from source:
```bash
sudo dnf install gettext-devel openssl-devel perl-CPAN perl-devel zlib-devel gcc autoconf libcurl-devel expat-devel wget tar -y
```    
 
### Step 3: Download Git specific version source code   
Visit the *[`Git archives page`](https://www.kernel.org/pub/software/scm/git/)* and download the specific version archive using wget. For example: *[`https://www.kernel.org/pub/software/scm/git/git-2.46.0.tar.gz`](https://www.kernel.org/pub/software/scm/git/git-2.46.0.tar.gz)*
```bash
wget https://www.kernel.org/pub/software/scm/git/git-2.46.0.tar.gz
```

### Step 4: Extract all files from the downloaded archive
```bash 
tar -xvf git-2.46.0.tar.gz
cd git-2.46.0
```  
### Step5: Compile and install Git 
This builds the Git binaries and tools under the /usr prefix that installs Git directly into /usr/bin, which is already in your $PATH by default:
```bash
sudo make prefix=/usr all
sudo make prefix=/usr install
```
### Step6: Enter a new shell to apply the Git package information changes
```bash 
bash
```
### Step7: Verify Git
```bash
git --version
```
Your updated Git version should appear like the one below:
```
git version 2.46.0
```

---
title: Hosting Website on Github for free!
date: 2024-04-03 12:42 +500
categories: [homelab, website, documentation]
tags: [github,documentation]
---

# Saving documents with Github and Gitlab.

## Step 1: Installing VS codium and static website generator Jekyll with Chirpy theme


```bash
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg \
    | gpg --dearmor \
    | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg

echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' \
    | sudo tee /etc/apt/sources.list.d/vscodium.list
deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main

sudo apt update && sudo apt install codium && sudo apt upgrade -y
```

```bash
sudo apt install ruby-full build-essential zlib1g-dev git
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
gem install jekyll bundler
```

## Step 2: Installing vscodium for editing and publishing directly via CI/CD pipelines
> I installed VSCodium via apt but you can pick your poison. 
{: .prompt-tip }
#### Step 2.1: Within vscodium install Github Actions and Codeium AI


## Step 3: Creating a site based on Chirpy Starter

Visit https://github.com/cotes2020/jekyll-theme-chirpy#quick-start

After creating a site based on the template, clone your repo within your computer or local machine you are working on

```bash
https://github.com/YOURUSERNAME/YOURREPO.github.io.git
```

After this install dependencies

```bash
cd YOURREPO
bundle
```

Make changes to the site - commit - push to github or gitlab. Process is same for both.

```bash
git add .
git commit -m "made some changes"
git push
```

If you want to see demo of your website locally either you can see within vscode preview window on upper right corner or you can use Jekyll command to show via localhost.

```bash
bundle exec jekyll s
```

## Step 4: Making your first Post on your website

To create a post, add a file to your **_posts** directory with the following format:

~~~
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.md
~~~

~~~
---
title: Hosting Website on Github for free!
date: 2024-03-29 13:31 +500
categories: [homelab, website, documentation]
tags: [github,documentation]
---

# Welcome
**Hello World**
~~~

Reference here:-
* https://jekyllrb.com/docs/posts/
* https://chirpy.cotes.page/posts/ write-a-new-post/
* https://technotim.live/posts/jekyll-docs-site/

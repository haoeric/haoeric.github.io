---
layout: post
title: Setup Kekyll to Host your Personal Website on AWS S3
comments: true
categories: [Skills]
tags: [jekyll, website, aws, s3, s3_website]
---


### Install Jekyll

```bash
## install homebrew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

## install a separate version of Ruby
brew install ruby

## add new ruby to your ENV PATH
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
## For compilers to find ruby you may need to set:
export LDFLAGS="-L/usr/local/opt/ruby/lib"
export CPPFLAGS="-I/usr/local/opt/ruby/include"

## install jekyll
gem install bundler jekyll
bundle update --bundler
```

### Build and Host your Website

```bash
## build your website
jekyll new my-website
cd my-website

## host your website
bundle exec jekyll serve
```

### Host your Website on AWS S3

with [s3_website](https://github.com/laurilehmijoki/s3_website), you can easily get your jekyll website deployed on AWS S3:

- Run `gem install s3_website` to install `s3_website`

- Create IAM credentials that have sufficient permissions to S3.

- Go to your website directory.

- Run `s3_website cfg create`. This generates a configuration file called `s3_website.yml`.

- Put your AWS credentials and the S3 bucket name into the file

- Run `s3_website cfg apply`. This will configure your bucket to function as an S3 website. If the bucket does not exist, the command will create it for you.

- Run `s3_website push` to push your website to S3. Congratulations! You are live.

At any later time when you would like to synchronise your local website with the S3 website, simply run `s3_website push` again. (It will calculate the difference, update the changed files, upload the new files and delete the obsolete files.)


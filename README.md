# remocle.com


## Install bundler (can skip if already installed)

Recommend using `gem install --user-install ...` instead of using `sudo gem install ...`, 
to minimize root permission issue.

    gem install --user-install bundler

    echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.bash_profile

## Install dependencies from Gemfile

    bundle install

Now you can run command with `bundle exec {command}` when {command} is defined and installed by Gemfile.
(github-pages gem already has dependency to jekyll.)

## Run local server

    bundle exec jekyll serve

## Deploy to github-pages

Just push changes to master branch.
(jekyll installation at github will generate the _site for you automatically upon push)

## Domain setup

Use github pages's custom domain config. Cloudflare is required only for the www to non-www redirection explained in
following section.

### www to non-www(apex) domain redirection with https

Use cloudflare dashboard

- Enable Cloudflare 'proxy' on CNAME record with 'www'. Otherwise, www won't be redirected to apex domain due to the
  cert error when connecting to https://www.remocle.com
  (Because github pages only issued cert for `remocle.com`, which is defined in the github pages configuration)

- Leave other A record as 'DNS only' (github pages already use AWS cloudfront CDN. Therefore, applying Cloudflare proxy
  will be the unnecessary cache duplicates)

- Add 'alway use https' option on Page Rules.

## Keep up-to-date Jekyll version

If the github-pages gem on your computer is out of date with the github-pages gem on the GitHub Pages server,
your site may look different when built locally than when published on GitHub.
To avoid this, regularly update the github-pages gem on your computer.

bundle update github-pages


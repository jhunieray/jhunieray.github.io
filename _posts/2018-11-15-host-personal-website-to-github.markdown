---
layout: post
title:  "Host Personal Website to Github"
date:   2018-11-15 20:39:58 +0800
categories: jekyll update
---
I have just finished building my personal website using **Jekyll + GitHub + Cloudflare**. I must say this is really a fantastic setup! I have multiple reasons for that:

* GitHub Pages are free.
* Thanks to Cloudflare we get free HTTPS and caching support + Security.
* Speed: static websites are fast and practically maintainence free
* Ease of development: jekyll & git makes development very convenient.

There are multiple nice themes available, I have settled for Beautiful Jekyll which is very simple to set up and looks great.

### Github Pages

First, head over to [GitHub](https://github.com) and create a new repository named **username.github.io**, where username is your username (or organization name) on GitHub. If the first part of the repository doesn’t exactly match your username, it won’t work, so make sure to get it right. Then, go to the folder where you want to store your project, and clone the new repository:

{% highlight terminal %}
git clone https://github.com/username/username.github.io
{% endhighlight %}

Next, enter the project folder. Before we install [Jekyll](https://jekyllrb.com), we need to make sure we have all the required dependencies.

{% highlight terminal %}
sudo apt-get install ruby ruby-dev build-essential
{% endhighlight %}

It is best to avoid installing Ruby Gems as the root user. Therefore, we need to set up a gem installation directory for your user account. The following commands will add environment variables to your *~/.bashrc* file to configure the gem installation path. Run them now:

{% highlight terminal %}
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
{% endhighlight %}

Finally, install Jekyll:

{% highlight terminal %}
gem install jekyll bundler
{% endhighlight %}

That’s it! Jekyll installed. Now add, commit, and push your changes:

{% highlight terminal %}
git add --all
git commit -m "Initial commit"
git push -u origin master
{% endhighlight %}

…and you're done!
Fire up a browser and go to ***https://username.github.io***.

If you want to use custom domain and SSL from Cloudflare, continue below.

### Domain Configuration 

I have a domain [suarez.rocks](https://suarez.rocks) purchased from [GoDaddy](https://godaddy.com). Login to your domain provider and go to Nameservers in the DNS Management page. Change the nameservers to: 
{% highlight terminal %}
jo.ns.cloudflare.com
{% endhighlight %}
{% highlight terminal %}
rick.ns.cloudflare.com
{% endhighlight %}

It will take up to 24 hours max of propagation.

### Cloudflare Configuration

Now login to your [Cloudflare account](https://cloudflare.com). Click *Add a Site* and input your domain, select free plan and click next until you came with the DNS Records Page. Now add four "A" Records: 
{% highlight terminal %}
185.199.108.153
{% endhighlight %}
{% highlight terminal %}
185.199.109.153
{% endhighlight %}
{% highlight terminal %}
185.199.110.153
{% endhighlight %}
{% highlight terminal %}
185.199.111.153
{% endhighlight %}

This will point you to Github's DNS. Now in the tab *Crypto*, go to the setting named **Always Use HTTPS** and toggle to **ON**. It may take up to 24 hours after the site becomes active on Cloudflare for new certificates to issue.

That’s it! You have now secured personal static website.

---
layout: post
title:  "Create your personal blog for free with Github"
date:   2017-10-21 14:13:53 +0200
categories: development
comments: true
lang: en
ref: githubpages
---

You can have your own personal website for free without having to pay any hosting services monthly or annualy. The blog that you are reading the content is hosted in github pages. 

Create a Github account 
----------------------------
The first thing that I had to do was to have a github account. <a href="https://github.com/">Github</a> has become a big community of developers that share their code with other people for free, it's a social network for developers and all the people that want to become involved in the world of software development. But even if you are not a developer you can take advantage of it and create a blog like the one that you are reading.

Fork a repository
----------------------------
Once you have created a Github account you have to <a href="https://en.wikipedia.org/wiki/Fork_(software_development)">fork</a> a repository. Fork a repository means to create a copy of a project that somebody else has created before and you want to continue from the point that this person is working at that moment. 

Is like if you want to continue a book that another person has started, you create a copy of his book and you start to write your own chapters. At this moment you become the writer of a new book based on the original book. You can modify a chapter that the original author has written, add more chapters or delete one that you don't like. It's up to you.

I forked <a href="https://github.com/barryclark/jekyll-now">jekyll-now</a> repository and I started my own blog website. I continued from this repository because it has things that help me the creation of the blog like some useful html pages in the include folder like google analytics `analytics.html`, `disqus.html` and `meta.html`. 

Adding content to your blog
-----------------------------
When talking about <a href="https://en.wikipedia.org/wiki/Commit_(version_control)">committing</a> it is like writting something into your new book. You write a section or a chapter and then you commit to it and you want to publish in your repository. 

When a developer commits code he is writing a chapter, section of his book. A good practise is to commit something meaningful for other people that will be able to see what you have commited. They should be able to understand your changes without asking you what have you written. Another helpful thing of a commit is to write a good comment of the commit, with the purpose of the changes that you are uploading to to your book. At the end of the chapter book if you have done meaningful commits you will have a comprehensive list of changes that will talk by themselves.   

If you don't want to download the repository and do the job in your computer without installing anything you can do it committing directly to github. You will end up with a lot of commits but you don't have to configure nothing extra in your computer (I prefer to do it locally first because this way I can see how everything fits, specially if you want to add some resources like images, and also you have less commits in your repository).

Urls of your new blog
-----------------------------
After forking the repository I had it created in <a href="https://github.com/alexmanrique/blog">https://github.com/alexmanrique/blog</a> and also ready and available to read for people in <a href="https://alexmanrique.github.io/blog">https://alexmanrique.github.io/blog</a> where you are able to access to blog index with a list of posts. Adding a new post to your blog is as easy as adding a new file in the `_posts` directory of your new repository. You should customize other things like your links to other websites and your `about` section where you present yourself to your readers. 

Bonus - Changing the url of your blog
-------------------------------
After forking the repository I had access to it in <a href="https://alexmanrique.github.io/blog">https://alexmanrique.github.io/blog</a> but I wanted that my blog appeared in <a href="http://www.alexmanrique.com/blog">http://www.alexmanrique.com/blog</a> because I have my resume in this domain and I wanted to group everything in the same place. 

Then what I did was to add a <a href="https://github.com/alexmanrique/blog/blob/master/CNAME">CNAME</a> file in the root directory of my project with `www.alexmanrique.com` and also change the property `base_url:""` to `base_url:/blog` in the `_config.yml` configuration file. This way, everytime that I access to <a href="https://alexmanrique.github.io/blog">https://alexmanrique.github.io/blog</a> it redirects me to <a href="http://www.alexmanrique.com/blog">http://www.alexmanrique.com/blog</a>

Conclusion
--------------------------
It's not really difficult to start your own blog if you know the tools to do it. You don't have to pay to have it up and running and you can add content to it simply by adding content to the an specific folder of a repository created in Github continuing "the book" that another person has started before you.
If you need help creating your blog send me an <a href="contact@alexmanrique.com">email</a> or contact me in twitter at <a href="https://twitter.com/amanrique">https://twitter.com/amanrique</a>






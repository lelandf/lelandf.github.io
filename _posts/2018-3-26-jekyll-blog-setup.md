---
layout: post
title: Setting up a Jekyll blog
---

I've always wanted to set up a Jekyll-powered blog, and tonight I did it.

Jekyll is a static site generator, so it's a departure from the database-driven sites I'm used to building.

For now, I'm hosting on GitHub Pages with a brand new .blog domain.

Here's how I did it:

## Install Jekyll locally
While this isn't required to get started if you plan on using GitHub Pages, you might as well install Jekyll locally anyway.

I'm a macOS user, so I followed the [Linux/Unix/macOS installation guide](https://jekyllrb.com/docs/installation/).

You will need Ruby installed first. You can confirm you have Ruby installed by typing "ruby -v" in Terminal.

If you don't, you can do this:

1. Install [Homebrew](https://brew.sh/)
2. Run "brew install ruby"
3. Run "ruby -v" again to confirm

After Ruby is installed, install the github-pages gem with `gem install github-pages`.

Since GitHub Pages is powered by Jekyll, this gem will install Jekyll along with a few other things that will come in handy with GitHub Pages.

There's a [guide for Windows users](https://jekyllrb.com/docs/windows/) as well.

Now that we have Jekyll installed, we can build a site locally.

## Fork a starter project
You're going to end up wasting time trying to start a Jekyll-powered blog "from scratch" so I looked around for a starter project to fork.

I ended up settling on [Jekyll Now](https://github.com/barryclark/jekyll-now) and cloned it locally.

```
mkdir blog
cd blog
git clone https://github.com/barryclark/jekyll-now.git
rm -rf .git
```

At this point, you should be able to run `jekyll serve` and have a Jekyll site running locally at `127.0.0.1:4000`.

You should also open up another Terminal tab to run `jekyll build --watch` to rebuild your Jekyll site when any file changes.

## Cleaning up Jekyll Now
There are a few things you will want to adjust before your Jekyll Now site is ready for launch.

### Edit config
Open up the `_config.yml` file and edit the following:

### Name of your site
Change "Your Name" to your actual name, or whatever you want your blog to be titled.

### Description of your site
Change "Web Developer from Somewhere" to a more useful description.

### Avatar
I ended up commenting this out, but if you want a logo you should swap this out with the path to something else.

### Social network links
I replaced the GitHub and Twitter references with my own, but you can remove them also.

### Deal with about page
I ended up just deleting this with `rm about.md` because I didn't feel like writing up a new About page for now.

You will need to update your navigation to reflect the now missing About page, but we'll get to that later.

### Deal with images
I decided to empty out the images directory with `rm -rf images` for now.

One of those images is referenced on the 404 page, so remember to delete that reference in `404.md`.

`[<img src="{{ site.baseurl }}/images/404.jpg" alt="Constructocat by https://github.com/jasoncostello" style="width: 400px;"/>]({{ site.baseurl }}/)`

### Adjust template to account for deleted things
I deleted the logo and the About page, but deleting those things doesn't magically remove those references in the template files.

To do that, we'll open `_layouts/default.html` and remove the following lines:

- Line 22: `<a href="{{ site.baseurl }}/" class="site-avatar"><img src="{{ site.avatar }}" /></a>`
- Line 31: `<a href="{{ site.baseurl }}/about">About</a>`

Now that our Jekyll Now site is sufficiently sanitized, we can start actually writing our first post.

## Writing your first post
Jekyll content is written in Markdown.

I was somewhat familiar with Markdown already, but if you aren't, take a quick gander at this [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

You can write plain paragraphs with no Markdown knowledge, but it is useful if you want to incorporate elements like links, headings, images, lists, and code in your writing.

### Peek in the _posts folder
Creating posts is as simple as adding a Markdown file to the _posts directory.

#### How to name your files
In the _posts directory of Jekyll Now, we see a file called `2014-3-3-Hello-World.md`.

This gives us a hint as to how files should be named, and the [Jekyll documentation on posts](https://jekyllrb.com/docs/posts/) fills in the gaps.

An interesting note in the documentation (emphasis mine):

> Where YEAR is a four-digit number, MONTH and DAY are both **two-digit numbers**

While it seems to work anyway, I decided to make my post file names more like this: `2014-03-03-hello-world.md`.

Note the leading zeros for months and days with single digits. And also the lowercase letters.

I noticed that if letters are capitalized in the post slug (i.e. "Hello World") that capitalization will be reflected in the URL after building (i.e. example.com/Hello-World/).

Just a personal preference, but I like lowercase letters in my URLs.

#### How to use YAML Front Matter
Inside the file, you'll notice this text at the top:

```
---
layout: post
title: You're up and running!
---
```

This is known as [YAML Front Matter](https://jekyllrb.com/docs/frontmatter/). Keep the `layout: post` line as-is, and swap out `You're up and running!` with your own post title.

There's more to it than that, but this is all you need to know for now.

## Point your domain to GitHub Pages over HTTPS
If you're happy with a `yourusername.github.io` URL, feel free to stop here.

If you want to use your own domain and have a https://example.com URL, read on.

### Add a CNAME file in your GitHub repo
Make a text file called `CNAME` (no extension or anything) with the domain you want to use.

```
https://fiegel.blog
```

[That's it](https://github.com/lelandf/lelandf.github.io/blob/master/CNAME).

### Point your domain to CloudFlare
Just a free plan will do. We'll be using one of CloudFlare's flexible SSL certifications.

## Still to write about 
- Continue discussing CloudFlare set up
- Page rule in CloudFlare: http://*fiegel.blog/* limited to three: https://hackernoon.com/set-up-ssl-on-github-pages-with-custom-domains-for-free-a576bdf51bc
- You need to name your GitHub repository yourusername.github.io
- End to end encryption. Self hosting?
- Make my own theme
- Find a Disqus alternative
- Explore syntax highlighting
- Find a nice Markdown editor
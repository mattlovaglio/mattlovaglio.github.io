---
layout: post
title: Making Embedded Content Responsive In Jekyll Posts
---

## Using YouTube content in Jekyll posts not mobile responsive

If you're using Jekyll or thinking about using Jekyll for blogging you might want to consider how the content within Jekyll posts are rendered. Both for Markdown and HTML.

On the occasion that you have to throw a line of HTML up in there, you should think about it's default behavior and how your css will affect it's presentation.

Currently, throwing a YouTube iframe in the mix doesn't bode well for mobile devices.

## Default behavior

Things like embedding a YouTube video will require some additional strategy. That is if you're using the iframe method and want the content to be responsive.

If you embed a YouTube video in a Jekyll post, as per the official YouTube instructions, you might notice that on an iPhone (or any mobile device) your embedded content spills out of the viewport. Not desirable. So as you can deduce, this method is not responsive friendly.

**The default YouTube embed instructions might look something like this:**

YouTube video being referenced here:

[DevTips: Getting Started With Jekyll, The Static Site Generator](https://www.youtube.com/watch?v=iWowJBRMtpc)

Basic YouTube embed link for this video:

{% highlight html %}

<iframe width="560" height="315" src="https://www.youtube.com/embed/iWowJBRMtpc" frameborder="0" allowfullscreen></iframe>

{% endhighlight %}

This method doesn't work well.

Lucky for you, it won't take much to fix this behavior.

## Finding a solution

I recently found a solution via [@rachelmccollin](https://twitter.com/rachelmccollin) in a [Smashing Magazine](http://www.smashingmagazine.com) post.

**Here are the article links:**

[Making embedded content work in responsive design](http://www.smashingmagazine.com/2014/02/27/making-embedded-content-work-in-responsive-design/)

[Creating intrinsic ratios for video](http://alistapart.com/article/creating-intrinsic-ratios-for-video)

In the name of not taking credit for someone else's article, I recommend reading the aforementioned links if you really want a more technical explanation. But for the sake of convenience, I'll give you the "short and sweet" version here.

## Basic method

Essentially what you have to do is put the iFrame embed code in a div with a custom class name that would be appropriate for your project. In this case we are using `.video-container` as the class name simply because that's what was used in the example.

Then, we style both that class and the nested iFrame as illustrated below.

*Once again, these code snippets were taken from the above articles and are being displayed here purely for your convenience.*

### HTML example:

{% highlight html %}

<div class="video-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/iWowJBRMtpc" frameborder="0" allowfullscreen></iframe>
</div>

{% endhighlight %}

### Class styles:

{% highlight css %}

.video-container {
    position: relative;
    padding-bottom: 56.25%;
    padding-top: 35px;
    height: 0;
    overflow: hidden;
}

{% endhighlight %}

### Nested iframe styles:

{% highlight css %}

.video-container iframe {
    position: absolute;
    top:0;
    left: 0;
    width: 100%;
    height: 100%;
}

{% endhighlight %}

You might not want to use `.video-container` as a class name, because it's extremely broad. It is possible that the framework or css you're using/authoring may already have this class name reserved for other things. Consider using something more appropriate to your taste.

## Some additional embedded content

Besides YouTube videos, you might consider using this technique with other types of embedded content. I've tested this method successfully with the following:

* [Goolge Maps](https://www.google.com/maps)
* [Google Views](https://www.google.com/maps/views/home?gl=us)

They both render beautifully on mobile devices.

## If you're using GitHub's Atom text editor

Since I love Atom, I've created a custom Atom snippet (scoped to Markdown) for this particular fix. The following code should be added to your snippets.cson file in the Atom Config Folder. Cson stands for CoffeScript object notation.

The snippet will be available when you are working in a Markdown document by typing in `yt` and then pressing the tab key. The `$1 and $2` in the code are just placeholders that render as the insertion points. When you execute the snippet, the cursor will automatically appear there and you just have to fill in the appropriate information. You can traverse from one insertion point to the next by pressing the tab key.

<div class="message">Please note you must include the language scope in the first line as illustrated in the code below. In this case it's scoped to GitHub Flavored Markdown, file extension: .gfm. However you may still save your Markdown file with a .md extension.</div>

### The code for the custom Atom snippet:

{% highlight coffeescript %}

'.source.gfm':
  'Embed YouTube In Markdown':
    'prefix': 'yt'
    'body': """<div class="$1">
      <iframe width="560" height="315" src="$2" frameborder="0" allowfullscreen></iframe>
    </div>"""

{% endhighlight %}

If you have any questions please hit me up on twitter: [@mattlovaglio](https://twitter.com/mattlovaglio) or shoot me an [email](http://www.mattlovaglio.com/about). I'm still in the process of setting up a commenting system, but it's not quite ready yet. Sorry folks.

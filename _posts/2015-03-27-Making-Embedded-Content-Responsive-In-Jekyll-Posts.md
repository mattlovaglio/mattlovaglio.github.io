---
layout: post
title: Making Embedded Content Responsive In Jekyll Posts
---

## Embedded content in Jekyll posts acting wonky?

If you are using Jekyll or thinking about using Jekyll for blogging you might want to consider how the content within Jekyll posts are rendered.

Some of the benefits of traditional content management systems are that they tend to have a GUI (graphical user interface) back-end and allow you to write and insert rich media much like you would a modern word processor. However a caveat of having this kind of functionality is you subscribe to the ways (or restrictions) of your specific CMS.

## Jekyll posts

Blogging with Jekyll is awesome, but remember you write posts like you would write HTML *even though you're using Markdown*. Which means that you must sometimes consider how your content will be rendered, as if you were hand coding a blog post.

Things like embedding a YouTube video or Google Map require some additional strategy. That is if you're using the iFrame method and want the content to be responsive.

<div class="message">Some people will be ok with this method, and some people won't. If you have a more appropriate technique, share it in the comments or send me a msg. Keep in mind, if you're going to be using GitHub Pages & Jekyll, you are not allowed to use plugins.</div>

If you embed a YouTube video in a Jekyll post, as per the official YouTube instructions, you might notice that on an iPhone (or any mobile device) your embedded content spills out of current viewport. Not desirable. So as you can deduce, this method is not responsive friendly.

**The default YouTube embed instructions might look something like this:**

YouTube video being referenced here: [DevTips: Getting Started With Jekyll, The Static Site Generator](https://www.youtube.com/watch?v=iWowJBRMtpc)

Basic YouTube embed link for this video: `<iframe width="560" height="315" src="https://www.youtube.com/embed/iWowJBRMtpc" frameborder="0" allowfullscreen></iframe>`

This is what you'll get on mobile devices:

---

![example](/images/example-issue.PNG)

---

This method doesn't work well.

Lucky for you, it won't take much to fix this behavior.

## Finding a solution

I recently found a solution via [@rachelmccollin](https://twitter.com/rachelmccollin) in a [Smashing Magazine](http://www.smashingmagazine.com) post.

**Here are the article links:**

[Making embedded content work in responsive design](http://www.smashingmagazine.com/2014/02/27/making-embedded-content-work-in-responsive-design/)

[Creating intrinsic ratios for video](http://alistapart.com/article/creating-intrinsic-ratios-for-video)

In the name of not taking credit for someone else's article, I recommend reading the aforementioned links if you really want a more technical explanation. But for the sake of convenience, I'll give you the "short and sweet" version here.

## Basic method

Essentially what you have to do is put the iFrame embed code in a div with a class of "video-container" (or custom class name that would be appropriate for your project). Then style both that class and the nested iFrame as illustrated below.

*Once again, these code snippets were taken from the above articles and are being displayed here purely for your convenience. I wholeheartedly give credit to their respective authors and original publications.*

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

### Nested iFrame styles:

{% highlight css %}

.video-container iframe {
    position: absolute;
    top:0;
    left: 0;
    width: 100%;
    height: 100%;
}

{% endhighlight %}

You might want to not use `.video-container` as a class name, because it is extremely broad. It is possible that the framework or css you are using/authoring may already have this class name reserved for other things. Consider using something more specific like: `.jekyll-youtube-module` or another custom class name with a higher level of specificity.

## Some additional embedded content

Besides YouTube videos, you might consider using this technique with other types of embedded content. I've tested this method successfully with the following:

* [Goolge Maps](https://www.google.com/maps)
* [Google Views](https://www.google.com/maps/views/home?gl=us)

They both render beautifully on mobile devices.

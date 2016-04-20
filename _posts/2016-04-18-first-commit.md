---
layout: post
title: First Commit
description: "Here is post description"
headline: "Here is headline"
categories: personal
tags: 
  - blog
  - jekyll
imagefeature: "summer_road.jpg"
comments: true
mathjax: true
featured: false
published: true
---

>&quot;If anything is worth doing, do it with all your heart.&quot;
><small><cite title="Buddha">Buddha</cite></small>

I have been away from the blog for quite a while. Recently, I encountered a wonderfull static website generating tool-Jekyll. After a searching online, I decided to use [hmfaysal-omega-theme](https://github.com/hmfaysal/hmfaysal-omega-theme) and begin to build my new blog. Here is my old blog building from Django+MongoDB [threelifestone](http://threelifestone.com). If the link not work, it means I close it in the future of this writing. I need some time to familiar with the tool. First, to show a piece of code as shown in below, just use four space before each line. It is very similar to the stack overflow code style. 

    It has four spaces before
     It has five spaces before
      It has six spaces before    
  

For code highlight:

{% highlight python %}
def bagOfWords2VecMN(vocabList, inputSet):
    returnVec = [0]*len(vocabList)
    for word in inputSet:
        if word in vocabList:
            returnVec[vocabList.index(word)] += 1
    return returnVec
{% endhighlight %}

Here is an example of table of contents:

<section id="table-of-contents" class="toc">
  <header>
    <h1>Table of contents</h1>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

## Item 1 ##

Notice that, ## Spaces before and after Item 1 ##

## Item 2 ##

Content of item 2

## Hello, world! ##
This is a classical example.
Good luck!

---

## Item 3  

Item 3 only has ## on the left. Notice the line above item 3.

### Subitem 1

Subitem 1 has ### on the left


### Subitem 2

This is subitem 2. Notice the line below 


---

## Other Items ##

* aaaaa
* bbbbb
* ccccc


**********************************

Examples of list:

- Item A1
- Item B1
   - Subitem C1

List with numbers:

1. item 1
1. item 2
    1. subitem 3

---


Now, comes to image: 
<figure>
        <a href="{{ site.url }}/images/gallery1/shahua.jpg"><img src="{{ site.url }}/images/gallery1/shahua.jpg"></a>
</figure>
<figure class="half">
        <a href="{{ site.url }}/images/gallery1/IMG059.jpg"><img src="{{ site.url }}/images/gallery1/IMG059.jpg"></a>
        <a href="{{ site.url }}/images/gallery1/IMG072.jpg"><img src="{{ site.url }}/images/gallery1/IMG072.jpg"></a>
</figure>

----

For mathematical equations, turn on mathjax. Here is the famous Schrodinger equation[^1]:

$$\frac{-\hbar}{2m}\frac{\partial^2\Psi(x,t)}{\partial x^2} + U(x)\Psi(x,t) = i\hbar\frac{\partial(x,t)}{\partial t}$$

**Maxwell's Equations**


$$\begin{align}
  \nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} & = \frac{4\pi}{c}\vec{\mathbf{j}} \\
  \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\
  \nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\
  \nabla \cdot \vec{\mathbf{B}} & = 0
\end{align}$$  
  
<br>



---

To show splited columns:

<div class="col-md-6">
<p class="lead">This is left column. If want to show three columns instead of two, just repeat div class col-md-x three times.</p>
</div>

<div class="col-md-6">
<p class="lead">This is the right column. Notice that we can specify col-md-x, where x is the number, but they add up should equal 12 in this site settings. </p>
</div>
<br>


Here you go.


[^1]: [Schrodinger equation wiki](https://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation)

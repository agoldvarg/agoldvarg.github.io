---
layout: post
title: "Partially Partials"
date: 2015-03-10 21:33:48 -0400
comments: true
categories: [code, how-to, flatiron, ruby, guide]
---

Opening Thoughts
-------

At school, concepts are typically presented from the bottom up. Meaning we start at the detail level and abstract our way from there. After parting with enough blood, sweat, and tears we are granted permission to weild powerful abstractions in all their glory. But this power comes with a cost. We no longer have that feeling of control. All of the sudden, things we practiced doing manually, directly, and purposefully are happening automatically, indirectly, and sometimes accidentally.

  <div align="middle">
    <iframe align="middle" src="//giphy.com/embed/i0Mdd0b7L2Cf6?html5=true" width="250" height="250" frameBorder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
  </div>

It's important to keep in mind that it **ALWAYS** feels this way. New things are new and they invariably get better with practice. I keep reminding myself that despite greater and greater levels of abstraction, *I am still writing the program -- The program is not writing me!* Rails is bursting at the seams with generators, macros, and constructor methods designed to make programmers lives easier but you can still accomplish the exact same outcomes at lower levels of abstraction. 

Focusing on the basics - DRY, writing clearly, and trying to be efficient in general will naturally lead to incorporating more advanced concepts over time.

A Partial Example
--------

*partial templates*: a powerful abstraction built into rails used to abstract reusable portions of html (or haml, or xml etc.) in Ruby (they exist in other languages too). All controllers inherit access to these partials and have the ability to cast data to the partial for rendering. I can't help but draw the comparison between the design and structure used for Ruby method calls and the way partials behave in rails. 

As an example, imagine a simple application designed to organize and display a collection of movies and tv shows. Ideally we want to maintain a consitent look and style across views in our application and we'd also like to avoid repeating the same snippets of HTML. We could quickly devise a partial for a simple header:

```html
<!-- Within views/shared/_header -->
<h1>WELCOME TO MEDIABROWSER!</h1>
<h1>IT PUTS THE MEAD IN MEDIA.</h1>
<h2>You are currently viewing <font color="red"><%= subject.title %></font></h2>

<p>
  Plot summary:
  <%= subject.plot_summary %>
</p>
```
Now that we've defined the partial, we can call it from any of our other templates - analogous to calling a helper method from a regular Ruby class. This particular partial is expecting to receive a local variable named `subject` when called from other views like so:

```html
<!-- Within views/movies/ -->
<%= render 'shared/header', {subject: @movie} %>

<!-- Within views/tv_shows/ -->
<%= render 'shared/header', {subject: @show} %>
```
When we visit the show pages for movies and shows, we see the heading, show title, and plot summary HTML elements that we only needed to code once.

Movies/show/1:

<img src="{{ root_url }}/images/mov.png" />

Shows/show/1:

<img src="{{ root_url }}/images/sho.png" />

We can extend this even further because as I mentioned earlier, partials accept collections too. A nice example would be to incorporate a list of Actors as links to the individual Actor's show pages. I am totally going to add to this post once I get a chance to build that...  Until then

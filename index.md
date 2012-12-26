---
layout: post
title: DynProg.Validation
summary: A validation library for .Net that introduce a simple DSL to make validation of arguments and method calls easier and less annoying.
---

### Why?

I wrote this library for the first time 6 or 7 years ago and keep re-writting it or enhancing it. I decided it was time to set it free and published in NuGet if for no toher reason that make my own life easier.

It's not a replacement for other popular libraries like <span class="code">FluentValidation</span> or  <span class="code">DataAnnotations</span>.

<strong>DynProg.Validation</strong> is intended to replace the countless checks for null argument and argument formatting and provide a simple and easy to use interface.

It should replace code like this:

{% highlight csharp %}
  public string setValue(string key, string value)
  {
      if (String.IsNullOrEmpty(key) || key.length < 5 || key.length > 20)
      {
          throw new ArgumentException("key");
      }
      if (String.IsNullOrEmpty(value))
      {
          throw new ArgumentException("value");
      }
      // the actual code goes here
  }
{% endhighlight %}

with something like this...

{% highlight csharp %}

  public string setValue(string key, string value)
  {
    var validator = new Validator();
    validator.CheckThat(() => key).IsNotNullOrEmpty()
        .LengthIsBetween(5, 20);
    validator.CheckThat(() => value).IsNotNullOrEmpty();
    validator.Throw();
    //the actual code goes here
  }
{% endhighlight %}

It doesn't looks like much but let's take a look at some of the niceties in the API and some of the facilities it provides before makig a decision.

### General usage

### Specific Exception per check

### Managing exceptions, throw on first, throw a list or just get the list on hold on it for a while.


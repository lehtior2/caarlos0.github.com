---
layout: post
title: "Guice and JUnit"
description: "it could be a lovy story &hearts;"
category: code
tags: [guice, java, junit]
---
{% include JB/setup %}

First of all: **Do you use Guice as Depency Injection Container in your Apps? If no, why not?**

Well, Guice is a lightweight depency injection container made by Google, for Java 5 and above.

I will not explain much more about Guice in this post, maybe another day, in another post.

But, if you use Guice in your apps, you of course has doubts about *how do I test this thing?*, am I right?

Yep, I has these doubts too, then, most of time, I just made something like this:

    public class FooTests {
      Injector i = Guice.createInjector(new FooModule());
      
      @Test
      public void testBar(){
        Bar b = i.getInstance(Bar.class);
        assertTrue(bar.thisShouldReturnTrue());
      }
    }

Pretty easy, **but**, when you want to inject some generic thing, like `Foo<Bar>`, e.g., the things start to be ugly. So, you start look around, trying to found some framework... and found it, but these frameworks come with a lot of thing you dont need, like mockito or anything else. What could you do, so?

Well, I found a great way to solve this.

I'll push it to github soon, but, I can tell you that the use is pretty simple, and it only depends on JUnit 4.10. With my lib, you will do tests just like this:

  
    @RunWith(GuiceTestRunner.class)
    @GuiceModules(FooModule.class)
    public class FooTests {
      
      @Inject Bar bar;

      @Test
      public void testBar(){
        assertTrue(bar.thisShouldReturnTrue());
      }
    }


I just dont made the push right now, because I'm using 3g, and, in Brazil, it's damn slow and expensive, so, wait until tomorrow, please :)

Cheers.
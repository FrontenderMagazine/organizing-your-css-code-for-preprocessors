*By [Tim Severien][1]*

CSS preprocessors are probably one of the most useful things we have right now
in front-end tooling. Whether you pick Sass, LESS or any other preprocessor, 
they’re great because they add so many features CSS never had. But I’m not 
trying to convince you use preprocessors, I assume you already do.

Instead, what we’re going to do is explore some different architectures you
can use with your chosen preprocessor to help you find the one that suits you 
best. Even though the files are all listed as Sass files (i.e. scss), all the 
architectures can easily be adopted regardless of your preprocessor of choice.

One of the best features of a CSS preprocessor, file inclusion, allows us to
distribute the code over multiple files. These files are later concatenated by 
the preprocessor. This allows us to have multiple files without bothering the 
browser with a long list of HTTP requests.

At first, you may be filled with excitement over this capability. That is,
until you start using it on a large project. That’s where, if you’re like me, 
you’re stylesheet has become a distributed mess. In my case, I really needed a 
structure and a way to organize my code.

What options do we have? CSS is hardly programming, but we can’t blatantly
copy a programming architecture. But how do you categorize the different 
portions of your styling? Pack your bags and put on your work shoes, it’s 
exploring time — Dora style (by that I mean sitting back and letting me do all 
the hard work
).

> As a note, I’m going to start all the architectures that I’ve personally
> defined with a folder called ‘base’, where I will put things you shouldn’t touch
> like resets and styles for included libraries.
>

## Functional Distribution

This is a structure that you may end up with when initially starting with a
preprocessor. Splitting functionality in separate files is actually a very 
logical thing to do. One for all variables, one for all mixins, etc. and finally
one for the actual stylesheets. Let’s add a`normalize.scss` for the sake of
realism.

*   /base 
*   _mixins.scss
*   _variables.scss
*   screen.scss

### Pros

*   A beautiful list of mixins and variables — yay!

### Cons

*   All the styles are in a single file.

### Conclusion

Okay, this is no good. We’ll end up with a massive script. We might as well
not use a preprocessor at all. This is pretty useful combined with the other 
architectures though. In fact, we’ll do that. But just this? Not a good idea.

## Katana Distribution

What if we divide our pages up in pieces, and style each part individually?

*   /base 
*   /sections 
    *   _header.scss
    *   _content.scss
    *   _footer.scss
    *   _sidebar.scss
    *   _modals.scss
*   _mixins.scss
*   _variables.scss
*   screen.scss

### Pros

*   Makes perfect sense
*   Unlikely to have double selectors

### Cons

*   Can get messy, especially if you have many different appearances
*   Scripts can get pretty large, `_content.scss` in particular

### Conclusion

Unfortunately, by using a structure like this, you’re motivating yourself to
target styles to specific areas only, resulting in static CSS and a lot of 
double properties (eg. border-radius). You can avoid that a little using mixins 
and variables. However, this could be considered a valid structure for small and
medium-sized projects.

## Template or Page Distribution

By writing a different stylesheet for every template or page, it’s easy to
look something up if naming is similar.

*   /base 
*   /templates 
    *   _category.scss
    *   _footer.scss
    *   _header.scss
    *   _index.scss
    *   _page.scss
    *   _single.scss
*   /pages 
*   _mixins.scss
*   _variables.scss
*   screen.scss

You may note that the template names look very WordPress-like. I did that on
purpose.

### Pros

*   Well distributed
*   Easy to look up
*   Per template customization

### Cons

*   We’re aiming for pretty specific elements again

### Conclusion

This is another acceptable candidate for certan projects. In fact, this and
previous architecture make a great couple, which could work nicely. This could 
work great on many medium to large-sized projects.

## Design Terminology

I heard Chris Coyier describe his architecture in the screencast ‘
[A Modern Web Designer’s Workflow][2]‘. As the title suggests, it’s for Web
designers, meaning that it will feel comfortable for people familiar with design
and it’s jargon.

What Chris doesn’t do is use folders, but they may be unecessary.

*   _normalize.scss
*   _buttons.scss
*   _footer.scss
*   _grid.scss
*   _header.scss
*   _icons.scss
*   _navigation.scss
*   _typography.scss
*   screen.scss

### Pros

*   Makes sense (for designers)

### Cons

*   Confusing for non-designers
*   Pretty messy
*   Can get duplicate selectors

### Conclusion

I should mention that the list of files that Chris originally showed had triple
the amount of files listed above. However this is a workable architecture. In 
fact, I usd it for quite a while.

## The Hugo Cocktail

Earlier this year, Hugo Giraudel wrote a [post about his Sass architecture][3]

*   /base 
    *   _normalize.scss
    *   _typography.scss
*   /components 
    *   _buttons.scss
    *   _navigation.scss
*   /helpers 
    *   _mixins.scss
    *   _variables.scss
*   /layout 
    *   _grid.scss
    *   _header.scss
    *   _footer.scss
*   /pages 
*   /themes 
*   /vendors 
    *   _bootstrap.scss
    *   _jquery-ui.scss
*   main.scss

### Pros

*   Small files
*   Looks organized

### Cons

*   Too many files and directories

### Conclusion

This structure can work well for large projects. As I mentioned earlier, tt’s
takes almost everything what we’ve discussed and mixes it into one architecture.
Personally, I sometimes find this structure to be a little overkill. On the 
other hand, I don’t work on many large-scaleprojects.

##A last word

These are merely examples of architectures. I have yet to discover the ‘
perfect’ one, if one exists. Even if it does, it is a personal preference anyway.
Either way, it’s an important matter to think about thoroughly. If you can avoid
creating a mess, especially up-front when you are creating a new project, you 
should.

 [1]: http://flippinawesome.org/authors/tim-severien

 [2]: http://css-tricks.com/video-screencasts/124-a-modern-web-designers-workflow/
 [3]: http://www.sitepoint.com/architecture-sass-project/

This is an experiemental demo exploring the possibilities of using the open source presentation software [Deck.js](http://imakewebthings.com/deck.js/) as a digital publication tool for books. The text and images used in this demo are "The Invention of Photography in the Victorian World" by Jennifer Green-Lewis, an essay originally published in the book [*A Royal Passion: Queen Victoria and Photography*](http://shop.getty.edu/products/a-royal-passion-queen-victoria-and-photography-978-1606061558), © Getty Publications, 2014.

View the demo online at: [gettypubs.github.io/inventionofphoto-deck.js](http://gettypubs.github.io/inventionofphoto-deck.js)

##Basics

In building a normal presentation with Deck.js you work within a single HTML file and add slides with simple section tags:

```html
  <section class="slide">
    <h1>Slide</h1>
  </section>
  
  <section class="slide">
    <h1>Content</h1>
  </section>
  
  <section class="slide">
    <h1>Here</h1>
  </section>
```

A digital book in Deck.js is structured the same way, but instead of the headings and bullet points that might be more common in a slide presentation, a digital book would include chapter and section titles, paragraphs of content, images, captions, etc...

```html
  <section class="slide">
    <h1>Chapter One</h1>
    <p>...</p>
    <p>...</p>
    <p>...</p>
  </section>
  
   <section class="slide">
    <h1>Chapter Two</h1>
    <p>...</p>
    <p>...</p>
    <p>...</p>
  </section>
```

## Navigation

Deck.js comes with some familiar, built in navigation functions and animations that work perfectly for digital books: use the left and right arrows to move from section to section in the publication; scroll down to read sections; and use the "M" keyboard shortcut to see thumbnails of all the sections. There's also a counter in the lower-right that tells readers where they are within the publication.

## Reading

While the navigation in Deck.js works almost perfectly as is for digital books, out of the box it does not allow for the overflow necessary for longer blocks of text. All content within the individual slides is scaled to fit within the height of the browser window. To remedy this for digital publications and allow for vertical scrolling, you must disable the Scale extenstion that comes with the standard Deck.js package. You can do this by deleting the CSS and JS references and associated files in your main HTML file:

```html
<link rel="stylesheet" media="screen" href="extensions/status/deck.scale.css">
<script src="extensions/status/deck.scale.js"></script>
```

Or, you can add $.deck('disableScale') to the initialization script at the end of the main HTML file:

```html
<script>
  $(function() {
    $.deck('.slide');
    $.deck('disableScale');
  });
</script>
```

## Extensions, Themes, and Related Projects

## Dependencies (included in this repository)

- [jQuery](http://jquery.com)
- [Modernizr](http://modernizr.com)

## Printing

Deck.js includes stripped down black and white print styles for the standard slide template that is suitable for handouts. It is included but not yet updated for digital publication use.

## License

Deck.js Copyright © 2011-2014 Caleb Troughton, and licensed under the [MIT license](https://github.com/imakewebthings/deck.js/blob/master/MIT-license.txt)

"The Invention of Photography in the Victorian World" Copyright © 2011-2014 Getty Publications.

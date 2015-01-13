This is an experiemental demo exploring the possibilities of using the open source presentation software [Deck.js](http://imakewebthings.com/deck.js/) as a digital publication tool for books. The text and images used in this demo are "The Invention of Photography in the Victorian World" by Jennifer Green-Lewis, an essay originally published in the book [*A Royal Passion: Queen Victoria and Photography*](http://shop.getty.edu/products/a-royal-passion-queen-victoria-and-photography-978-1606061558), © Getty Publications, 2014.

View the demo online at: [gettypubs.github.io/inventionofphoto-deck.js](http://gettypubs.github.io/inventionofphoto-deck.js)

See too another Deck.js publication, [*The Last Cartographer*](http://digitalpathways.net/lastcartographer/original/), from Simon Fraser University. (Read more about *that* project [here](http://digitalpathways.net/).) Where *The Last Cartographer* is much more a visual, multi-media presentation that takes advantage of the kind of slide- or image-based storytelling Deck.js is really built for, the demo here attempts to use Deck.js for a more traditional, text-based publication.

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

## Necessary Modifications

### Vertical Scrolling for Reading

The first thing we need to account for is that Deck.js does not automatically allow for the overflow necessary for longer blocks of text. All content within the individual slides is by default scaled to fit within the height of the browser window. To remedy this for digital publications and allow for the vertical scrolling needed for longer texts, you must disable the Scale extenstion that comes with the standard Deck.js package. You can do this by deleting the CSS and JS references and associated files in your main HTML file:

```html
<link rel="stylesheet" media="screen" href="extensions/status/deck.scale.css">
<script src="extensions/status/deck.scale.js"></script>
```

Or, you can add `$.deck('disableScale')` to the initialization script at the end of the main HTML file:

```html
<script>
  $(function() {
    $.deck('.slide');
    $.deck('disableScale');
  });
</script>
```

### Navigation

Deck.js comes with some familiar, built in navigation functions and animations that work perfectly for digital books: including being able to move left to right from section to section, having a counter that tells readers where they are within the publication, and accessing a menu of thumnails of each section much like the thumbnail view table of contents in apps built with Adobe's Digital Publication Suite.

While the Left and Right arrows come built in to Deck.js as one of the primary extensions and are easily visible on the screen for reader, by default the Menu can only be accessed with "M" on the keyboard. To give readers access to this function, we added a MENU toggle on the lower right, next to the Status counter. 

```html
<a href="#" onclick="$.deck('toggleMenu')" class="deck-menu-link">MENU</a>
```

The toggleMenu function is already included in Deck.js, this link merely gives readers a way to access it without knowing the keyboard shortcut. Once included, it can be styled anyway you'd like with CSS, and could also be applied to other elements like an icon or button.

### Styling

Deck.js comes with three Themes for styling slides. These do tend to be specific for slides though, so some custom CSS work is necessary to account for paragraphs of text and the like.

## Extensions, Themes, and Related Projects

## Dependencies (included in this repository)

- [jQuery](http://jquery.com)
- [Modernizr](http://modernizr.com)

## Printing

Deck.js includes stripped down black and white print styles for the standard slide template that is suitable for handouts. It is included but not yet updated for digital publication use.

## License

Deck.js Copyright © 2011-2014 Caleb Troughton, and licensed under the [MIT license](https://github.com/imakewebthings/deck.js/blob/master/MIT-license.txt)

"The Invention of Photography in the Victorian World" Copyright © 2011-2014 Getty Publications.

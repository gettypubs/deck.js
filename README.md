This is an experiemental demo exploring the possibilities of using the open source presentation software [Deck.js](http://imakewebthings.com/deck.js/) as a digital publication tool for books. The text and images used in this demo are "The Invention of Photography in the Victorian World" by Jennifer Green-Lewis, an essay originally published in the book [*A Royal Passion: Queen Victoria and Photography*](http://shop.getty.edu/products/a-royal-passion-queen-victoria-and-photography-978-1606061558), © Getty Publications, 2014.

View the demo online at: [gettypubs.github.io/inventionofphoto-deck.js](http://gettypubs.github.io/inventionofphoto-deck.js)

See too another Deck.js publication, [*The Last Cartographer*](http://digitalpathways.net/lastcartographer/original/), from Simon Fraser University (read more about it [here](http://digitalpathways.net/).) Where *The Last Cartographer* is much more a visual, multi-media presentation that takes advantage of the kind of slide- or image-based storytelling Deck.js is really built for, the demo here attempts to use Deck.js for a more traditional, text-based publication.

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

## Modifications

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

Deck.js comes with some familiar, built in navigation functions and animations that work perfectly for digital books, including being able to move left to right from section to section, and having a counter that gives readers some sense of where they are within the publication. There is also a thumnail view that shows all the sections in the publication, not unlike the thumbnail view in apps built with Adobe's popular Digital Publication Suite. In the iPad screenshots below, Adobe DPS is on the left, Deck.js is on the right:

![Menu Screenshots](https://github.com/gettypubs/inventionofphoto-deck.js/blob/gh-pages/images/readme_01.png)

Because Deck.js was designed with one user in mind, the presenter, there is normally no need to make access to this Menu feature more intuitive, and as a result it can only be accessed by hitting "M" on the keyboard. So, to give readers of our demo publication more direct access to this function, we added a MENU toggle on the lower right, next to the Status counter. Luckily, a `toggleMenu` function is already included in Deck.js, so it is easy to create a link that calls the function. Once created, it can be styled anyway you'd like with CSS, and likewise could also be applied to other elements like an icon or button.

```html
<a href="#" onclick="$.deck('toggleMenu')" class="deck-menu-link">MENU</a>
```

### Scroll to Top

When moving from section to section (left to right) in a Deck.js publication like this demo, you move along the same vertical point in the scroll, rather than automatically being sent back to the top (the start) of the next slide/section. This isn't an issue in the slide format where each is the same height and 100% of the browser height, but with our variable height, scrolling secdions it leads to an awkward reading experience. To address this, we added a line to the `deck.core.js` file. It's possible that there is a better way to do this, which could give us a cleaner visual transition and possibly also avoid modifying the core file. However, this seemed the simplest way to make it work, and to do so for the arrow icons, the keyboard shortcuts, *and* touch gestures. All of which serve to change slides/sections in Deck.js.

```js
if (!beforeChangeEvent.isDefaultPrevented()) {
        $document.trigger(events.change, [currentIndex, index]);
        $container.scrollTop(0); // <-- this is the new line
        changeHash(currentIndex, index);
        currentIndex = index;
        updateStates();
      }
```

### Styling

Deck.js comes with three Themes for styling slides. These do tend to be specific for slides though, so some custom CSS work is necessary to account for paragraphs of text and, in our case, figure images, captions and footnotes. For this demo, we started with the "Swiss" theme that's included with Deck.js. We also included some modest responsive styling with media queries to make for a better presentation on tablets and phones. The new stylesheet can be found at `themes/style/book.css`.

### Print Styling

Deck.js includes stripped down stylesheet for the standard slide templates that is suitable for printing out handouts, it does not work for this publications demo version. By redoing the print stylesheet though, it is quite easy to have a version of your Deck.js presentation print out in its entirety in a very clean and easy to read format. The new print stylesheet can be found at `themes/style/bookprint.css`.

![Print Style Screenshot](https://github.com/gettypubs/inventionofphoto-deck.js/blob/gh-pages/images/readme_02.png)

Note: Along with adding in the custom stylesheet for print, it was also necessary to add `media="screen"` to the core.css declaration so that the basic slide format was not applied to the print version.

```html
<link rel="stylesheet" media="screen" href="core/deck.core.css">
```

### Internal Linking -- not yet modified

All the content lives within a single HTML file, and sections are linked to one another for navigaction with anchor links:

```html
http://gettypubs.github.io/inventionofphoto-deck.js/#slide-1
http://gettypubs.github.io/inventionofphoto-deck.js/#slide-2
http://gettypubs.github.io/inventionofphoto-deck.js/#slide-3
etc.
```
The problem is that this means no existing anchor links will work as expected. So, you can't have have an anchor link for footnote or figure reference.

## Dependencies

- [jQuery](http://jquery.com)
- [Modernizr](http://modernizr.com)
- [Google Fonts](https://www.google.com/fonts)

jQuery and Modernizr are dependencies within Deck.js and are included in this repository. Google Fonts were added for this demo and not included in the repo, though would have were this intended for actual publication.

## License

Deck.js Copyright © 2011-2014 Caleb Troughton, and licensed under the [MIT license](https://github.com/imakewebthings/deck.js/blob/master/MIT-license.txt)

"The Invention of Photography in the Victorian World" Copyright © 2011-2014 Getty Publications.

#Responsive Design Workshop

##Some Examples of Responsive Sites

* [Smashing Magazine](http://www.smashingmagazine.com/)
* [Happy Cog Blog](http://cognition.happycog.com/)
* [Responsive Cat](http://roxik.com/cat/)
* [Simon Collison's Site](http://colly.com/)
* [Mediaqueri.es](http://mediaqueri.es/)
* [The Grid System](http://www.thegridsystem.org/)

##Helpful Articles/Resources

* [Responsive Design: Visual Guide VIDEO](https://www.youtube.com/watch?v=GtjDtek9EFU)
* [Responsive Web Design: What It Is and How To Use It](http://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/)
* [Brain Dump on Responsive CSS VIDEO](https://css-tricks.com/video-screencasts/102-braindump-on-responsive-web-design/)
*  [Beginner's Guide to Responsive Web Design](http://blog.teamtreehouse.com/beginners-guide-to-responsive-web-design)
*  [Blueprint: Responsive Image Grid](http://tympanus.net/codrops/2013/07/01/responsive-icon-grid/)
*  [Blueprint: Responsive Full Width Tabs](http://tympanus.net/codrops/2014/03/21/responsive-full-width-tabs/)
*  [Blueprint: Responsive Horizontal Drop Down](http://tympanus.net/codrops/2013/03/05/horizontal-drop-down-menu/)
*  [Blueprint: Responsive Multi-Column Form](http://tympanus.net/codrops/2013/06/06/responsive-multi-column-form/)

##Dissecting Bootstrap

We've all used Bootstrap and are familiar with some of its responsive elements.  We're going to work with the navbar.  Here's a simple bootstrap navbar [template](http://getbootstrap.com/examples/navbar/).  Open it up and change the screen size.  What happens?!!!?

Let's take a look at at the [Bootstrap Source Code](https://github.com/twbs/bootstrap/blob/master/dist/css/bootstrap.css)

See if you can find the line(s) responsible for making the Bootstrap Navbar responsive.  In particular, can you figure out how the hamburger icon works?


##Media Queries

Media Queries are the underlying magic behind most responsive sites.  Media Queries allow us to get information about the user's device and then selectively apply styles.  The most common use is to apply different styles depending on the screen size of a device, but media queries also give us access to things like resolution, color mode, and media type(print, braille, projection, etc.).

[MDN Media Queries](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Media_queries)

Here's a media query 'template'

```
@media (some-user-info: value) {
  //Apply the following styles only if the above condition is true
  p {
    background-color: purple;
  }
}
```

Here's a media query to text-align some stuff to the right when the screen is at least 1200 pixels wide:

```
@media (min-width: 1200px) {
  form > div > label,
	legend {
  	text-align: right;
  }
}
```

**Here's a great media query [reference guide](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/) to figure out what media queries to use to target different devices.**

##Logical Operators

####AND

```
@media (min-width: 700px) and (orientation: landscape) {
	//styles that only apply when the screen size is greater than 700px, and the device is in landscape
}
```

```
@media (min-width: 600px) and (max-width: 800px) {
  body {
    background-color: green;
  }
}
```

####OR

```
@media (max-width: 600px), (min-width: 800px) {
  html { background: red; }
}
```

####NOT

```
@media not all and (max-width: 600px) {
  html { background: red; }
}
```

Read more on logical operators [here](https://css-tricks.com/logic-in-media-queries/)


##Media Queries on a Link Attribute

Sometimes you want to apply an entire different stylesheet depending on some user media.  This is really easy to do in CSS3:

```
<link rel="stylesheet" media="(max-width: 800px)" href="example.css" />
```

---
date: 
  created: 2024-10-25
categories:
  - Marketing
  - A Builder's Journey
---

# How to Redesign an Event Landing Page - From Design to Full HTML

Recently a colleague asked if I wanted to redesign an event page for a fellow University event. Well of course, I love small gigs! Ready to ride along? I will show you how to take the [finished design from Part 1]({{ config.site_url }}/2024/10/11/how-to-redesign-an-event-landing-page---from-scratch-to-new-design/) and fully implement it into a static HTML & CSS website.

<!-- more -->

## Pick the Right Tool For the Job

Before kicking things off, let's review our requirements:

1. a static event landing page which basically acts as a flyer
2. the organizers also mentioned they would like to quickly add documentation in the future

To fulfill the first point we would only need a simple HTML page with some CSS, but for the second point we need a proper tool. In recent times I have been growing more and more fond of the [great mkdocs material project](https://squidfunk.github.io/mkdocs-material/). My favorite features of it are:

- write simple Markdown, auto-convert it to beautiful docs
- searchable, very customizable
- converts everything to a static website, meaning the server only has to serve static files and the browser does all the searching, etc. This reduces server complexity by a lot
- bonus points for site navigation working without JavaScript. I hate pages that do not even show something when JavaScript is disabled (_yes, I'm that kind of nerd_)

I have been using mkdocs material for my team's [main project](https://phaidra.org) and also for this blog. And it easily fits the needs for the event landing page too. Convenient and good choice for sure. So off we go and set up a basic page with mkdocs [](https://squidfunk.github.io/mkdocs-material/getting-started/):

![]({{ config.site_url }}/assets/img/posts/event-page-redesign-ii/barcamp3-raw-mkdocs.png)

Just by selecting the right tool we already fulfill requirement 2., ready to be used whenever the maintainers decide to add docs. Now the only job left for us is to customize our landing page to bring our design to life.

## Start With the Layout Skeleton

Before diving into any fancy details, we need to set up the overall page layout. We inspect the [new design](http://localhost:8000/2024/10/11/how-to-redesign-an-event-landing-page---from-scratch-to-new-design/#the-result-a-finished-figma-prototype) and structurally divide it into its natural sections. I counted six: `<Nav>`, `<Hero>`, `<Features>`, `<Call to Action>`, `<Discussion>` and `<Footer>`.

![]({{ config.site_url }}/assets/img/posts/event-page-redesign-ii/barcamp3-prototype-sections.png)

We can see that this is a three-column layout. The `<Nav>`, `<Hero>`, `<Call to Action>` and `<Footer>` should span the entire width, while the `<Features>` and `<Discussion>` should only span the middle part with white space to spare left and right.

### Create Basic Elements for All Page Sections

So simply start off by creating basic HTML elements for each section. No need to complicate things.

```html
<main id="landing-page">
  <section id="hero">hero</section>

  <section id="features">
    <div>Mountains Image</div>
    <div>Feature 1 Text</div>
    <div>Feature 2 Text</div>
    <div>Calendar</div>
  </section>

  <section id="call-to-action">call to action</section>

  <section id="discussion-points">
    <h3>Diskussionsthemen</h3>
    
    {% for _ in range(10) %}
      <p>Lorem ipsum</p>
    {% endfor %}
  </section>
</main>
```

Notice we do not have to take care of `<nav>` and `<footer>` since mkdocs already creates those for us.

### Make the Elements Visible With Glittery CSS

Now let's add some fancy styles to better see our elements:

```css
/* make all text big and put all content in the center */
section, section div {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: large;
}

/* "fancy" borders for visibility */
section#hero {
  border: 5px solid lightgreen;
}

section#features {
  border: 5px solid lightcoral;
}

section#call-to-action {
  border: 5px solid lightskyblue;
}

section#discussion-points {
  border: 5px solid lightgray;
}
```

### Set Up Your Layout With CSS Grid (the best layout tool)

Now comes the snazzy bit: Grid Template Areas. It is a rather unknown CSS feature which lets you very smoothly set up page layouts. There are three parts to this:

#### 1. Set `display: grid;` to the Container Element

```css
main#landing-page {
  display: grid;
}
```

#### 2. Link Each Section to A Grid-Area

```css
section#hero {
  grid-area: hero;
}

section#features {
  grid-area: features;
}

section#call-to-action {
  grid-area: cta;
}

section#discussion-points {
  grid-area: discussion;
}

/* needed since mkdocs <footer> is a bit of an edge case (not an important rabbit hole) */
footer {
  grid-area: footer;
}
```

#### 3. Magically Create Different Layouts for Desktop and Mobile

So after some repetitive prep-work, we can set up the layout with `:::css grid-template-areas`. As inspected, we want three columns, where different sections either take the full width and others only have the middle bit:

```css
/* desktop view, min-width copied from mkdocs-material which makes the switch at 76.25em too */
@media screen and (min-width: 76.25em) { 
  #landing-page {
    grid-template-areas:
      ' hero   hero   hero '
      '  .   features   .  '
      ' cta     cta    cta '
      '  .  discussion  .  '
      'footer footer footer';
    /* 
      middle bit is 61 rem, which is exactly the same for mkdocs-material content
      and whenever the page becomes bigger, the right and left part both get one fraction each
      this basically means the space is evenly divided between left and right 
    */
    grid-template-columns: 1fr 61rem 1fr;
  }
}
```

Now look at the result:

![]({{ config.site_url }}/assets/img/posts/event-page-redesign-ii/barcamp3-layout-skeleton-desktop.png)

Wow, this is amazing for a rather small amount of groundwork. Each element is visible due to the glittery borders. Notice how the middle column perfectly aligns with the content within the `<nav>` and `<footer>` provided by mkdocs. Perfect!

But what about smaller screens? On mobile we want a single column where all content just flows after one another. With `:::css grid-template-areas`, this is a breeze to set up:

```css
/* mobile */
#landing-page {
  grid-template-areas: 
    'hero'
    'features'
    'cta'
    'discussion'
    'footer';
}
```

And just like that, we created a mobile-friendly layout:

![]({{ config.site_url }}/assets/img/posts/event-page-redesign-ii/barcamp3-layout-skeleton-mobile.png){style="width:40%;margin: 0 auto;"}

With `:::css grid-template-areas`, you could super easily create another view for tablets etc. I love that tool! But for us, we now have all the basics done.

## Customize Each Element Within Your Layout

With the layout done, it becomes much easier to design each section individually without having to worry about section arrangement. I will not go through all the CSS code, as the curious can easily [look it up](https://github.com/oerBASE/Barcamp3/tree/main/docs/assets/css) in the source code, and even easily [follow each step in the process](https://github.com/oerBASE/Barcamp3/commits/main/).

I still want to show the discussion points as an example. Since we only have to take care of its contents, the CSS is very straightforward:

```css
section#discussion-points {
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 6em 1em;
  gap: 1em;
}

section#discussion-points h3 {
  font-size: var(--large-font-size);
}

section#discussion-points li, section#discussion-points p {
  max-width: 42rem; /* cap the width for very large screens */
  font-size: var(--normal-font-size);
}
```

We set `:::css display: flex;` to easily align everything in the center. We also apply `:::css flex-direction: column;` so elements flow downwards instead of the default sideways. Then we just control the spacing via `:::css padding` and `:::css gap`. The `:::css font-size` are set via CSS variables.

## Limit the Amount of Font Sizes

Another thing I want to highlight is we only use 3 font sizes, just like we defined in the design. This makes the site look much cleaner. If you want to emphasize a text, use tools like `bold` or `underline`. The variables set in **global.css** come in very handy to reduce repetition:

```css
:root {
  --huge-font-size: 3rem;
  --large-font-size: 1.5rem;
  --normal-font-size: 0.9rem;
}
```

The beauty here is that even though we use `:::css rem` for the font sizes, which normally would be static and would not change with different screen sizes; but mkdocs material has our back yet again and already did some of the heavy lifting for us. In their **main.css**, they define:

```css
html {
    font-size: 125%;
}

@media screen and (min-width: 100em) {
    html {
        font-size: 137.5%
    }
}

@media screen and (min-width: 125em) {
    html {
        font-size: 150%
    }
}
```

This automatically makes our fonts increase with bigger screens and being smaller on mobile phones, etc. Very convenient!

## The Final Site

Wrapping up, most of the custom CSS work for each section was straightforward, the only exception being the `<feature>` section, but nothing the use of `:::css display: flex` could not solve. Again, if you want to dive into the details, you can view the source code [](https://github.com/oerBASE/Barcamp3/tree/main/docs/assets/css) and the commit history [](https://github.com/oerBASE/Barcamp3/commits/main/) on GitHub.

It feels pretty good to turn a concept into reality, [live for everyone to see](https://oerbase.github.io/Barcamp3/). For me, this makes web development the best part of the process. Turning an idea into reality and pushing it online for everyone to see, that's the magic of the Internet. (_not that this event will be too relevant for most people globally speaking, but still_)

Thanks for joining along, have a great rest of your day!

<div class="goodie">
  To learn more about <a href="https://youtu.be/rg7Fvvl3taU">CSS grid</a> (<i>or any other CSS topic for that matter</i>), check out Kevin Powell's YouTube Channel <a href=https://www.youtube.com/@KevinPowell></a>. Kevin is the best CSS tutor on the planet in my humble opinion.
</div>

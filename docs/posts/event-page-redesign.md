---
date: 
  created: 2024-10-11
categories:
  - Marketing
  - A Builder's Journey
readtime: 8 # 5 was auto-calculated, but time will be spent on the images filled with text and content too
---

# How to Redesign an Event Landing Page - From Scratch to New Design

Recently a colleague asked if I wanted to redesign an event page for a fellow University event. Well of course, I love small gigs! Ready to ride along? I will show how to detect issues in the current design, how to plan for improvements and of course the final design.

<!-- more -->

## Inspect What Is Here and Highlight the Important Information

Check out the current website: 

**Homepage**

![]({{ config.site_url }}/assets/img/posts/event-page-redesign/barcamp3-old-home.png)

Even though it is in German you will follow along easily as I'll translate the key bits.

> **Translation:** Listing **When?**, **Where?** and asking visitors to register to the event via email.


**Details Page**

![]({{ config.site_url }}/assets/img/posts/event-page-redesign/barcamp3-old-info.png)

> **Translation:** The page starts off with the **What?** header (OER-Infrastructure-Barcamp), accompanied with a small motto "normalise openness".
>
> Then the date is listed with a passage about the philosophies behind the event. Followed by a rather long list of potential discussion topics.

### What Do You Think About the Site?

Before scrolling on, take a minute to think about how you assess the situation:

- What info was there for you to easily extract and understand?
- What is still missing? Where are you still confused?
- What information is important for such an event landing page?
- What would you add? What would you remove? What would you emphasize more?

### My Analysis: the Info Is There, But Badly Arranged

Diving into each page:

**Homepage**

- some of the important pieces, like <**When?**>, <**Where?**> and the <**Call to Action**>, are present which is great. But they are not necessarily highlighted
- Also, the literal questions "When?" and "Where?" are less important than the actual info. So instead of asking, simply give the answer. The visitor will figure out that "14.11.2024" will represent the <**When?**>
- the <**What?**> is missing on this page

![]({{ config.site_url }}/assets/img/posts/event-page-redesign/barcamp3-old-home-highlighted.png)


**Details Page**

- the <**What?**> is present, but still very technical. The abbreviation "OER" is not explained
- the texts are rather long. A casual visitor will evaluate whether to even attempt to read all of that
- the event date <**When?**> is repeated, which is good practice! But it is a small element which is not really visible

![]({{ config.site_url }}/assets/img/posts/event-page-redesign/barcamp3-old-info-highlighted.png)

### Steps to Fix The Bad

1. given the information is rather limited, there is no need for two separate pages. Put everything into a one-pager instead
2. emphasize all important pieces by using bigger fonts and better positioning
3. space out the long block of text into multiple paragraphs and add images so the reader can more easily digest it bit by bit

## Get to Know the People Behind the Event For Site Personality

Having evaluated the status-quo, in theory we would be equipped to create an improved design. But let us pause and take a step back. A website should represent the person(s) or organization behind it, just like a business card. One shoe does not fit all.

So in order to add perstonality to our drafts, we need to know a thing or two about the organizers behind the barcamp. After a few emails back and forth, these are the clues they gave me:

- they love black and white
- they are the nerdy types targeting nerdy folks
- it is okay to be a bit trashy

Perfect, that is all we need! This will help us for a more personal design.

## The Result: A Finished Figma Prototype

When designing website layouts, I firmly believe you should not reinvent the wheel. Just replicate design layouts that work and later add sprinkles for a personal touch. It makes it easier, both for you to design and for visitors to navigate.

So after getting some inspiration from other event landing pages I dived into [Figma](https://www.figma.com/) and came up with this:

![]({{ config.site_url }}/assets/img/posts/event-page-redesign/barcamp3-figma-prototype.png)

### A Structure That Follows Common Web Conventions

- the overall structure just imitates common web practices: a navbar, a hero, some features, some content, and the footer to wrap things up
- the top navbar shows the most important information and is present at all times. Normally you navigate between different sections of a website, but this one-pager has no real navigation so we can instead show the <**What?**>, <**When?**>, <**Where?**> and a <**Call to Action**> directly at the top. You only have to read this and already know everything important.
- the hero catches the attention of the user. It especially speaks to nerds (if you get the reference)
- we have spaced out paragraphs accompanied by visuals. Previously, this was a wall of text, but now it is separated across two feature sections with 5 paragraphs in total. A much easier reading experience!
- the visuals serve a purpose too, one repeats the <**Where?**>, the other repeats the  <**When?**> and the <**Call to Action**>. Always repeat the important stuff.
- the register via mail <**Call to Action**> gets its own section after the two blocks
- all details about discussion points are at the bottom, for invested readers, just like in the old design
- the site only uses three font sizes for a cleaner design. Font weight is the tool for prioritizing.

### Add Sprinkles For Personality

You have seen these website structures before, so as discussed we add some sparkles to make them less boring and to better resemble the event and its organizers. These were my simple ideas:

- use "[Fira Code](https://fonts.google.com/specimen/Fira+Code/license)" as the website font, which is often used within terminals, giving the site a nerdy look
- the ">" also references a terminal
- "Hello Friend{{ config.site_url }}." references the TV show [Mr. Robot](https://en.wikipedia.org/wiki/Mr._Robot), which I hope many will understand
- the second sentence in the hero ("wir müssen reden", translation: "we need to talk") makes it very clear that this is a German event
- the site is mostly black and white, which vibes with the organizers
- the image is a rough drawing of mountains; perfect since we do not want anything fancy
- the image also resembles the host city which is surrounded by mountains

## Wrapping Up & Next Up: HTML Implementation

Whew, that was quite the ride. A good time to take a break. We inspected the current version, discovered its shortcomings, got to learn some traits of the event organizers and drafted a nice design for how we want the new landing page to look like.

We achieved a lot, thanks for joining! Next post I will cover the journey from design to a fully implemented website. See you there.

<div class="goodie">
  It is always better to think about the bigger picture first, before jumping into action.
</div>
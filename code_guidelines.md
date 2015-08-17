# Code Guidelines

These guidelines outline the Forward Partners coding style for a constructing a good CSS architecture.

This is a living document, and as such will be continually updated and improved.

This document aims to:

1. Ensure code consistsency between the different Forward Partners projects; and
2. Establish best practices for internal and external developers to follow.

## Contents

1. [General guidelines](#general-guidelines)
2. [Progressive Enhancement](#progressive-enhancement)
3. [HTML](#html)
4. [CSS](#css)
5. [JavaScript](#javascript)
6. [Accessibility](#accessibility)
7. [Performance](#performance)
8. [Browser Support](#browser-support)
9. [References](#references)

## General Guidelines

The guiding principles are as follows:

- Markup should be clear, concise, semantic and valid.
- Javascript should progressively enhance the user's experience.

Projects are expected to be:

- Developed from a 'mobile-up' perspective;
- Developed to be progressively enhanced;
- Developed to be fully accessible (WCAG AA);

### Indentation

Indent all code by 2 spaces. This minimises horizontal whitespace.

### Readability vs Compression

Code is designed to be read, and subsequently maintained by developers. Therefore use of whitespace and comments are encouraged in order to promote maintainability.

There is no need to purposively compress HTML, CSS of Javascript in the development environment. Minification, concatenation and compression are handled by the frontend build tools prior to deployment (currently Gulp).

## Progressive Enhancement

It is important that you follow the principles of progressive enhancement. The Government Digital Service explain Progressive Enhancement [here](https://www.gov.uk/service-manual/making-software/progressive-enhancement.html).

Make sure your content is in a logical order. Select the most appropriate HTML tags (and WAI-ARIA attributes) to markup the content. Use an externally linked CSS file to style the page. Enhance elements on the page using unobtrusive, externally linked JavaScript.

## HTML

### HTML5

Use the HTML5 doctype by default when marking up a page.

```
<!DOCTYPE html>
```

This allows us to use WAI-ARIA roles, microdata and validate our pages. This also triggers standards mode in the browser.

We test our markup against the [W3C validator](http://validator.w3.org/), to ensure that the markup is well formed. 100% valid code is not essential, but validation helps identify possible issues when building maintainable, accessible, robust sites as well as debugging code.

UMake full use of the new HTML5 elements such as `main`, `header`, `nav`, `section`, `article`, `aside`, `footer`. However ensure that they are being used correctly. Good guidance can be found on [HTML5doctor.com](http://html5doctor.com/element-index/) element index.

### Attributes

Wrapping inline attributes in quotation marks is optional in the HTML5 specification. However we require the use of double quoation marks around attributes.

```
// Good
<a href="http://www" class="link">Click me</a>

// Bad
<a href=http://www class=link>Click me</a>
```

### Character Encoding

All markup should be delivered as UTF-8. This should be specified in a meta tag in the head of the document.

```
<meta charset=UTF-8">
```

### Semantic HTML

You are reminded to use markup that represents the semantics of the content being created, in the logical order that the content is displayed in the document. This is the fastest way to ensure you are accessible by default.

The following are guidelines for when a specific element should be used:

Specifying the language of content via the lang attribute which ensures content is read out correctly by screenreaders.

```
<html lang="en-GB">
```

Do not use `<br/>` tags to break chunks of text into paragraphs. Use `<p>` tags.

### Headings

Each page should have one unique `<h1>`. This is normally the page or article title. This is essential for those navigating the page using an assistive device.

Use a semantically correct heading hierarchy. Headings represent the outline for your document and are essential to users of assistive devices in navigating the entirity of the page, so they should be logical.

Always use title-case when entering text into headers and titles. Do not use all caps or all lowercase titles in markup, as this is difficult to read. Instead use CSS to transform the text into uppercase/lowercase based on a class name, or element type.


### Links & Buttons

An anchor link should take you to content on the same page or another page. The button tag should perform an action such as opening a widget or submitting a form. Do not use a link to open a modal, or a button to link off to another part of the same page.

### Tables

Do not use tables for page layout.

Use THEAD, TBODY, CAPTIONS and TH tags (with the scope attribute) when marking up tables.

### Forms

Use label fields to label each form field, the for attribute should associate itself with the id of the input field, so users can click the labels. The label and the input should normally be wrapped in a `<div>` element.

```
<div>
  <label for="search-field">Search Field</label>
  <input type="text" id="search-field"/>
</div>
```

Do not use the size attribute on input fields. The size attribute is relative to the font-size of the text inside the input. Instead use the css width property to adjust the size of the input.

### Microformats

In order to convey more information to search engines, use microformats and/or microdata. An example of this is marking up an hCard or and address.

### WAI-ARIA roles

WAI-ARIA landmark roles are important for conveying extra information to users navigating your website using an assistive device such as a screen reader.

A list of the most used [WAI-ARIA landmark roles can be found here]().

This [article by the Paciello Group](http://www.paciellogroup.com/blog/2013/02/using-wai-aria-landmarks-2013/) explains more about WAI-ARIA roles.

The most commonly used WAI-ARIA roles are:
```
role="banner"
role="complementary"
role="contentinfo"
role="form"
role="main"
role="navigation"
role="search"
```

Use the `aria-required="true"` attribute to indicate that a form field is required before a form can be submitted. This can also work along with the HTML5 `required` attribute but cannot be replaced by it.

For example:

```
<form>
  <label for="first-name">First name:</label>
  <input id="first-name" type="text" aria-required="true" />
</form>
 ```

Live regions are useful to inform screen reader users of dynamic text changes, for example:
```
<div aria-live="polite" aria-atomic="true">
```

You should follow the [WAI-ARIA 1.0 Authoring Practices](http://www.w3.org/TR/wai-aria-practices/) when implementing javascript widgets such as sliders, tooltips and tab panels.

## CSS

CSS should be added to the document by referencing external files in the head. Do not use inline CSS to style the page.

Use the `<link>` tag rather than the `@import` statement.

All elements are to be styled using class names, no IDs. Avoid styling elements such as `<h1>` in favour of using reusable class names. This is a more flexible approach.

### Reset

We use [Normalize.css](https://github.com/necolas/normalize.css/) to reset the styles for the website to a sensible baseline.

### Naming Classes

We follow the a variant of the BEM naming convention for naming classes. BEM is an acronym that stands for block, element, modifier. Elements of a block are signified by using double underscores wheras a modified block is signified using double dashes, as so:

```
.block { }
.block__element { }
.block--modifier { }
```

The block can be seen as a component that makes up part of the page, such as a 'callout'. The element is a descendant of the block and helps form it. The modifier represents a different state or version of the block.

A simple example of this uses the human body. If you were to 'markup' the human body using BEM you would do as follows:

```
// Body is the 'block'
.body {}

// The hand is an 'element' of the body block.
.body__hand {}

// The right hand is a modified version of hand, in the same way the male is a modified version of the body.
.body__hand--right {}
.body--male {}
```

When modifying a block we do so as such:

```
<a href="" class="block block--modifier"></a>
```

We use BEM in order to clarify the relationship that components and subcomponents have to one another. It is an organisational tool that helps the developer by making the code more maintainable.

Further explanation of this can be found on [CSS Wizardry](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/).

*Additionally*, do not use presentational class names.

### SASS

We use the .scss flavour of the SASS preprocessor in order to help make our code more maintainable and accessible to future developers. *Do not use SASS purely for organisational purposes*

Therefore, when using SASS aim for a shallow heirarchy. The exception is for states where nesting is logical and useful.

For example:

```
// Bad, uneccessary nesting of selectors
.block {
  background-color: green;

  .block__element {
    colour: blue;
  }
}

// Good, shallow heirarchy
.block {
  background-color: green;
}

.block__element {
  color: blue;
}

// Nesting of states
.block {
  background-color: green;

  &:hover {
    background-color: blue;
  }
}
```

When using `@extends`, `@includes` and `&` states organise them as follows:

```
.block {
  @extend %clearfix; // extends come first
  @include span(12); // includes come second

  &:hover {
    //states come last, and are separated from the main block by one line of white space.
  }
}
```

### CSS Architecture

All projects should be organised using the following CSS architecture. This allows for an easily maintainable, and scalable website architecture.

Example file structure:

```
  /base
    _typography.scss
  /components
    _block.scss
  /core
    _functions.scss
    _mixins.scss
    _placeholders.scss
    _variables.scss
  /layouts
    _header.scss
  _settings.scss
  _index.scss
```


`_index.scss` contains a list of all of the individual files, imported using SASS's `@import` command.

`_settings.scss` contains the key projects settings, variables, and configuration maps.

*core* directory contains all non-printing styles, or SASS helpers. These can either be organised in named files, e.g. `_visually_hidden.scss` or in single function-based files, e.g. `_mixins.scss`.

*base* directory contains all of the visual styles that are not based on layouts or components, for example, typography.

*components* directory holds self-contained components. Each file is a block (see BEM above) and is named after the component. for example, `.block {}` is in file `_block.scss`.

*layouts* directory contains layout classes. These are shelves that the components are slotted into.

## JavaScript

We *do not* rely on a JavaScript preprocessor such as CoffeeScript. Please write all code in vanilla JavaScript.

### JavaScript Libraries

Our library of choice is [jQuery](http://jquery.com/). However, we avoid using jQuery mobile or jQuery UI.

Use [html5shiv](https://github.com/afarkas/html5shiv) to ensure html5 element work in older version of Internet Explorer (pre IE 9) which is also provided as part of mas-assets

### JavaScript Code Guidelines

We are currently adhering to the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript).

## Accessibility

All web pages must comply to Web Content Accessibility Guidelines (WCAG) 2.0 AA standard both to the letter and in spirit.

The four characteristics of accessible web content are:

## Perceivable

- Provide text alternatives for non-text content.
- Provide captions and other alternatives for multimedia.
- Create content that can be presented in different ways, including by assistive technologies, without losing meaning.
- Make it easier for users to see and hear content.

## Operable

- Make all functionality available from a keyboard.
- Give users enough time to read and use content.
- Do not use content that causes seizures.
- Help users navigate and find content.

## Understandable

- Make text readable and understandable.
- Make content appear and operate in predictable ways.
- Help users avoid and correct mistakes.

## Robust

- Maximize compatibility with current and future user tools.

## Common Accessibiliy Blunders

Please watch out for the following 'accessibility blunder'. These are commonly made and ear easily avoidable. Accessibility is similar to progressive enhancement in that if you start coding with the principle in mind then you need to make very few changes later on in the project.

Common blunders include:

Content not being in a logical order in the document. Do not focus on the visual layout and ignore the content hierarchy.

Not using the alternative text ("alt") attribute that conveys the meaning of an image appropriately. Conversely not applying a null attribute if the image is decorative, or of no realy value, e.g. `alt=""`.

Not having a text alternative for multimedia content, i.e captions and transcripts.

Using jargon or complicated language instead of simple and clear language.

Not using headings correctly. A page should have one single h1 representing the page title. Other headings should be hierarchichal and allow a screen reader user to get an overview of the content on a page.

Failing to use the most appropriate semantic elements to mark up content.

Using too many lists and headings which add aural clutter to screen reader users.

Failing to mark up forms correctly.

Communicating information by colour alone which will not be percieved by colour blind users.

Not having a visual state that shows when an element has focus - i.e not styling :focus the same as :hover.

Only communicating states and actions visually - e.g selected, open, close. This also needs to be in the content/markup layer.

Failing to allow a keyboard user to access all content and functionally on a page - usually by using incorrect HTML elements, e.g spans and divs instead of links or buttons or by introducing keyboard traps with javascript.

Failing to inform a screen reader user when content dynamically updates on a page.

Failing to set focus when dynamic content is loaded such as a modal box and not enabling a keyboard user to close such content.

## Performance

A slow website results in poor user experience. Most of web page performance is affected by front-end engineering, that is, the user interface design and development.

### Basics

Link to styles from the document head. A browser renders a page progressively in a specific order, and it will not render a page until it has gathered all the required style information. If you are linking to the page's stylesheets at the bottom of a page it will not draw the page until this link is reached. Consequently we link to our stylesheets in the head so that the browser can start rendering immediately upon load.

Link to non-essential scripts from the bottom of the document (before the closing body tag) as JavaScript blocks the browser from downloading assets until it has loaded any required scripts.

A browser normally attempts to download as many assets as it can in parallel. JavaScript interrupts this process.

First, the browser assumes that any script being called may alter the page substantially and therefore prioritises loading the script before loading an asset.

Secondly, scripts are downloaded asynchronously in order that a library like jQuery arrives before the script that relies on it (your slider plugin).

In a nutshell - to render a page as fast as the browser will allow link to your styles in the head and to prevent JavaScript from stalling the rendering process, call scripts from the bottom. An excpetion is when creating contextual classes that are used for layout such as .js - these need to be in the head to prevent a flash of unstyled content.

### HTTP Requests

Download less.

Every asset on a page requires a HTTP request to call it to be downloaded and rendered. This involves a DNS lookup, redirects and possible 404 errors for lost assets. Minimising the amount of information the browser has to request is the simplest way of increasing website performance.

Additionally, browsers can only download a set number of assets "in parallel" which can introduce a bottleneck when downloading, for example, large images.

### Browser Support

We accept that the nature of the web is such that not all web pages can be produced uniformly and consistently across all browsers. The following browser support guidelines seek to address the trade-off between experience, reach and resources.

### Primary Browsers - supported

All content must be readable and all functionality must work.

| Browser name | Version | Platform  |
| ------ | ------ | -----: |
|  Internet Explorer  |  9,10 |   Windows  |
|  Firefox  |  Latest version  |   Mac/Windows  |
|  Chrome  |  Latest version |   Mac/Windows  |
|  Safari  |  5.1+  |   Mac  |


### Mobile browsers - supported as secondary browsers
Follow secondary browser standards of performance and user experience.

| Browser name | Version | Platform  |
| ------ | ------ | -----: |
|  Safari for iOS  |  6+  |   iOS iPad, iPhone  |
|  Chrome for iOS  |  Latest version  |   iOS iPad, iPhone  |
|  Android Webkit  |  2.x and 4.x  |   Android  |

**Latest version** - Where latest version is listed, it means the latest major stable version plus one major version back, as these browsers regularly self-update.

## References

These Code Guidelines based on the [Money Advice Service](https://github.com/moneyadviceservice/frontend-code-standards) code standards and have been expanded on.

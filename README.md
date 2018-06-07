# HTML Forms

## Problem Statement

Up until this point, all of the HTML elements that we've introduced are used to
display data to the user. This is great, but what happens when we want to _get_
information from our users? In order to get user information we need to write
HTML forms. We will learn to write HTML forms in this lesson.

## Objectives

1. Define the purpose of a form
2. Write an HTML form tag
3. Define the `GET` vs `POST` HTTP methods
4. Write HTML form data elements

## Define The Purpose Of a Form

Forms gather user information. Let's suppose that you're the owner of a dog
walking business that needs a way to gather information from clients. You want
to create an HTML form to collect information like:

* owner's name
* owner's address
* dog's name
* dog's age
* walking frequency

You can do this with HTML. When the owner fills out the form and clicks
"Submit," a record of their responses will be sent to a server where the
information can be stored and used for newsletters, promotions, and invitations
to client-appreciation parties.

To process and store the information, we would need a language like Ruby, PHP,
Java, or C++. We won't be covering that in this lesson. However, _all_ those
languages are designed to receive the information sent by an HTML form.

## Write An HTML Form Tag

The crucial starting element is the `<form>` tag.  The form element wraps all
the `input` elements that will collect our users' information inside of them.
Examples of `input` elements are text fields, text areas, radio buttons,
drop-down lists, and password fields. We will cover the `input` elements later
in this lesson.

The first attribute, `action`, decides where the user information is sent.
This is typically the URL of a remote server.

The second attribute, method, sets the HTTP method the browser will use to send
the user information to the server. You can think of "HTTP method" as being
like an envelope type. Some envelopes are good for documents, other envelopes
are good for confidential letters, others are good for international postage.
The HTTP methods used in forms are GET and POST. Let's examine how the HTTP
method changes the "envelope" around our users' information.

## Define The `GET` vs. `POST` HTTP Methods

### GET

Below we see the `form` example code for making a `GET` request.

```html
<form action="http://example.com/process-user.php" method="GET">
  <input type="text" name="owner-name">
  <input type="text" name="dog-name">
  <input type="text" name="favorite-toy">
  <input type="submit" value="submit">
</form>
```

When the user clicks the submit button, their responses in the `input` fields
are captured and labeled using the `name` attributes from each element. The
browser temporarily stores this information like so:

`owner-name=Bob+Barkley&dog-name=SirBarksALot&favorite-toy=ball`

This is known as the _Query String_.  The browser _then_ attaches the _Query
String_ onto the location listed in the `action` attribute after a `?` to
create a URL that looks like this:

`http://example.com/process-user.php?owner-name=Bob+Barkley&dog-name=SirBarksALot&favorite-toy=ball`

The browser then goes to this new URL.

The HTTP `GET` method is the default method for browsers to request material on
the internet. When a _Query String_ is added, it's a **great** solution for
filtering the information that comes back.  While this is a great method for
things like search, this is not really ideal for passwords, as the people
looking over your shoulder at your favorite park might be able to read the
contents of what you are sending.

When you need to send your response in a way that doesn't leak information, you
want your form to use the `POST` HTTP method.

### POST

Below we see the same form example code for making a POST request.

```html
<form action="http://example.com/process-user.php" method="POST">
  <input type="text" name="owner-name">
  <input type="text" name="dog-name">
  <input type="text" name="favorite-toy">
  <input type="submit" value="submit">
</form>
```

When the user clicks the submit button, their responses in the `input` fields
are captured and labeled using the `name` attributes from each element. The
browser temporarily stores this information like so:

`owner-name=Bob+Barkley&dog-name=SirBarksALot&favorite-toy=ball`

A `POST` is like a secure envelope, we can't see the information being sent.
That's why `POST` is the right call when sending sensitive information like
passwords or national IDs. The user's browser **is not redirected** in this
case.

Now that we know how to write a form tag and we understand the HTTP action that
goes in its `action` attribute, let's talk about different ways we can ask for
information within our `form`.

## Write HTML Form Data Elements

### Text Field Input

Creating an `input` tag with `type="text"` gives our users a place to type
in a single line of text. It looks like this:

`<input type="text" name="owner-name" placeholder="Full Name"> `

The `placeholder` attribute puts some dummy text into the element that will be
replaced as the user starts typing.  The `name` attribute gives our input a
name.

```html
<label for="owner-name">Owner Name</label>
<input type="text" name="owner-name" placeholder="Full Name">
```

<label for="owner-name">Owner Name</label>
<input type="text" name="owner-name" placeholder="Full Name">

Generally, HTML form attributes should not contain spaces. Common exceptions to
this rule are `placeholder` and `class`. If you're not sure whether or not your
attribute can contain a space, check out [this article][article].

### A Note on Labels

You might have noticed we sneaked an extra tag in, the `label` tag. When
writing forms, we don't want to describe what goes in the form by using `p`
tags. We can "tie" descriptive text to an input field using a `label` tag. The
`name` attribute of the `input` is provided to the `label`'s `for` attribute
and the browser knows to put them close to each other.

While labels are not strictly necessary on HTML forms, they increase the
usability and accessibility for those using the web with assistive devices.
It's the Right Thing to Do.

### Password inputs

Creating an `input` tag with `type="password"` gives our users a place to type
information that will _not_ be displayed by the browser. Most of the time
browsers put `*` or dots instead of the character.  This is useful when private
information is entered, so your password isn't displayed for others to see.

```html
<input type="password" name="password" placeholder="Enter your password here">
```

<input type="password" name="password" placeholder="Enter your password here">

#### Telephone inputs

Creating an `input` tag with `type="tel"` behaves like a text field, but will
bring up the numeric keypad on supported mobile devices.

```html
<input type="tel" name="phone" placeholder="Phone Number">
```

<input type="tel" name="phone" placeholder="Phone Number">

#### Submit Tag

Creating an `input` tag with `type="submit"` creates a submission button that,
when clicked, will send a users `form`.  The `value` attribute holds the text
that will appear on the button.

```html
<input type="submit" value="Let me walk your dog!">
```
<input type="submit" value="Let me walk your dog!">

#### Radio Inputs

Radio inputs are useful when you want to have several possible options, but only
want the user to make one choice. To accomplish this, you set different `value`
attributes for each radio button, but they _must_ have the same `name`
attribute.

```html
<h3>Does your dog get along with other dogs?</h3>
<input type="radio" name="plays-well-with-others" value="high"> The more dogs, the better!<br>
<input type="radio" name="plays-well-with-others" value="medium"> It depends on the dog, but generally they are ok<br>
<input type="radio" name="plays-well-with-others" value="low"> My dog prefers their walkies solo<br>
```
<h3>Does your dog get along with other dogs?</h3>
<input type="radio" name="plays-well-with-others" value="high"> The more dogs, the better!<br>
<input type="radio" name="plays-well-with-others" value="medium"> It depends on the dog, but generally they are ok<br>
<input type="radio" name="plays-well-with-others" value="low"> My dog prefers their walkies solo<br>

#### Checkboxes

Checkboxes are ideal if we wish to allow our users to choose one or more values.

```html
<h3>What are your dogs favorite toys?</h3>
<input type="checkbox" name="toy-1" value="kong"> Kong <br>
<input type="checkbox" name="toy-2" value="stuffed-animals">Stuffed Animals<br>
<input type="checkbox" name="toy-3" value="rope-toys">Rope Toys<br>
<input type="checkbox" name="toy-4" value="squeaky-toys">Squeaky Toys<br>
<input type="checkbox" name="toy-5" value="balls">Balls, Frisbees, anything a dog can fetch!<br>
```

<h3>What are your dogs favorite toys?</h3>
<input type="checkbox" name="toy-1" value="kong"> Kong <br>
<input type="checkbox" name="toy-2" value="stuffed-animals">Stuffed Animals<br>
<input type="checkbox" name="toy-3" value="rope-toys">Rope Toys<br>
<input type="checkbox" name="toy-4" value="squeaky-toys">Squeaky Toys<br>
<input type="checkbox" name="toy-5" value="balls">Balls, Frisbees, anything a dog can fetch!<br>

#### Select Menus

Select menus create a drop menu with either single or multiple selectable
options. Here the user could choose a single option, so this could be a
replacement for a set of radio buttons, or you can allow your user to make
multiple selections. Here you assign a text label between the opening and
closing option elements as well as a `value` attribute that is the the choice
the user selects that will be passed along during form submission. The order
that you list your choices in your HTML will be the order they are displayed in
the select drop-down.

```html
<h3>What size is your dog?</h3>
<select name="size">
  <option value="small" selected>Small(0-25 pounds)</option>
  <option value="medium">Medium (26-50 pounds)</option>
  <option value="large">Large (51-75 pounds)</option>
  <option value="x-large">Extra Large (over 75 pounds)</option>
</select>
```

<h3>What size is your dog?</h3>
<select name="size">
  <option value="small" selected>Small(0-25 pounds)</option>
  <option value="medium">Medium (26-50 pounds)</option>
  <option value="large">Large (51-75 pounds)</option>
  <option value="x-large">Extra Large (over 75 pounds)</option>
</select>

#### Textarea

Textarea elements are useful if we want our users to be able to be able to write
multiple lines of text. For example, if we wish to allow our clients to write
special notes for their dogs, we can let them write as much or as little as they
like.

```html
<h3>Any other things we should know about your dog?</h3>
<textarea name="message"></textarea>
```

<h3>Any other things we should know about your dog?</h3>
<textarea name="message"></textarea>

## Summary

We use HTML `form`s to collect data from users. Start with a form element. Give
it an `action` and `method`, probably `POST`.  Inside the `form` add several
`input` elements.  You won't use them all, so don't try! Use the best `input`
for the data you're requesting. Make sure that your `input`s are clearly
labeled. If you follow these guidelines you'll soon be getting all the user
data you can handle!

## Resources

- [HTML Forms and Iframes](https://www.youtube.com/embed/eiCtXc2YMKc?rel=0)
- [Presentation Slides](https://docs.google.com/presentation/d/115ECvsMyDnFBcc-Rvb4Jn876JhOycXxKVN6sv7OiJ1Y/edit?usp=sharing)
- [MDN - HTML - Form](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form)
- [MDN - HTML - Button](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)
- [HTML Goodies - Form Basics](http://www.htmlgoodies.com/primers/html/article.php/3881421)
- [HTML Form Generator](http://www.phpform.org/)

<p class='util--hide'>View <a href='https://learn.co/lessons/HTML-Forms-and-iFrames'>HTML Forms and iFrames</a> on Learn.co and start learning to code for free.</p>

[article]: https://www.htmlgoodies.com/primers/html/article.php/3881421

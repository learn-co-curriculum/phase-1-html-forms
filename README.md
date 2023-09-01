# HTML Forms

## Learning Goals

- Explain the purpose of HTML forms
- Write an HTML `form` tag
- Define the `GET` vs. `POST` HTTP methods
- Write HTML `form` data elements

## Introduction

Up to this point, all of the HTML elements we've seen are used to display data
_to_ users. This is great, but what happens when we want to get information
_from_ our users? In order to get user information we need to write HTML forms.
We will learn how to do that in this lesson.

## State The Purpose Of a Form

Forms gather user information. They're just like surveys you might fill out
about an event you attended, or a medical history form you'd fill out at the
doctor's office.

Let's suppose that you're the owner of a dog walking business that needs a way
to gather information from clients. You would use an HTML form to collect
information like:

- owner's name
- owner's address
- dog's name
- dog's age
- walking frequency

You collect this information in HTML tags called `input`s located within the
`form` tag. You will also code a `submit` button so the client can say "OK! I'm
done!" We'll discuss `input`s in more detail below.

When the owner fills out the form's inputs and clicks the submit button, a
record of their responses will be sent to a server where the information can be
stored. Once the server has the information stored, code can be written to use
that information to create an account for the owner, send payment reminders,
send invitations to client-appreciation parties, etc.

To store the information, we need a language like Python, PHP, or Java. You will
learn how to do that later in the course. For now, let's learn how to write an
HTML form.

## Write An HTML Form Tag

The starting element in an HTML form is the [`<form>` tag][form]. The `form`
element wraps all the [`input` elements][input] that will collect our users'
information and allow them to submit it when they're done. The `form` tag looks
something like this:

```html
<form action="http://example.com/process-user.py" method="POST">
```

The `form` tag's first attribute, `action`, decides where the user information
is sent. This is typically the URL of a server. This server will run the code
(Python, PHP, Java or other) to use the data in some way. In our dog walking
business example, the server would most likely store the information in a
database.

The second attribute, `method`, sets the _HTTP method_ the browser will use to
send the user information to the server. There are two methods that can be used
with HTML forms: `GET` and `POST`. In most cases, when you fill in an online
form and submit it, the _HTTP method_ being used is `POST`, but there are some
common use cases for `GET` as well.

## Define The `GET` vs. `POST` HTTP Methods

### GET

One common use for the `GET` method with forms is to filter the content being
displayed on a page. When you use a search box on a website, you may be using an
HTML form. Let's take a look at an example.

![amazon search box](https://curriculum-content.s3.amazonaws.com/phase-1/html-forms/amazon.png)

Go to [amazon.com](https://www.amazon.com/), right-click inside the search box
and select "Inspect" from the menu. In the "Elements" tab of the DevTools, you
should see an `input` tag with a `type` of "text" highlighted. If you look up a
few lines from there, you should see the opening `form` tag. It will look
something like this:

```html
<form id="nav-search-bar-form" accept-charset="utf-8" action="/s/ref=nb_sb_noss_2" class="nav-searchbar nav-progressive-attribute" method="GET" name="site-search" role="search">
```

Note that the `method` for this `form` element is `GET`.

Go ahead and enter "dog toys" into the search box and hit enter. The content on
the page will update to reflect your search. Now take a look at the page's URL;
you should see the search term "dog+toys" embedded in it somewhere.

We mentioned earlier that our form needs some way to submit the information.
With the Amazon search box (and probably many others you've used), after typing
in our search string, we can hit "enter" to submit the form. When we hit enter,
we're actually using another `input`! There is just some extra code behind the
scenes that enables users to submit the form without clicking the button.

Right-click on the magnifying glass icon at the end of the search box and select
"Inspect." Once again, you'll see an `input` highlighted in the "Elements" tab.
Note that in this case the `type` attribute is set to "submit".

While `submit` `input`s are typically styled as buttons and typically have
labels like "Create Account", "Sign Up", or "Submit", that doesn't have to be
the case. They can be styled and labeled any way you like, or even suppressed
from view entirely!

Amazon's search box is just a special type of HTML `form`. It may look different
from a typical web form, but it's built from the same components: a `form` tag
that wraps `input` tags.

While `GET` is often the `method` used for HTML forms that filter content, you
can use it as the method with any HTML form. For example, we could use a `GET`
request to collect the info for our dog walking business. The `form` might look
something like this:

```html
<form action="http://example.com/process-user.py" method="GET">
  <input type="text" name="owner-name" />
  <input type="text" name="dog-name" />
  <input type="text" name="favorite-toy" />
  <input type="submit" value="submit" />
</form>
```

When the user clicks the submit button, their responses in the `input` fields
are captured and labeled using the `name` attributes from each element. The
browser captures this information and represents it behind the scenes like this:

```txt
owner-name=Bob+Barkley&dog-name=SirBarksALot&favorite-toy=ball
```

This is known as the _Query String_. The browser _then_ attaches the _Query
String_ to the location listed in the `form`'s `action` attribute after a `?` to
create a URL that looks like this:

```txt
http://example.com/process-user.py?owner-name=Bob+Barkley&dog-name=SirBarksALot&favorite-toy=ball
```

The browser redirects to this new URL and the server uses _back end programming_
to access and use the information in the _Query String_ in some way, e.g., to
save it to a database.

While this is a great method for things like search, it would be bad for
passwords. A URL containing a _Query String_ that includes
`password=ByronBestPoodle` is not a good way to handle passwords! When you need
to send your response in a way that doesn't leak information, you want your form
to use the `POST` _HTTP method_.

> **ADVANCED**: An advanced concept is that a `GET` request is "idempotent."
> That means the browser can run it repeatedly without changing information on
> the back-end. We can ask for a filtered list of dog toys again and again and
> again by refreshing the page again and again and again. Nothing changes on the
> server if we do that.

### POST

Below we see our example dog walking form with a POST request:

```html
<form action="http://example.com/process-user.py" method="POST">
  <input type="text" name="owner-name" />
  <input type="text" name="dog-name" />
  <input type="text" name="favorite-toy" />
  <input type="submit" value="submit" />
</form>
```

It's exactly the same form as before, except the `method` attribute is now
`POST` instead of `GET`.

When the user clicks the submit button, their responses in the `input` fields
are captured using a query string, just like before:

```txt
owner-name=Bob+Barkley&dog-name=SirBarksALot&favorite-toy=ball
```

But in this case, rather than redirecting to a URL that contains the query
string, the information is passed to the server behind the scenes. This keeps
the form information protected.

A `POST` is like a secure envelope. We can't see the information being sent.
That's why `POST` is the right call when sending sensitive information like
passwords or national IDs. We can't show you a screenshot of what this looks
like because, well, there's nothing to show. Usually after a successful POST,
the web site will send you to a page that says "Thanks for your purchase" or
"Thanks for joining our site."

> **ADVANCED**: An advanced concept is that a `POST` request is **not**
> "idempotent." If the browser runs it repeatedly, it **will** change data on
> the back end. Submitting payment for a credit card is **not** idempotent.
> Each refresh will take money out of your bank account! That's why many
> finance sites say "Don't refresh this page while we process your request."

Now that we know how to write a `form` tag and we understand the HTTP method
that goes in its `method` attribute, let's talk about different ways we can ask
for information within our `form` by choosing the right `input`.

## Write HTML Form Data Elements

What _is_ an `input`?

Think about a doctor's questionnaire: sometimes they ask you to fill in the
blank, sometimes they ask you to mark checkboxes next to symptoms, and other
times they ask you to write a short answer. They ask all these different _types_
of questions within the same questionnaire or _form_. All of those types of
questionnaire prompts have a cousin in an HTML `input` or tag. A
fill-in-the-blank question is an `<input type="text">`. A checkbox is `<input
type="checkbox">`.

The rest of this lesson will be spent introducing you to the `input` elements,
as well as two other elements that can be used in HTML forms: `select` and
`textarea`.

Examples of each type of form element we'll discuss are included in
`index.html`. Open it in the browser to see the different types in action and
try them out. Note that there is no back-end code to handle form submission so
if you click the submit button, you'll get an error.

### Text Field Input

Creating an `input` tag with [`type="text"`][text] gives our users a place to type
in a single line of text. It looks like this:

```html
<label for="owner-name">Owner name:</label>
<input
  type="text"
  name="owner-name"
  id="owner-name"
  placeholder="Full Name"
/>
```

The `placeholder` attribute puts some dummy text into the element. That text
will be replaced when the user starts filling it in. The `name` attribute
gives our input a name.

Generally, the values of HTML form attributes should not contain spaces. Common
exceptions to this rule are `placeholder` and `class`. If you're not sure
whether or not your attribute's value can contain a space, check out [this
article][article].

### A Note on Labels

You might have noticed above that instead of using a paragraph or heading tag to
label the field, we used a [`label`][label] tag. This tag, which is intended
specifically for labeling form inputs, allows us to "tie" descriptive text (that
is, a label) to an input field. The `id` attribute of the `input` is provided to
the `label`'s `for` attribute so the browser knows that the `label` "belongs" to
that `input`.

Labels are important for those using assistive devices. It makes our site
accessible, which means more users can use it. It's one of the ways we can help
ensure that the web is an inclusive and accessible place.

### Password Inputs

Creating an `input` tag with [`type="password"`][pw] gives our users a place to
type information that will _not_ be displayed by the browser. Most of the time
browsers put `*` or a dot in place of each character. This is useful when
private information is entered, so your password isn't visible to others who may
be able to see your screen.

```html
<label for="password">Password: </label>
<input
  type="password"
  id="password"
  name="password"
  placeholder="Password"
/>
```

### Telephone Inputs

Creating an `input` tag with [`type="tel"`][tel] behaves like a text field, but will
bring up the numeric keypad on supported mobile devices.

```html
<label for="tel">Telephone number: </label>
<input id="tel" type="tel" name="phone" placeholder="123-456-7890"/>
```

You can also, optionally, include a `pattern` attribute to validate the phone
number. If the user submits an invalid value, they will receive an error.

### Radio Inputs

[Radio inputs][radio] show users multiple options, but only allow them to select
one. You will set different `value` attributes for each radio button, but they
_must_ have the same `name` attribute. This is how the browser knows that the
radio buttons go together and that a selected option should be de-selected if a
different option is clicked.

```html
<h3>Does your dog get along with other dogs?</h3>
<input type="radio" id="high" name="plays-well-with-others" value="high" />
<label for="high">The more dogs, the better!</label><br />
<input type="radio" id="medium" name="plays-well-with-others" value="medium" />
<label for="medium">It depends on the dog, but generally they are ok</label><br />
<input type="radio" id="low" name="plays-well-with-others" value="low" />
<label for="low">My dog prefers their walkies solo</label>
```

Note that, because each of the options is an `input`, we provide a separate
label for each one.

### Checkbox Inputs

[Checkboxes][checkbox] are like radio buttons... but you can choose more than one.

```html
<h3>What are your dog's favorite toys?</h3>
<input type="checkbox" id="toy-1" name="toy-1" value="kong" />
<label for="toy-1">Kong </label><br />
<input type="checkbox" id="toy-2" name="toy-2" value="stuffed-animals" />
<label for="toy-2">Stuffed Animals</label><br />
<input type="checkbox" id="toy-3" name="toy-3" value="rope-toys" />
<label for="toy-3">Rope Toys</label><br />
<input type="checkbox" id="toy-4" name="toy-4" value="squeaky-toys" />
<label for="toy-4">Squeaky Toys</label><br />
<input type="checkbox" id="toy-5" name="toy-5" value="balls" />
<label for="toy-5">Balls, Frisbees, anything a dog can fetch!</label>
```

### Select Elements

[Select elements][select] create a drop-down menu. Inside the `select` tag you
use `option` tags to create the choices in the menu. The menu label to use for
each choice goes inside the opening and closing `option` tags. The `select`
tag's `name` attribute and the `value` attribute of the option that is selected
are sent in the _Query String_. For example, because the `small` option is
selected in the code below, the _Query String_ would contain `size="small"`.

```html
<h3><label for="size">What size is your dog?</label></h3>
<select id="size" name="size">
  <option value="small" selected>Small (0-25 pounds)</option>
  <option value="medium">Medium (26-50 pounds)</option>
  <option value="large">Large (51-75 pounds)</option>
  <option value="x-large">Extra Large (over 75 pounds)</option>
</select>
```

Note that, in this case, we provide a `label` for the `select` tag.

### Textarea

[Textarea elements][textarea] are useful if we want our users to be able to
write multiple lines of text. For example, if we wish to allow our clients to
write special notes for their dogs, using a `textarea` enables them to write as
much or as little as they like.

```html
<h3><label for="message">Anything else we should know about your dog?</label></h3>
<textarea id="message" name="message"></textarea>
```

### Submit Inputs

Creating an `input` tag with [`type="submit"`][submit] creates a submit button
that, when clicked, will do something with a user's `form` data. The `value`
attribute holds the text that will appear on the button.

```html
<input type="submit" value="Sign me up!" />
```

## Optional Activity - KEEP?

In `index.html`, change the form's `method` to `GET`. Refresh the browser page,
enter information into each of the form's inputs, and click the "Sign me up!"
button.

Were you surprised by what happened? If you were, go back and review the info on
what happens when an HTML form that uses the `GET` method is submitted. Be sure
to take a close look at the page URL as well before you move on.

## Summary

We use HTML `form`s to collect data from users. To create a form, start with a
`form` element and give it an `action` and `method` (most often, `POST`). Inside
the `form` add whichever `input`s and other elements make the most sense for the
data you're requesting. Make sure that all the elements are clearly labeled. If you
follow these guidelines you'll soon be getting all the user data you can handle!

## Resources

- [MDN - HTML - Form](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form)
- [MDN - HTML - Button](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)
- [HTML Goodies - How to Build Forms Part 1](https://www.htmlgoodies.com/html/build-web-forms-html/)
- [HTML Goodies - How to Build Forms Part 2](https://www.htmlgoodies.com/html/building-web-forms-part-2/)
- [W3School - HTML Form Attributes](https://www.w3schools.com/html/html_forms_attributes.asp)
- [HTML Form Generator](http://www.pyform.org/)
- [IANA-managed Reserved Domains](https://www.iana.org/domains/reserved) - KEEP?

[article]: https://www.w3schools.com/html/html_forms_attributes.asp
[form]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form
[input]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input
[text]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text
[label]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label
[pw]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/password
[tel]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel
[radio]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio
[checkbox]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox
[select]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select
[textarea]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea
[submit]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit

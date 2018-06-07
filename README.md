# HTML Forms

## Problem Statement

Up until this point, all of the HTML elements that we've introduced are used to display data to the user. This is great, but what happens when we want to reach out to our users? Websites from personal blogs to business sites increase user inteaction with newsletters, special offers, and exclusive content sent directly to the user. In the next few lessons and labs, you're the owner of a dog walking business that needs a way to keep in contact with current clients, and a way to connect with new clients. 

## Objectives

1. Understand get vs post
2. Familiarization with form elements

## Understanding Get vs. Post

### Forms

Forms are essential for gathering user information from site visitors. As the owner of a dog walking business, you can collect crucial information like owner's name and address, walking frequency, dog names and ages, and other details. Then, a record of their responses can be sent remotely to a server where the information is stored. (We're going to focus on the front-end part of the form submission for now.)

### Form Tag
We will start with the crucial parent element `<form>`. The form element wraps all the input elements that will collect our users' information inside of it. The form element has two important attributes: action, and method. 

The first attribute, `action`, will specify where the user information is sent. This is typically the URL of a remote server. 

The second attribute, `method`, will dictate the manner in which we submit our information. The most common HTTP methods are `GET`, `POST`, `PATCH`, `PUT`, and `DELETE`, but for now we will focus on the most common two for form submissions: `GET` and `POST`.

#### GET

Below we see the form example code for making a `GET` request.

```html
<form action="process-user.php" method="get">
  <input type="text" name="owner-name">
  <input type="text" name="dog-name">
  <input type="text" name="favorite-toy">
  <input type="submit" value="submit">
</form>
``` 

When the user clicks the submit button of our form all their responses are captured and labeled using the name attributes on each element. Then they are sent to the location listed in the action attribute: `process-user.php`. The request uses the method attribute set as `GET`. This causes the information to be sent as a _query string_ (everything after the ?) included into the URL. The URL for our `GET` request looks like this:

![HTTP GET URL](https://curriculum-content.s3.amazonaws.com/html-forms/html-forms-get-request.png)

By looking at the headers of our request in the Developer Tools > Network tab, we can see the request type listed as `get`, and our user's response is located in the Query String Parameters.

![HTTP GET Headers](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-get-headers.png)

An HTTP `GET` request is used when we want to get back particular content from the server and we want to pass it some options to refine the search of what we are getting back from the server. As you can see above, the content of our request is visible in the URL string at the top of the browser window. While this is a great method for things like search, this is not really ideal for passwords, as the people looking over your shoulder at your favorite park might be able to read the contents of what you are sending off your screen.

#### POST

Below we see the same form example code for making a POST request.

```html
<form action="process-user.php" method="post">
  <input type="text" name="owner-name">
  <input type="text" name="dog-name">
  <input type="text" name="favorite-toy">
  <input type="submit" value="submit">
</form>
``` 
When the user clicks the submit button of our form all their responses are captured and labeled using the name attributes on each element. Then they are sent to the location listed in the action attribute in our case `process-user.php` The request uses the method attribute set as `POST`. This causes the information to be sent as _form data_ that is passed along to our process-user.php file. The URL for our post request looks like this:

![HTTP Post URL](https://curriculum-content.s3.amazonaws.com/html-forms/html-forms-post-request.png)

By looking at the headers of our request in the Developer Tools > Network tab, we can see the request type listed as `POST`, and our user's response is tucked into the Form Data.

![HTTP Post Headers](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-post-headers.png)

HTTP `POST` request is ideally used when we wish to post content to the server. This is the more appropriate of the two methods for sending something like a password as the content is sent within Form Data and not directly visible in a query string in the URL as they are with GET requests. Most forms should be set to a `POST` request, unless you specifically want the user to be able to see the query string. 


#### Text Inputs

Setting the input element with a `type="text"` gives our users a place to type in a single line of text content. The `placeholder` attribute puts some dummy text into the element that will be replaced as the user starts typing. The `name` attribute gives our input value a label. This makes it possible to grab its value at the other end on the server by calling up the value by giving its name, also known as a `key`).

```html
<label for="owner-name">Owner Name</label>
<input type="text" name="owner-name" placeholder="Full Name">
```
<label for="owner-name">Owner Name</label>
<input type="text" name="owner-name" placeholder="Full Name">

Generally, HTML form attributes should not contain spaces. Exceptions to this rule are `placeholder` and `class`. If you're not sure whether or not your attribute can contain a space, check out [this article](https://www.htmlgoodies.com/primers/html/article.php/3881421).

##### A Note on Labels
Have you ever been filling out a form that only had placeholder labels, and then totally forgotten what you're supposed to be writing in the box you're filling out? While labels are not strictly necessary on HTML forms, they can increase the usability and accessibility. You'll see labels in several examples here.

#### Password inputs

Setting the input element with a `type="password"` is a special kind of text input. It displays dots as the user types characters, instead of the actual characters. This is useful when private information is entered, so your password isn't displayed for others to see.

```html
<input type="password" name="password" placeholder="Enter your password here">
```

<input type="password" name="password" placeholder="Enter your password here">

#### Telephone inputs

Setting the input element with a `type="tel"` will bring up the numeric keypad on supported mobile devices.

```html
<input type="tel" name="phone" placeholder="Phone Number">
```

<input type="tel" name="phone" placeholder="Phone Number">

#### Hidden Input field

Setting the input element with a `type="hidden"` will send the inserted `value` attributes data along with the form submission, but won't make the data visible in the browser window.

```html
<input type="hidden" name="id" value="UID-99298356982">
```

However, you can see the input field if you inspect the HTML, so be judicious where you use hidden fields. 

#### Submit and Button Tags

Both the submit and button inputs will allow the user to submit the information to your server. They come with different default styling, but generally the same behavior. Without a `submit` or `button` tag with a `type="submit"`, users will not be able to submit their information, and you'll lose a lot of potential clients!

Setting the input element with a `type="submit"` will create a submission button that will submit the form when the user clicks it. The `value` attribute holds the text that will appear on the button.

```html
<input type="submit" value="Let me walk your dog!">
```
<input type="submit" value="Let me walk your dog!">

You can also use a `button` element:

```html
<button type="submit">Time for walkies!</button>
```
<button type="submit">Time for walkies!</button>

With a `button` element, the text that appears on the button goes between the `<button>` and `</button>` tags. Feel free to play around with how buttons are displayed! What happens if you put an image tag in between the button tags?
Note: Remember to set the button tag to `type="submit"`! Some browsers will default to that behavior, but it's unpredictable, so it's better to set the type explicitly. 

#### Radio Inputs

Radio inputs are useful when you want to have several possible options, but only want the user to make one choice. To accomplish this, you set different `value` attributes for each radio button, but they _must_ have the same `name` attribute. 

```html
<h3>Does your dog get along with other dogs?<h3>
<input type="radio" name="plays-well-with-others" value="high"> The more dogs, the better!<br>
<input type="radio" name="plays-well-with-others" value="medium"> It depends on the dog, but generally they are ok<br>
<input type="radio" name="plays-well-with-others" value="low"> My dog prefers their walkies solo<br>
```
<h3>Does your dog get along with other dogs?<h3>
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

Select menus create a drop menu with either single or multiple selectable options. Here the user could choose a single option, so this could be a replacement for a set of radio buttons, or you can allow your user to make multiple selections. Here you assign a text label between the opening and closing option elements as well as a `value` attribute that is the the choice the user selects that will be passed along during form submission. The order that you list your choices in your HTML will be the order they are displayed in the select drop-down.

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

Textarea elements are useful if we want our users to be able to be able to write multiple lines of text. For example, if we wish to allow our clients to write special notes for their dogs, we can let them write as much or as little as they like.

```html
<h3>Any other things we should know about your dog?</h3>
<textarea name="message"></textarea>
```

<h3>Any other things we should know about your dog?</h3>
<textarea name="message"></textarea>


## Summary

There are many options for gathering user input. First, you start with a form element, then give it an action and method. The `POST` method posts content to a server tucking form data within the request, while the `GET` method sends form content as a set of options in the form of a query string visible in the browser's URL bar. When you are gathering form content, make sure that your user experience is clearly laid out and appropriately labeled, and soon you'll have all the clients you can handle!

## Resources

- [HTML Forms and Iframes](https://www.youtube.com/embed/eiCtXc2YMKc?rel=0)
- [Presentation Slides](https://docs.google.com/presentation/d/115ECvsMyDnFBcc-Rvb4Jn876JhOycXxKVN6sv7OiJ1Y/edit?usp=sharing)
- [MDN - HTML - Form](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form)
- [MDN - HTML - Button](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)
- [HTML Goodies - Form Basics](http://www.htmlgoodies.com/primers/html/article.php/3881421)
- [HTML Form Generator](http://www.phpform.org/)
- 
<p class='util--hide'>View <a href='https://learn.co/lessons/HTML-Forms-and-iFrames'>HTML Forms and iFrames</a> on Learn.co and start learning to code for free.</p>

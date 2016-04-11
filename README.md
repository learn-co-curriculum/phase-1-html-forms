# HTML Forms and Iframes

## Overview

In this lesson we will learn how to use HTML form elements to gather user input. We will also learn about using iframe elements to load other HTML content windows in our page.

## Objectives

1. Understand form elements get and post differences.
2. Familiarization with form elements.
3. A look at iframe code.

## Gathering User Input

<iframe width="640" height="480" src="//www.youtube.com/embed/eiCtXc2YMKc?rel=0" frameborder="0" allowfullscreen></iframe>

*Note: Slides for this lecture video are provided in the resources at the bottom of this lesson.*

### Forms

Forms are essential for gathering user information from site visitors. Text can be inserted, selections made and a record of their responses can be sent remotely to a server whose backend can store the information. At this time we will not be going into detail about the back-end portion of a form submission, but instead focusing on the front-end portion. Let's explore some of the many form elements we have at our disposal for gathering user input.

We will start with the crucial parent element `<form>`. The form element wraps all the input elements that will collect our user information inside of it. The form element has two important attributes: action, and method. The `action` attribute will specify where the user information is sent to. This is typically the URL of a remote server. The second attribute is the `method` which will dictate the manner in which we submit our information. The most common HTTP methods are `GET`, `POST`, `PATCH`, `PUT`, and `DELETE` but for now we will focus on the most common two for form submissions `GET` and `POST`.

#### GET

Below we see the form example code for making a GET request.

```html
<form action="process-user.php" method="get">
  <input type="text" name="full-name">
  <input type="password" name="password">
  <input type="submit" value="submit">
</form>
``` 

When the user clicks the submit button of our form all their responses are captured and labled using the name attributes on each element. Then they are sent to the location listed in the action attribute in our case `process-user.php` The request uses the method attribute set as `get`. This causes the information to be sent as a Query String included into the URL. The URL for our GET request looks like this,

![HTTP Get URL](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-get-url.png)

By looking at the headers of our request in the Developer Tools > Network tab, we can see the request type listed as GET, and our users responses is located in Query String Parameters.

![HTTP Get Headers](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-get-headers.png)

HTTP Get request is used when we want to get back particular content from the server and we want to pass it some options to refine the search of what we are getting back from the server. Since the content of our request is visible in the URL string at the top of the browser window, this is not really ideal for passwords, as the people looking over your shoulder at your favorite cafe might be able to read the contents of what your sending off your screen.

#### POST

Below we see the same form example code for making a POST request.

```html
<form action="process-user.php" method="post">
  <input type="text" name="full-name">
  <input type="password" name="password">
  <input type="submit" value="submit">
</form>
``` 
When the user clicks the submit button of our form all their responses are captured and labled using the name attributes on each element. Then they are sent to the location listed in the action attribute in our case `process-user.php` The request uses the method attribute set as `post`. This causes the information to be sent as Form Data that is passed along to our process-user.php file. The URL for our post request looks like this,

![HTTP Post URL](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-post-url.png)

By looking at the headers of our request in the Developer Tools > Network tab, we can see the request type listed as POST, and our users responses is tucked into the Form Data.

![HTTP Post Headers](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-post-headers.png)

HTTP Post request is ideally used when we wish to post content to the server. This is the more appropriate of the two methods for sending something like a password as the content is sent within Form Data and not directly visible in a query string in the URL as they are with GET requests.

Next, let's explore some of the many form elements we can use to gather user input.

#### Text Inputs

Setting the input element with a `type="text"` gives our user a place to type in a single line of text content. The `placeholder` attribute puts some dummy text into the element that will be replaced as the user starts typing. The `name` attribute gives our input value a label. This makes it possible to grab its value at the other end on the server by calling up the value by giving its name (key).

```html
<input type="text" name="username" placeholder="username">
```

<input type="text" name="username" placeholder="username">

Setting the input element with a `type="password"` displays dots as the user types characters instead of the actual characters. This is useful when private information is entered that we do not want others around the user to read.

```html
<input type="password" name="password" placeholder="password">
```

<input type="password" name="password" placeholder="password">

Setting the input element with a `type="tel"` will bring up the numeric keypad on supporting mobile devices.

```html
<input type="tel" name="phone" placeholder="phone">
```

<input type="tel" name="phone" placeholder="phone">

#### Hidden Inputs

Setting the input element with a `type="hidden"` will send the inserted `value` attributes data along with the form submission, but won't make the data visible in the browser window.

```html
<input type="hidden" name="id" value="UID-99298356982">
```

#### Submit Buttons

Setting the input element with a `type="submit"` will create a submission button that will submit the form upon clicking it. The `value` attribute holds the text that will appear on the button.

```html
<input type="submit" value="submit">
```

<input type="submit" value="submit">

#### Radio Inputs

Radio inputs are useful when you want to have several possible values but wish to limit the user to choosing one or another. To accomplish this we must set different `value` attributes for each radio button, but they must share the same `name` attribute. 

```html
<input type="radio" name="gender" value="male"> Male <br>
<input type="radio" name="gender" value="female"> Female
```

<input type="radio" name="gender" value="male"> Male 
<input type="radio" name="gender" value="female"> Female

#### Checkboxes 

Checkboxes are ideal if we wish to allow our user to choose one, another, or both values.

```html
<input type="checkbox" name="vehicle-1" value="bike"> Bike <br>
<input type="checkbox" name="vehicle-2" value="car"> Car
```

<input type="checkbox" name="vehicle-1" value="bike"> Bike 
<input type="checkbox" name="vehicle-2" value="car"> Car

#### Select Menus

Select menus create a nice drop menu which multiple selectable options. Here the user must also choose a single option, so this could be a replacement for a set of radio buttons. Here we must assign a text lablel between the opening and closing option elements as well as a `value` attribute that will hold the choice the user selects that will be passed along during form submission.

```html
<select name="size">
  <option value="small" selected>small</option>
  <option value="medium">medium</option>
  <option value="large">large</option>
</select>
```

<select name="size">
  <option value="small" selected>small</option>
  <option value="medium">medium</option>
  <option value="large">large</option>
</select><br>

#### Textarea

Textarea elements are useful if we wish to allow our user to insert multiple lines of text, for example if we wish to gather feedback that requires they can type as much or as little a response as they like.

```html
<textarea name="message"></textarea>
```

<textarea name="message"></textarea>

### Iframes

Iframe elements allow us to link to other HTML content from within a frame window on our pages. The `src` attribute points to the location of other html content elsewhere and display it within the current page.

```html
<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d335994.89219194185!2d2.0673752159642937!3d48.8589713267984!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47e66e1f06e2b70f%3A0x40b82c3688c9460!2sParis%2C+France!5e0!3m2!1sen!2sus!4v1457911182825" width="600" height="450" frameborder="0" style="border:0" allowfullscreen></iframe>
```

<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d335994.89219194185!2d2.0673752159642937!3d48.8589713267984!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47e66e1f06e2b70f%3A0x40b82c3688c9460!2sParis%2C+France!5e0!3m2!1sen!2sus!4v1457911182825" width="600" height="450" frameborder="0" style="border:0" allowfullscreen></iframe>

## Summary

- There are many options for gathering user input.
- We can start with a form element and give it an action and method.
- The POST method posts content to a server tucking form data within the request.
- The GET method sends form content as a set of options in the form of a query string visible in the browsers URL bar. The purpose is to describe to the server options for the content you wish to get back.
- We can use an iframe element to display other HTML documents inside a frame within our own HTML document.

## Resources

- [Presentation Slides](https://docs.google.com/presentation/d/115ECvsMyDnFBcc-Rvb4Jn876JhOycXxKVN6sv7OiJ1Y/edit?usp=sharing)
- [MDN - HTML - Form](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form)
- [MDN - HTML - Iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)
- [HTML Goodies - Form Basics](http://www.htmlgoodies.com/primers/html/article.php/3881421)
- [HTML Form Generator](http://www.phpform.org/)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/HTML-Forms-and-iFrames' title='HTML Forms and Iframes'>HTML Forms and Iframes</a> on Learn.co and start learning to code for free.</p>

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/HTML-Forms-and-iFrames'>HTML Forms and iFrames</a> on Learn.co and start learning to code for free.</p>

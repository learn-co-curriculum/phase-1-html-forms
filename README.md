# HTML Forms and Iframes

## Overview

In this lesson we will learn how to use HTML form elements to gather user input. We will also learn about using iframe elements to load other HTML content windows in our page.

## Objectives

1. ...

## ...

<iframe width="640" height="480" src="//www.youtube.com/embed/eiCtXc2YMKc?rel=0" frameborder="0" allowfullscreen></iframe>

*Note: Slides for this lecture video are provided in the resources at the bottom of this lesson.*

### Forms

Forms are essential for gathering user information from site visitors. Text can inserted, slections made and a record of their responses can be sent remoetly to a server whose backend can store the information. At this time we will not be going into detail about the back-end portion of a form submission, but instead focusing on the front-end portion. Let's explore some of the many form elements we have at our disposal for gathering user input.

We will start with the crucial parent element `<form>`. The form element wraps all the input elements that will collect our user information inside of it. The form element has two important attributes: action, and method. The `action` attribute will specify where the user information is sent to. This is typically the URL of a remote server. The second attribute is the `method` which will dictate the manner in which we submit our information. The most common HTTP methods are `GET`, `POST`, `PATCH`, `PUT`, and `DELETE` but for now we will focus on the most common two for form submissions `GET` and `POST`.

#### POST

```html
<form action="process-user.php" method="post">
  <input type="text" name="full-name">
  <input type="password" name="password">
  <input type="submit" value="submit">
</form>
``` 

![HTTP Post URL](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-post-url.png)

![HTTP Post Headers](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-post-headers.png)

#### GET

```html
<form action="process-user.php" method="get">
  <input type="text" name="full-name">
  <input type="password" name="password">
  <input type="submit" value="submit">
</form>
``` 

![HTTP Get URL](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-get-url.png)

![HTTP Get Headers](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/http-get-headers.png)

#### Text Inputs

...

#### Radio Inputs

...

#### Checkboxes 

...

#### Select Menus

...

#### Textarea

...

#### Submit Buttons

...

### Iframes

...

## Summary

- ...

## Resources

- [Presentation Slides](https://docs.google.com/presentation/d/115ECvsMyDnFBcc-Rvb4Jn876JhOycXxKVN6sv7OiJ1Y/edit?usp=sharing)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/HTML-Forms-and-iFrames' title='HTML Forms and Iframes'>HTML Forms and Iframes</a> on Learn.co and start learning to code for free.</p>

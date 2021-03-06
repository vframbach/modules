# <img src="https://cloud.githubusercontent.com/assets/7833470/10423298/ea833a68-7079-11e5-84f8-0a925ab96893.png" width="60"> HTML5 Forms

| Objectives |
| :--- |
| Explore HTML Forms and Inputs |
| Understand the difference between a `method` and an `action` |
| Create forms that utilize parameters |

### An Example `<form>` Element (Tag)

```html
<form method="POST" action="/pages">
  <label for="name">Page Name</label>
  <input id="name" type="text" name="page_name" />
  <input type="submit" value="Create" />
</form>
```

#### Attributes

In the opening of the `<form>` tag you can see two attributes: `method` & `action`

- **method**: the HTTP verb (method) that the browser uses to submit the form.
- **action**: the path of the HTTP request page that processes the information submitted via the form.

>A `route` is simply a combination of a method & action. For example `GET '/pages/1'` or `POST '/users'` are both valid routes.

>For now simply understand that it is convention for <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3" target="_blank">GET</a> to be used in a request when the client wants to receive data, and for <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.5">POST</a> to be used in a request when the client wants to send data.

**Client / Server Model**

![client/server](https://mdn.mozillademos.org/files/4291/client-server.png)

### The `<label>` Element (Tag)

The `<label>` element is the formal way to define a label for an HTML form widget.
"This is the most important element if you want to build accessible forms." *— MDN*

There are two ways to use labels correctly:

```html
<!-- Simple (nested) label example -->
<label>Click me
  <input type="text" id="user" name="name" />
</label>

<!-- Using the "for" attribute with the input's id -->
<label for="user">Click me</label>
<input id="user" type="text" name="name" />
```

#### `<label>`'s Attributes

* The `for` in a label references an `<input>`'s `id` attribute, not it's `name` attribute! Sometimes these values will be the same, but `for` always is matched with `id`.

* The `name` is the `key` of the `<input>`'s value when data is sent.

## Common Inputs

| Field Type | HTML Code | Widget (Control) | Notes |
|:-- |:-- |:-- |:-- |
| plain text | `<input type="text">` | ![<input type="text">][text] | the type attribute can be omitted |
| password field | `<input type="password">` | ![<input type="password">][text] | echoes dots instead of characters |
| text area | `<textarea></textarea>` | ![<textarea></textarea>][area] | a more customizable plain text area |
| checkbox | `<input type="checkbox">` | ![<input type="checkbox">][check] | can be toggled on or off |
| radio button | `<input type="radio">` | ![<input type="radio" name="group"> <input type="radio" name="group">][radio] | can be grouped with other inputs |
| drop-down lists | `<select><option>` | ![<select><option>Option 1</option><option>Option 2</option></select>][select] | [check here for more info](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) |
| file picker | `<input type="file">` | ![<input type="file">][file] | pops up an “open file” dialog |
| hidden field | `<input type="hidden">` |  | nothing there!
| submit button | `<input type="submit">` | ![<input type="submit">][submit] | activates the form's submission <br/>(a `POST` request or <br/>Javascript action) |

<!-- Images -->
[text]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-text.png
[area]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/textarea.png
[check]:  https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-checkbox.png
[radio]:  https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-radio.png
[select]: https://raw.github.com/h4w5/html_form_cheatsheet_images/master/select-option.png
[file]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-file.png
[submit]: https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-submit.png

### Important Attributes

**All input types (including `<textarea>`s):**

- **`type`**: the type of data that is being input (affects the "widget" that is used to display this
  element by the browser).
- **`name`**: the key used to describe this data in the HTTP request.
- **`id`**: the unique identifier that other HTML elements, JavaScript and CSS use to access this
  element in the browser.
- **`value`**: the default data that is assigned to the element.
- **`placeholder`**: not a default value, but a useful HTML5 addition of a data "prompt" for an input.
- **`autofocus`**: defaults the cursor to a specific input when the page originally loads. You can only have one autofocus on your page.
- **`disabled`**: a Boolean attribute indicating that the "widget" is not available for interaction.

**Radio buttons or checkboxes:**

- **`checked`**: a Boolean that indicates whether the control is selected by default (is false unless).
- **`name`**: the group to which this element is connected. For radio buttons, only one element per
  group (or name) can be checked.
- **`value`**: the data or value that is returned for a specific group (a multi-element control), if
  this element is checked.

## Common Validations

Validations avoids having users submit bad data to our application. Knowing how to use them will save time and make your app a lot more usable.

Bad data could be anything from a required field being empty, an email address that was mistyped, or a password confirmation that doesn't match. Thankfully, HTML forms give us simple out-of-the-box validations for these common situations.

(Note: This is NOT supported in Safari (including on iOS). A good alternative to this is <a href="http://jqueryvalidation.org/" target="_blank">jQuery validate</a>.)

### Required

Try submitting the below form without entering your name:

```html
<form>
  <label for="colorField">What is your favorite color?</label>
  <input id="colorField" name="favColor" required>
  <button>Submit</button>
</form>
```
Notice the `required` attribute on the input. Therefore, the form will not submit until some information is entered into the field.

### Pattern matching

```html
<form>
  <label for="kindOfBob">Do you go by bob or bobert?</label>
  <input id="kindOfBob" name="bobType" pattern="bob|bobert" required>
  <button>Submit</button>
</form>
```

The `pattern` attribute allows us to specify the values we will accept. In this case only `bob` or `bobert` are acceptable.

### Length

You may need the user to enter a specific amount of characters. Let's say you need a username to be at least 6 characters. You can use the `minlength` or `maxlength` attributes to help.

```html
<form>
  <label for="userName">What's your username?</label>
  <input id="userName" name="userName" minlength="6" required>
  <button>Submit</button>
</form>
```


### Challenges

For the following exercises, please ONLY use html.

**Login Form.** Create an html form with two inputs: one for a username (named "username"), the other for password (named "password") (normally you don't see your password when you type it, so make sure it's blocked out!). What happens when you click submit?

**Doomed Yet?** Create an html form that, on submit, sends the user to "hasthelargehadroncolliderdestroyedtheworldyet.com". Hint: what's the form action? Bonus: Can you change the submit button to say "Are we doomed?".

**Color Search.** Create an html form that contains the html5 color-picker input (named "q"). When the user picks a color and clicks submit, redirect them to, e.g. "https://duckduckgo.com/?q=%2300fa91".

**Image Search.** Create an html form that has an action of "https://www.google.com/search" and contains three inputs:

 * a hidden input with a name of "tbm" and a value of "isch".
 * a (required) text input with a name of "q", and a default value of "http status cats".
 * a submit button

You should end up here: "https://www.google.com/search?tbm=isch&q=http+status+cats"

**Movie Search.** Create an html form that searches for movies on the OMDB API by title and by year. You will need to take care to use the correct query parameters. The only way to find out what they are is to read their documentation.

**Stretch:** Return of the Movie Search. It's great that we can find find data about movies using the Open Movie Database, but it's not very helpful having all that data somewhere else. It would be awesome if we could "pull in" that data and use it on our webpage. It's time to learn about AJAX! Your goal is to figure out how to use jQuery's get method to request information (JSON) about the movie "Primer". Can you console.log the movie description? HINT: start by hitting the endpoint directly, then figure out how to "drill down" through the json object to get to the data you want.

## Further Reading (optional)

MDN has a number of exhaustive resources on HTML forms and inputs. It can be a lot to absorb, so look for patterns and try to grasp the big picture.

* <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms" target="_blank">HTML Form Reference</a> is a great resource and has been distilled below.
* <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input" target="_blank">HTML Input Reference</a>
* <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/The_native_form_widgets">Native Form Widgets</a>
* <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Data_form_validation" target="_blank">Form Validation</a>

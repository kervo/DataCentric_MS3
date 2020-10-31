<img src="https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png" style="margin: 0;">

Deployed project: https://wondercook-book.herokuapp.com/

# WonderCook Data Centric Milestone 3 Project

# UX Practices

My colour scheme for Materialize: pink-text text-darken-4

The fontawesone icons use in this application are food related as this is a recipes database.

To make it easier for users to log into their profile's section, email has been removed from the credentials.

In order to have a nice centred panel on *register.html* we need to use `<div class="col s12 m8 offset-m2">` where offset-m2 would push the card two spaces to the left.

* Using fontawesone icons:
`<i class="fas fa-key prefix"></i>` PREFIX class allows the fontawesone icon to be displayed as part of the text.

# Software Development Practices:

* The Structure

Index
```
|—Log in
---| <user> <session>
---| Dashboard
        |—Search recipes <recipe>
        |—Add Recipe
        |—Edit a recipe
        |—Delete a recipe
        |—Log out <session>

|— register
    <username>, <email>, <password>



|—Index with random recipes <random>
```

To create the folders on the command line:
`mkdir templates`

For this project we used MATERIALIZE: https://materializecss.com/getting-started.html

In order to add a nice margin around the content, on the base.html file is important to have this structure:

```<div class="container">
      {% block content %}
      {% endblock %}
</div>
```

## Testing
### "password": generate_password_hash(request.form.get("password"))
* Problem: TypeError: a bytes-like object is required, not 'NoneType'.
* Solution: password input field wasn't correctly marked as `type="password"` and it wasn't marked as required which causes error with the Werkzeug package.

### jinja2.exceptions.UndefinedError: 'get_flasehd_messages' is undefined
* Solution: typo

### Defensive coding

```<input id="username" name="username" type="text" minlength="5" maxlength="20" pattern="^[a-zA-Z0-9]{5,20}$" class="validate" required>```

This piece of code shows that minimum characters are five, maximum 20 and the alpha numberic only. Any exception will be flashed.

### 127.0.0.1 - - [30/Oct/2020 08:00:55] "GET /login HTTP/1.1" 200 - 127.0.0.1 - - [30/Oct/2020 08:01:14] "POST /register HTTP/1.1" 302 -
I was getting redirected to the login page with its flash messages, my Log in page was taken action to POST on the register function rather that the login function.

### pymongo.errors.InvalidOperation: cannot set options after executing query
Calling information `{{ recipes.recipe_name }}` from the data base added on a template after the `{% endfor %}`

## Deployment on the command line

`pip3 freeze --local > requirements.txt`

Procfile file for Heroku app running:

`web: python app.py`

To wireup Flask and MongoDB:

`pip3 install flask-pymongo`

`pip3 install dnspython`


# References

## Images
All images taken from PEXELS https://www.pexels.com/

## Gitpod

* Beautify indentation: https://community.gitpod.io/t/indentation-with-alt-shift-f/1030

* Materialize Styling: https://materializecss.com/

<img src="https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png" style="margin: 0;">

Deployed project: https://wondercook-book.herokuapp.com/

# WonderCook Data Centric Milestone 3 Project

# UX Practices

In order to have a nice centred panel on *register.html* we need to use `<div class="col s12 m8 offset-m2">` where offset-m2 would push the card two spaces to the left.

* Using fontawesone icons:
`<i class="fas fa-key prefix"></i>` PREFIX class allows the fontawesone icon to be displayed as part of the text.

# Software Development Practices:

* The Structure

Index
```
|—Log in
---| <user> <session>
|—Sign up
  |——-Dashboard
  |—Search recipes <recipe>
  |—Add Recipe
  |—Edit a recipe
  |—Delete a recipe
  |—Log out <session>

|—Index with random recipes <random>
```

To create the folders on the command line:
`mkdir templates`

For this project we used MATERIALIZE:

https://materializecss.com/getting-started.html

In order to add a nice margin around the content, on the base.html file is important to have this structure:
```
<div class="container">
      {% block content %}
      {% endblock %}
</div>
```

## Testing
### "password": generate_password_hash(request.form.get("password"))
* problem: TypeError: a bytes-like object is required, not 'NoneType'

## Deployment on the command line

`pip3 freeze --local > requirements.txt`

Procfile file for Heroku app running:

`web: python app.py`

To wireup Flask and MongoDB:

`pip3 install flask-pymongo`

`pip3 install dnspython`

Another blue button should appear to click: *Open Browser*.

In Gitpod you have superuser security privileges by default. Therefore you do not need to use the `sudo` (superuser do) command in the bash terminal in any of the backend lessons.

# References

## Gitpod

* Beautify indentation: https://community.gitpod.io/t/indentation-with-alt-shift-f/1030

![Final Front Page](https://github.com/kervo/DataCentric_MS3/blob/master/static/img/wondercook-frontpage.png)

Deployed project: https://wondercook-book.herokuapp.com/get_recipes

# WonderCook Data Centric Milestone 3 Project

# UX Practices
<img src="https://github.com/kervo/DataCentric_MS3/static/img/wireframe-user stories.png" style="margin: 0;">

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

```python
<div class="container">
      {% block content %}
      {% endblock %}
</div>
```
* The Categories
The main problem at the moment is displaying the meal type on from the select list. I have it in MongoDB as an array, I think the best is to have them as different entries in a collection so the can have the same key value of "meal_time".

### Handling errors
Loading the page for the first time and click on the *ME* link without starting a session was throwing a 404 error, the best practice is to ask the users to log in.
```html
{% if session.user|lower == recipes.wonderchef|lower %}
```

## Testing

### Problem: "password": generate_password_hash(request.form.get("password"))
* Message: TypeError: a bytes-like object is required, not 'NoneType'.
* Solution: password input field wasn't correctly marked as `type="password"` and it wasn't marked as required field which causes error with the Werkzeug package.

### Problem: jinja2.exceptions.UndefinedError: 'get_flasehd_messages' is undefined
* Solution: typo

### Problem: jinja2.exceptions.UndefinedError: 'recipe' is undefined
* Solution: Edit_recipe section was throwing this error, I had to link my edit function `recipe_id` with the actual collection on the data base `recipes`
Wrong code:
```html
<a href="{{ url_for('edit_recipe', recipe_id=recipe._id) }}
```
Correction:
```html
<a href="{{ url_for('edit_recipe', recipe_id=recipes._id) }}
```
### Problem: raise ValueError('update only works with $ operators')
* Solution: `.update()` for mongo.db.recipes.update_one({"_id": ObjectId(recipe_id)}, edit_recipe)

# Defensive Design 
### Denied access to functions and links if is not a user:
```html
{% if session.user|lower == recipes.wonderchef|lower %}
```
This codes will allow to use certain functions and links when users log in.

### 404 Errors
```python
@app.errorhandler(404)
def not_found(e):
    return render_template("404.html")
```
This piece of code simply redirects to the logic page for any 404 errors that may occur on a user's session.

```html
<input id="username" name="username" type="text" minlength="5" maxlength="20" pattern="^[a-zA-Z0-9]{5,20}$" class="validate" required>
```

This piece of code shows that minimum characters are five, maximum 20 and the alpha numberic only. Any exception will be flashed.

### Problem: 127.0.0.1 - - [30/Oct/2020 08:00:55] "GET /login HTTP/1.1" 200 - 127.0.0.1 - - [30/Oct/2020 08:01:14] "POST /register HTTP/1.1" 302 -
* Solution: I was getting redirected to the login page with its flash messages, my Log in page was taken action to POST on the register function rather that the login function.

### pymongo.errors.InvalidOperation: cannot set options after executing query
Calling information `{{ recipes.recipe_name }}` from the data base added on a template after the `{% endfor %}`

### IndexError: no such item for Cursor instance
Problem to call values from array into `<select>` list on my add_recipe function.

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


## Pymongo
* https://stackoverflow.com/questions/12345387/removing-id-element-from-pymongo-results

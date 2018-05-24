
# RESTful Flask App with JSON Lab

## Introduction
In this lab, we will practice creating a RESTful flask app. In programming we talk a lot about convention and the importance to adhering to a convention. Usually we talk about naming variables and functions appropriately descriptive so that our code is easier to maintain by us and other developers. In this lab we will be focusing on the REST convention. We will adhere to the REST principals and create an application that can take requests from and return information to the client. We will see how REST makes it easier to find resources accross different applications as well as scale our own application. 

## Objectives
* Understand what is rest
* Build RESTful routes that return JSON data
* Build RESTful routes that return HTML

## What is REST?
What does RESTful mean? REST stands for **Re**presentational **S**tate **T**ransfer. REST provides standards or conventions between computer systems which make it easier to communicate accross systems. RESTful systems also are characterized by a separation of concerns for client and server. Basically, we design what the client consumes separate from what the server does. So, we can make changes to our client's view without affecting how the server operates. Another key element of a RESTful system is that they are stateless. Meaning the server does not need to know anything about the client or what *state* the client is in to complete a request. This way both client and server can understand any messages without knowledge of previous messages.

If all of this sounds a little confusing don't worry. It will make more sense as we learn more about web applications. But the most important take away from REST is that it provides a convention for creating URLs that represent access to an application's specific **resources**. This makes it easier to scale an application as well as facilitates easier and more predictable communication between different applications. 

## Building RESTful Routes

### Returning JSON

Now that we have a better idea of what REST means, let's put it to practice. We already have an app started for us in our app.py file, and we have a couple templates set up for us as well. We're importing some data from a pictures.py file, which contains a list of dictionaries with information about various pictures. We will use this as our data that we return to our client.

So, in our app, Pictures will be our main **resource** and we will want to start out by returning information about these pictures. We will follow the pattern of prepending `/api/` to our routes. This format not only differentiates the routes that return date from the routes that return our HTML, it also visually indicates that we are requesting data from our  from 

Below are a list of routes we will want to define: 

```python
"/api/pictures" 
# returns a list of all pictures
```

```python
"/api/pictures/<int:id>" 
# returns a single picture whose ID matches the ID from the URL
```
> **Note:** Our variable is still referred to as `id` in the function that follows the route, but by putting `int:` before our variable `id`, we are telling the route to expect an interger. This serves two purpopses; it differentiates the route from other routes that may expect a string as an param in our URL, and it ensures that when we pass the `id` variable to our function, it comes through as an interger instead of a string. 

What if we wanted our API to also return pictures by country? It seems like someone using our app might want to see all pictures by country instead of just getting all picutres or a single picture by it's ID. Let's define the following route and have it return a list of dictionaries where the country matches the country in our URL.

```python
"/api/pictures/<country>" 
# returns a list of dictionaries whose country matches the country from the URL
# hint: remember to compare these strings without case sensitivity
```

### Returning HTML

Okay, now that we have our API set up and returning to us the data we want, let's put it to use! You'll notice that our app already has some templates set up for us. Let's define some RESTful routes that render the appropriate HTML templates for both a single Picture object as well as a list of picture objects. To retrieve the data we will need to pass to the templates, we will use the API routes we just defined. 

To do this, we will need to import the `requests` module and in our app.py file and use the requests module to 'get' our data from our API routes. Once we get the data back from our other routes, we need to coerce it from a response object into JSON so that our templates will be able to display the data. Below is an example of how we would retrieve the data for a list of all picture objects.

```python
pictures = requests.get('http://localhost:5000/api/pictures')
pictures_json = pictures.json()
```

Once we have coerced our response object into JSON data we can pass it along to our render_template function and our data should display when we visit the provided routes!

> **Note:** Look carefully at how the templates are expecting the data to be formatted. 

We will want three RESTful routes that return HTML for us:
* Returns page with a list of all pictures
* Returns a page with a single picture by its `id`
* Returns a page with a list of pictures by `country` 

> **Note:** These will follow a similar pattern to our API routes, however these routes will not be prepended with '/api/' since they will be returning HTML instead of JSON data.

Once we have all of our routes defined, visit them in the browser to see them working! 

# Summary

Great work! In this lab we practiced building a RESTful web application. We designed our URLs to act as resources so that if we wanted all pictures our URL would start with `/api/pictures` and if we wanted something more specific like the the pictures from the USA, our URL would become `/api/pictures/usa`. We were then able to use these URLs to get the data for our pictures and extrapolate our RESTful pattern to then return HTML for our pictures as well. We can see that having a convention to follow for defining routes makes it not only easier to scale our application but also to communicate between the front-end and back-end of our application too. 

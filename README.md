## Google App Engine Review
You will use these files (which you should have created on Day 6) to learn more about Google App Engine. Specifically, we will spend today learning how to make our templates dynamic by adding logic and passing and reading variables.

Let's break down each part of our controller, in this case helloworld.py

```python
import jinja2
import os
import webapp2
```

This is where we import our libraries. 
* Jinja2 is our templating library. 
* OS allows us to access our machine to decide our local directory.
* Webapp2 is the framework that allows us to easily build all three parts of our MVC.

```python
jinja_environment = jinja2.Environment(loader=
    jinja2.FileSystemLoader(os.path.dirname(__file__))) 
```
This line is doing a lot. In Python, __file__ is a special variable that indicates the current file, in this case, helloworld.py. This line opens the directory (dirname) that our templates are in. Then when we call jinja2.Environment, we are telling our code how we want to load those templates (by using Jinja!)

```python
class HelloHandler(webapp2.RequestHandler):
	def get(self):
		template = jinja_environment.get_template('templates/hello.html')
		self.response.out.write(template.render())
```
This is the heavy-hitter of our code, our handler. Each handler is a class  with one or more methods that runs to handle the request and generate a response. In this case,  HelloHandler is set up to handle get requests. The response could be any python code t it's your job as the developer to tell the handler how to respond.  In our example, our handler responds by rendering the hello.html template. 

```python
routes = [  ('/.*', HelloHandler),]
```
In this line of code, we set up our routes, the * means that ALL urls will route to the HelloHandler.


```python
app = webapp2.WSGIApplication(routes, debug=True)`
```
Finally, we make sure that we use the WSGIA app, which helps our web server interact with or app. WSGIA is beyond the scope of our class, but feel free to learn more [here](http://www.fullstackpython.com/wsgi-servers.html). 

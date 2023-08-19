### Conceptual Exercise

Answer the following questions below:

- What are important differences between Python and JavaScript?
-Javascript is used for both front-end and back-end development, whereas Python is used for back-end devleopment. Python is used in a wide variety  of scientific applications (AI, machine learning, data science, etc.) while JS is used primarily for web development, servers, and the user-facing side. Python uses block code (indentation) to specify pieces of code whereas JS uses curly braces {}. Javascript uses camel casing (firstZero) and Python uses snake casing (first_zero). To define variables in JS you use let x = 10, in Python you just say x = 10. For immutable constants in Python the naming style is to use all capital letters with an underscore separating the words. In JS we out the letters const in front of the vairable name. Number data in Python is either int(integer), float(floating point number-whole num w decimal), or complex (real number & imaginary number). JS's numeric types are number (floating type not integer) or BigInt. JS uses null, whereas Python uses None. For non code comments, JP uses // and Python uses #. Python has tuples which are a data strcture similar to a list in JS , but are immutable. The equivalent of a JS array is a Python list. For output JS uses console.log() whereas Python uses print(). In Python ":" is used after the else statement. In JS we use else if, whereas in Python we use elif. For loops look a bit different--Python-- for i in range(n): --JS-- for(let i =0; i ,n; i++{}). For defining functions Python uses, ex. def countZeroes whereas JS uses ex. function countZeroes.

- Given a dictionary like ``{"a": 1, "b": 2}``: , list two ways you
  can try to get a missing key (like "c") *without* your programming
  crashing.
  
  thisdict = {"a": 1, "b": 2}
  
  answer1 = thisdict.get("c")
  if answer1 is None:
  	print("Key 'c' does not exist")
  	
  try:
  	answer2 = thisdict["c"]
  except KeyError:
  	print("Key 'c' does not exist")
  
- What is a unit test?
-Unit tests ask if an individual function or method works. Unit tests do not test the integration of components. You can use assert as a way to expect a certain condition to be true in your code. If the condition is not true it will raise an exception and the code will exit. You can use Python built in testing framework "unittest" which can be used for both unit tests and integrations tests. We define our tests inside of special classes that we define. These test classes are typically written in a separate file from the code we are testing. (From unittest import TestCase, class OurFirstTest(TestCase):, def test_adder(self):, assert arithmetic.adder python -m unittest NAME_OF_FILE)


- What is an integration test?
-Integrations tests test that components work together. Used to test our Flask applications. We do not have to run the server to test. We make requests to Flask using client, ex.: 
from app import app
from unittest import TestCase
class ColorViewsTestCase(TestCase):

    def test_color_form(self):
        with app.test_client() as client:
        	response = client.get('/')
        	html = res.get_data(as_text=True)
        	
        	self.assertEqual(res.status_code, 200)
        	self.assertIn('<h1>Color Form</h1>', html)
        
- What is the role of web application framework, like Flask?
-Flask is used to develop web application using Python (a Python module). Frameworks contain a set of predefined classes, modules, and libraries that makes the programming of an application easier. 

- You can pass information to Flask either as a parameter in a route URL
  (like '/foods/pretzel') or using a URL query param (like
  'foods?type=pretzel'). How might you choose which one is a better fit
  for an application?
-You would probably want to choose a URL parameter for something that seems more like a subject of a page and a query parameter in something like a form that may be used to sort/filter extra info.

- How do you collect data from a URL placeholder parameter using Flask?
-
from flask import Flask, request
app = Flask(__name__)

//define a route with the URL parameter//


- How do you collect data from the query string using Flask?
-Use the request object. The query string is what comes after the question mark in a URL. 

ex.
from flask import request

@app.route("/search")
def search():
    """Handle GET requests like /search?term=fun"""

    term = request.args["term"]
    return f"<h1>Searching for {term}</h1>"

- How do you collect data from the body of the request using Flask?
-You can use the request.data attribute or request.json (if you need to parse JSON data from body).

from flask import Flask, request, jsonify
app = Flask(__name__)

@app.route("/example-json")
def example_json_route():
    """Return some JSON."""

    info = {"name": "Whiskey", "cute": "Hella"}
    return jsonify(info)

    # Alternate syntax
    # return jsonify(name="Whiskey", cute="Hella")

- What is a cookie and what kinds of things are they commonly used for?
-Cookies are name/string-value pairs of information stored on the client's browser (makes http stateful). Cookies are commonly used to save infomration like what is in your shopping cart on a site, what pages your have viewed, time spent on on a page, where you hovered, etc. Unlike local storage, cookie info is sent via a request header and on server side the server can receive that data. Server responds accordingly to the cookie.

- What is the session object in Flask?
-A feature within Flask that requires less code and fixes some issues with cookies. Can add info in and get info from cookies-a "magic dictionary" without any conversion from a string. Contains info from current browser, preserve type (list stays a list, etc), are "signed" so users can't modify data (safer). 
 
	from flask import Flask, session

	app = Flask(__name__)
	app.config["SECRET_KEY"] = "SHHHHHHHHHHH SEEKRIT"
	
	@app.route('/some-route')
	def some_route():
    """Set fav_number in session."""

    	session['fav_number'] = 42
    	return "Ok, I put that in the session."

- What does Flask's `jsonify()` do?
-A function used to create JSON response objects. You pass a Python dictionary (or other JSON serialized object) to jsonify() and it gets converted into a JSOn formatted response. This process can be very helpful in creating APIs.

from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/data')
def get_json_data():
    data = {"key": "value"}
    response = jsonify(data)
    return response

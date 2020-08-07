---
layout: post
title:      "Running python script on a website"
date:       2020-08-07 19:11:37 +0000
permalink:  running_python_script_on_a_website
---

The first step is, of course, setting up a website that can run the script. I was recommended [python anywhere](https://www.pythonanywhere.com/pricing/) which is a good, basic version to start with, as the free version works well for implementing basic code. I got my introduction from one of their [blog posts](https://blog.pythonanywhere.com/169/) that gives a step by step introduction to writing an initial webpage. This blog post is more intended to describe a few of the basic functions, and how to modify them, to implement specific tasks.<br><br>

I used flask as the library to communicate between python and the website itself. Python anywhere offers several options; flask is perhaps the most basic, which means that it's easy to get started and run some basic code (but doing more complicated things will likely become even more complicated than using one of the other libraries). I will be explaining Flask, largely by showing pieces of code and explaining what they do.<br><br><br>

`from flask import Flask,request`

flask.Flask is the implementation needed to run the code, flask.request has methods to turn user input into usable values for the code. Also, it is a good idea to set up processing code in a separate python file, which would be imported in this step.<br><br><br>

```
app = Flask(__name__)
app.config["DEBUG"] = True
```
This sets up flask to run the code. The line for “debug” is not necessary, but will cause any errors to be printed in the error file, which can be consulted if a crash happens. I usually find that coding is easiest for me when I try things, see them fail, and then work to address the specific error, instead of trying to make sure the code is absolutely perfect the first time. Using python anywhere means the errors won't be as visible as they are in jupyter notebooks! The website will just crash, and you need to open a separate page to see what went wrong.<br><br>

`@app.route('/', methods=["GET", "POST"])`<br>
This line comes right before the function you want to run. '/' denotes that this runs on the base webpage, you can also add text (such as '/secondary_page') if you instead want the code to run when (website)/secondary_page is loaded. Methods refer to how the page is loaded-get means loading from entering the site name, or refreshing the page; post means that it is loaded from an internal action, most commonly a “submit” button.<br><br>

Next, we'll jump to writing the end of the code, and come back to writing the middle section later. This is actually similar to how the code itself is often implemented! It is common to go straight to “return” on “get”, and then run the rest of the code only if request.method=='POST'.
```
def main():
    return '''
        <html>
            <body>
                <p>Text to display</p>
                {errors}
                <form action="." method="POST">
	        <input name="text_input">
                    <input type="file" name="myImage" id="fileToUpload">
                    <input type="submit" value="Upload Image" name="submit">
                </form>
            </body>
        </html>
    '''.format(errors=errors)
```
<br>
Flask uses html to format the returned string, to display the webpage! Anything in the `<form>` to `</form>` will be involved in the user input. Above are three different types of user input. The first, which specifies only the name, will create a text box where the user can input a typed value, which will be saved to the variable listed under name (in this case, saved to “text_input”). The second input creates a button that will open the users folder, for them to choose a file from their computer, which is saved to the variable “myImage” (name always represents where it's getting saved). That type='file' is how the program knows it's different than a text box. Finally, the input type “submit” creates a submit button, the “value” shows what text will be displayed on this button. Clicking this will submit the action in the initial `<form>` clause. In this case, the action “.” will reload the same page, but can also be specified to, for instance, go to /secondary_page as mentioned above. Method means that it will load the page in post, rather than get. Also, to use a file, include enctype="multipart/form-data" in this form line! We'll get to the errors bit when we go to the 'post' code, but note that it a variable we specify, not a native value. <br><br>

So, now for the 'post' code!<br>
```
    errors = ""
    if request.method == "POST":

        try:
           num_input = float(request.form['text_input'])
        except:
            errors += '<p>{} is not a number.</p>'.format(request.form['text_input']

        try:
            img = load_img(request.files['myImage'],target_size=(64,64))
        except:
            errors += '<p>Error, no image found</p>'

        if errors == "":
            results = img_to_results(img)
            return '''
                <html>
                    <body>
                        <p>{result}</p>
                        <p>Some text to display if successful</p>
                        <p><a href="/">Click here to return to user input stage</a>
                    </body>
                </html>
            '''.format(result=results)
```
Generally, it's a good idea to use “try:” and “except” when dealing with user inputs-if the user put in an invalid response, we can just tell them it was invalid, instead of crashing the webpage. Above lists a couple examples. The first tries to fit a variable with the float value of the text input. If it's a number, it will set that num_input value as specified, but if it is not a number, then it will cause an error, and go to the “except” clause. In this code, we created an empty string, errors, and if we get to that except clause, we add a string to it. This string will then display in the return code, so if a user made an error, they will be told about it. The second try/except clause tests to see if an uploaded file is an image, in this cause by using keras.preprocessing.image.load_img.<br><br>

If errors is still an empty string (if both of our try clauses did not meet an error), we can run the rest of the code! In this case “img_to_results” is a function in a separate python file, that does the processing mentioned earlier, in the import step, and the return string is part of the if statement-we still have the earlier return statement in the case that we do not go into this if statement (if errors is more than an empty string). We calculate a result, which causes a new string to be displayed-it shows us the result, potentially some extra text, and gives the user a link to return to the input stage.<br><br>

If we do not go through the if statement, we instead return the string described in the earlier step. And hopefully you can see what the errors value does now! Besides just being part of the if statement, it will display in this text, so the user can know what went wrong.<br><br>

Another note: you can also upload files to be used with the python files, such as a pickled model. The path location to use for this is '/home/your_username/mysite/file_name', if you're using python anywhere.<br><br>

To sum up, here is the full code (note that process.img_to_results is another .py file that is saved in the same directory):
```
from flask import Flask,request
from process import img_to_results
from keras.preprocessing.image import load_img

app = Flask(__name__)
app.config["DEBUG"] = True

@app.route('/', methods=["GET", "POST"])
def main():
    errors = ""
    if request.method == "POST":

        try:
           num_input = float(request.form['text_input'])
        except:
            errors += '<p>{} is not a number.</p>'.format(request.form['text_input']

        try:
            img = load_img(request.files['myImage'],target_size=(64,64))
        except:
            errors += '<p>Error, no image found</p>'

        if errors == "":
            results = img_to_results(img)
            return '''
                <html>
                    <body>
                        <p>{result}</p>
                        <p>Some text to display if successful</p>
                        <p><a href="/">Click here to return to user input stage</a>
                    </body>
                </html>
            '''.format(result=results)
    return '''
        <html>
            <body>
                <p>Text to display</p>
                {errors}
                <form action="." method="POST" enctype="multipart/form-data">
                    <input name="text_input">
                    <input type="file" name="myImage" id="fileToUpload">
                    <input type="submit" value="Upload Image" name="submit">
                </form>
            </body>
        </html>
    '''.format(errors=errors)
```

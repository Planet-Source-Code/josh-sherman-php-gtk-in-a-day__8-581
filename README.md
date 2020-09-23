<div align="center">

## PHP\-GTK in a Day


</div>

### Description

PHP-GTK is a hot new extension for the PHP language allowing for cross-platform GUI development. This tutorial is meant to help explain PHP-GTK and how to use it to develop your own GUI application.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Josh Sherman](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/josh-sherman.md)
**Level**          |Intermediate
**User Rating**    |3.8 (15 globes from 4 users)
**Compatibility**  |PHP 4\.0
**Category**       |[GUIs](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/guis__8-30.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/josh-sherman-php-gtk-in-a-day__8-581/archive/master.zip)





### Source Code

```
<P align="justify">
First, I would like to mention that this tutorial assumes you already have some basic knowledge of PHP, and have installed the PHP-GTK package (http://gtk.php.net/download.php). If you are new to PHP, then please check out my PHP 101 tutorial before proceeding.
</p>
<P align="justify">
Recently, I've found myself moving further and further away from application development, and more into web development. This isn't a bad thing, until the day you need to code an application and realize you don't know where to begin.
</p>
<P align="justify">
C isn't my favorite language, seeing as I'm a very amature programmer with the language. Perl and I aren't really friends anymore, and VB is out of the question now that I run Linux full time.
</p>
<P align="justify">
This would normally be a problem, but there is a new kid on the block, PHP-GTK. If you weren't aware already, I love PHP and if it were possible, I'd want it to have my children. Back to the point, PHP-GTK is a new extension of the PHP language that allows you (the developer) to write client-side, cross-platform GUI applications.
</p>
<P align="justify">
Pretty sexy, huh?
</p>
<P align="justify">
PHP-GTK utilizes the GTK+ libraries which are used to create graphical user interfaces. This technology was originally developed for the GIMP (GNU Image Manipulation Program) and has become a large part of Gnome.
</p>
<P align="justify">
As mentioned, PHP-GTK is cross-platform, allowing for applications to be developed on Linux and Windows.
</p>
<P align="justify">
Enough with the history, I bet you want to put PHP-GTK to good use. If you don't have PHP (4.0.5 or greater) and PHP-GTK (0.5.0 is the latest, and I recommend using it) installed, then please do so or you're going to be up the creek without a paddle in a few minutes.
</p>
<P align="justify">
In the grand tradition of programming, we are going to build a "hello world" application.
</p>
<P align="justify">
First thing you will need to do is create a new file, and name it "hello_world.php". Once you have that, open it up for editting.
</p>
<P align="justify">
Just like a PHP web page, a PHP-GTK file is going to start with <? and end with ?>. You can go ahead and put in the <? to start off our document.
</p>
<P align="justify">
After we put in the opening delimiter, we need to insert the code to tell the system that it is PHP-GTK and not just a standard PHP document.
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
if (!class_exists('gtk')) {<BR>
   dl('php_gtk.' . (strstr(PHP_OS, 'WIN') ? 'dll' : 'so'));<BR>
}
</i></b></font></td></tr></table>
<P align="justify">
This code is very significant to your code being cross-platform. It checks to see if the PHP-GTK extension is already available, and if not, it will load it up for you. The file that is loaded is either php_gtk.dll on Windows, or php_gtk.so on Linux.
</p>
<P align="justify">
If you have been checking out source code for PHP-GTK you have probably seen:
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
if (!class_exists('gtk')) {<BR>
   if (strtoupper(substr(PHP_OS, 0,3) == 'WIN'))<BR>
     dl('php_gtk.dll');<BR>
   else<BR>
     dl('php_gtk.so');<BR>
}
</i></b></font></td></tr></table>
<P align="justify">
which will accomplish the same task, but the previous code is only 3 lines instead of 6. Either one is acceptable.
</p>
<P align="justify">
So now our file has what it needs to tell the system that it is a PHP-GTK file. The next step is going to be to write some functions.
</p>
<P align="center">
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
function delete_event()<BR>
{<BR>
   return false;<BR>
}<BR>
<BR>
function shutdown()<BR>
{<BR>
   print("Shutting down...\n");<BR>
   gtk::main_quit();<BR>
}
</i></b></font></td></tr></table>
<P align="justify">
These are the functions that are used to handle terminating our application. The delete_event() is going to be registered as a handler for the "delete-event" signal, later in our code.
</p>
<P align="justify">
WTF?!?
</p>
<P align="justify">
Let me clarify, when the application is being closed, it sends out a "delete-event" signal to tell the system to delete the widget. Returning the value of "false" tells the system to continue with the deletion of the widget (in this case, our window).
</p>
<P align="justify">
The "delete_event()" function isn't 100% necessary, because the "delete-event" signal returns "false" by default. It was included because if you wanted to have an application prompt the user, to confirm that they wanted to close the application, the code would go in there. Returning the value of "true" will stop execution and leave the widget on the screen.
</p>
<P align="justify">
Hope that wasn't too much for you, because there's still more :)
</p>
<P align="justify">
The "shutdown()" function is pretty self explanatory. We are going to register that function as a handler for the "destroy" signal. The destroy signal is called when "delete-event" is "false". The function will contain any code you want to execute when the application is terminated. In this case, we're going to display "Shutting down..." in the console, and then call the funtion gtk::main_quit() which will tell the application to stop listening for events and to terminate itself and free up the memory.
</p>
<P align="justify">
Now our code is coming together, we have the code to load the PHP-GTK extension, and two functions to aid in terminating the application. Next on our plate is our function that will display "Hello World" for us.
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
function hello_world()<BR>
{<BR>
   print "Hello World!\n";<BR>
}
</i></b></font></td></tr></table>
<P align="justify">
This function will later be registered as a handler for the "clicked" signal on a button. When the button is clicked, the application will display "Hello World!" in the console.
</p>
<P align="justify">
Our functions are complete, so now it is time to build out our window. The next bit of code will build the window and connect the handlers to the functions we wrote previously.
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
$window = &new GtkWindow();<BR>
$window->connect('destroy', 'shutdown');<BR>
$window->connect('delete-event', 'delete_event');<BR>
$window->set_title('Hello World!');<BR>
$window->set_border_width(5);
</i></b></font></td></tr></table>
<P align="justify">
Up until now, the code we had written should have looked pretty familiar as most of it was plain PHP, now we are getting more into the meat and potatoes of the GTK+ side of PHP-GTK.
</p>
<P align="justify">
The first line creates a new widget and assigns it to the variable "$window". New widgets are always loaded in this format:
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
variable = &new GtkWidgetType;
</i></b></font></td></tr></table>
<P align="justify">
In this instance, our widget is the actual window that will contain our buttons and such. The window widget is known as GtkWindow.
</p>
<P align="justify">
Once we have created our widget, we have to connect the handlers to the functions we created earlier. The format for using the "connect" method is as follows:
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
widget->connect('signal', 'function');
</i></b></font></td></tr></table>
<P align="justify">
Incidentially, this is basically the same format we use for all methods, including the next two lines. The first one uses the "set_title" method to assign the title for the window, and the next sets the border width.
</p>
<P align="justify">
Now that we have our window built, we can go ahead and add a button to it. The button will trigger the "hello_world()" function and print out "Hello World!" in the console.
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
$button = &new GtkButton('Hello World!');<BR>
$button->connect('clicked', 'hello_world');<BR>
<BR>
$window->add($button);
</i></b></font></td></tr></table>
<P align="justify">
Like before, we create the new widget and assign it to a variable. This time, we have an arguement to the constructor, which will assign the text that will appear on our button.
</p>
<P align="justify">
After we create the button widget, we have to connect the "clicked" signal to the "hello_world()" function. Now whenever someone clicks on the button, the "hello_world()" function will be executed.
</p>
<P align="justify">
The third line refers back to the window widget we added earlier in our code. We use the method "add" to place the button on to the window.
</p>
<P align="justify">
You're almost done with your first PHP-GTK application. All we need to do now is display the widgets that we can created, and then tell the application to start listening for events. The following two lines do just that.
</p>
<TABLE align="center"><TR><TD><FONT size="2"><B><I>
$window->show_all();<BR>
gtk::main();
</i></b></font></td></tr></table>
<P align="justify">
Of course, we will need to add another delimiter to close off the PHP code, so tack on the ?> to the end, save the file, and close out of your editor.
</p>
<P align="justify">
Running your application is the next step in our adventure. If you are expecting to double-click on the file, and it executes, you're very mistaken. To use this application we will have to execute it with the PHP executable.
</p>
<P align="justify">
Depending on your system, you will have different syntax, but the basic method is going to be "php -q hello_world.php". The arguement "-q" is for quiet-mode, which will supress any HTTP header output to the console.
</p>
<P align="justify">
When you run that command on your system, it should bring up a nice little window with a button in the middle labeled "Hello World!"
</p>
<P align="justify">
Try clicking the button, it should display "Hello World!" in the console everytime you click it. Now click on the close button, and it should say "Shutting down..." and exit the application.
</p>
<P align="justify">
Congrats, you've just built your first PHP-GTK application.
</p>
<P align="justify">
The code in "hello_world.php" is functional, but doesn't get too deep. There are many different widgets that can be utilized. We only used the window and the button widgets, but could easily implement tool tips for our on screen objects, more buttons for different functions, entry fields to take input from the user, et cetera. This will be covered in future tutorials.
</p>
```


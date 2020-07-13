# For The Newbies: A simple PHP Contact Form Using Ajax To Send Email

## This is an old tutorial I've written back in 2012 and not on my website anymore. Saving it here because a lot of people found it useful.

<a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/z33man"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>
  
I’ve decided that I will write something for the newbie’s to PHP and show you how to create a simple contact form using AJAX to send an email to your email address.

I remember my first time starting out and learning PHP, damn was it hard to understand the first time. When you practice and write code often you will come to grips with it and as you go along you will get better at it.

So let’s get started with writing code. We are going to write the PHP code that handles the sending of emails first. Yes I know I’m doing it in the reverse order as we are only going to use three fields in our form, the name, email and message field.

**The PHP code to handle the form details and sending of the email**

    // Here we get all the information from the fields sent over by the form.
    $name = $_POST['name'];
    $email = $_POST['email'];
    $message = $_POST['message'];

    $to = 'youremail@domain.com';
    $subject = 'the subject';
    $message = 'FROM: '.$name.' Email: '.$email.'Message: '.$message;
    $headers = 'From: youremail@domain.com';

    if (filter_var($email, FILTER_VALIDATE_EMAIL)) { // this line checks that we have a valid email address
        mail($to, $subject, $message) or die('Error sending Mail'); //This method sends the mail.
        echo "Your email was sent!"; // success message
    }

The code above gets the field values posted using the $_POST  variable via the form we will be creating. We then set the variables to hold the TO, SUBJECT, MESSAGE and mail HEADERS information. We also do a small email validation via the PHP filter_var () method. Then we sent the message via the mail() method.

**Next Create the Contact Form to send a message.**

    <form id="mycontactform" action="" method="post"><label for="name">Name:</label>;

        <input id="name" type="text" name="name" />

        <label for="email">Email:</label>

        <input id="email" type="text" name="email" />

        <label for="message">Message:</label>

        <textarea id="message" name="message"></textarea>

        <input id="submit" type="button" value="send" />
        <div id="success" style="color: red;"></div>
    </form>
    
As you can see by the code above we created a very simple form to send a message with, nothing big about it at all.

**Next we create the jQuery Ajax code to post the form details to our PHP code**

    <script type="text/javascript" src="http://code.jquery.com/jquery-latest.js"></script><script type="text/javascript">
        $(document).ready(function(){

            $('#submit').click(function(){

                $.post("send.php", $("#mycontactform").serialize(),&nbsp; function(data) {&nbsp;&nbsp; });

                $('#success').html('Message sent!');
                $('#success').hide(2000);

            });

        });
    </script>
    
Here we call the jQuery code directly from the jQuery code library. Then write code to run when the page is done loading.

We use an onclick event which sends the form data to our send.php file which contains our PHP code to handle the email sending. We then set a success message and hide it again.

**Update 03 Dec 2012**

I've made some changes to the code as requested.

The response of the jQuery is now working and you will get a notice if you insert the incorrect email. Here is the html and jquery

    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://code.jquery.com/jquery-latest.js"></script>
    <script>
        $(document).ready(function(){

            $('#submit').click(function(){

                $.post("send.php", $("#mycontactform").serialize(),&nbsp; function(response) {
                $('#success').html(response);
                    //$('#success').hide('slow');
                });
                return false;

            });

        });
    </script>
    </head>
    <body>

        <form action="" method="post" id="mycontactform" >
            <label for="name">Name:</label><br />
            <input type="text" name="name" id="name" /><br />
            <label for="email">Email:</label><br />
            <input type="text" name="email" id="email" /><br />
            <label for="message">Message:</label><br />
            <textarea name="message" id="message"></textarea><br />
            <input type="button" value="send" id="submit" /><div id="success" style="color:red;"></div>
        </form>
    </body>
    </html>

**Here is the new PHP code.**

    // Here we get all the information from the fields sent over by the form.
    $name = $_POST['name'];
    $email = $_POST['email'];
    $message = $_POST['message'];

    $to = 'youremail@domain.com';
    $subject = 'the subject';
    $message = 'FROM: '.$name.' Email: '.$email.'Message: '.$message;
    $headers = 'From: youremail@domain.com' . "\r\n";

    if (filter_var($email, FILTER_VALIDATE_EMAIL)) { // this line checks that we have a valid email address
        mail($to, $subject, $message, $headers); //This method sends the mail.
        echo "Your email was sent!"; // success message
    }else{
        echo "Invalid Email, please provide an correct email.";
    }
    
If you’ve liked this tutorial or if you have some questions let me know in the comments section below. Please like the article?

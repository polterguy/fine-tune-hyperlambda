# Helper project to fine tune OpenAI on Hyperlambda

This project allows you to fine tune OpenAI and their GPT models on Hyperlambda. It creates a database named `fine-tune`, which it will use to store training material and validation material. It contains helper functions to insert from Hyperlambda example files into this database, and it allows you to generate JSONL files from the content of the database.

## Hyper parameters

Below are hyper parameters I've had success with in some example runs for gpt-40-mini.

1. Epochs - 1
2. Batch size - 8
3. LR multiplier - 0.3

If you're successful, you should have training loss around 0.1 - 0.7, and full validation loss at 0.3 higher than training loss, between 0.4 and 1.0. But you'll need to test the model to make sure it's performing.

Notice, during inference you should use around 0.0 and 0.1 in temperature to tighten results.

## Example test prompts

Below are some example prompts you can run through the model after fine tuning is done to test it.

* How do I convert a string to an integer?
* Generate a list of strings containing names of famous books
  - Add 3 items to it
* Generate a list of objects being employees
  - Add one item to it
  - Wrap it into and endpoint and return all employees
  - Loop through them and remove their names
  - Add departments to each entry from within your existing loop in addition to continuing removing items
* How do I open a database connection?
* How do I concatenate 2 strings?
  - Add a space between
  - Remove the space
* How do I send an email?
  - Change it such that it becomes and endpoint taking arguments for email message
  - Add name argument
  - Allow the caller to change the subject
  - Add an explicit SMTP server configuration. I will populate its values!
  - Turn it into a multi part message and attach /README.md
  - Change it such that the caller can define what file to attach as [filename]
* Write an endpoint taking age and name, and responding with a personal greeting
* Select contacts records from my ERP database.
  - Wrap it into an endpoint and returns contacts.
  - Change database to chinook and table to Artist. Return ALL columns!
  - Add paging arguments
  - Make paging arguments optional
  - Add sorting arguments
  - Return contacts as [result_from_db]
  - Include Album records for each record. Use ArtistId as your foreign key!
  - Add filtering on name
* Create an endpoint taking a message only allowing admin users to execute it, then log the message
  - Return success
  - Add 30 seconds of http caching
* Create an endpoint that allows me to return records from my employees table in my hr database with paging and sorting.
  - Make sorting optional
  - Make paging optional
  - Make both paging and sorting mandatory
  - Comment your code extensively!
  - Create a log entry with all arguments and their values
* Create an endpoint allowing me to create new items in my contacts table in my CRM database.
  - Make email mandatory
  - Make sure email is a valid email address
  - Return result of data.create as [result]
* Generate an API endpoint allowing me to select users from employees database, with optional filtering for name, email, and phone
  - Add paging
  - Make paging optional
* Generate an endpoint that only partner users can execute
* How do I retrieve a configuration value named 'foo' inside of my 'magic' section?
  - Assign it to a temporary variable
  - Prepend 'Bearer ' when assigning it
  - Use it in an HTTP GET invocation towards foo.com
* Select all contacts from CRM, loop through all of these and update these one at the time and change their names to 'REDACTED' and save your changes
  - The primary key is 'id'
* Generate code for an endpoint allowing me to update items in my stock table in my logistics database
  - Make updated values optional such that I can provide any values I wish
  - Return the result of [data.update]
* How do I delete a record from contacts in crm database?
* Create an endpoint taking a name filter that's using SQL slots to return customers from my sales db
* Create an endpoint that sends an email with subject, body, name and email as arguments
  - Make the name argument mandatory
* Create an endpoint that loads a file specified as an argument and returns its content back to caller.
  - Assume file is only filename and ONLY return files from /etc/www/
  - Split the files into lines and return individual lines
  - Change it such that only 'admin' users can execute it
  - Return how many lines there are in file, in addition to each individual line
* Create an upload file endpoint that saves files to /etc/temp/ folder
* I've got a file at /etc/www/foo.zip. I want you to show me the code required to unzip it
* Create an HTTP endpoint that invokes Chuck Norris Joke API to generate a random joke and return to caller
* I need an endpoint that's invoking Cat fact API and returns the fact to the caller
* How do I update a record in my HR database and its employees table?
* Show me an endpoint concatenating name and age with a greeting and returning the result to caller
* Generate an HTTP endpoint for me that lists all files in /etc/www/ and returns this to the caller
  - Change the folder to /foo/bar/
  - Create a log entry when invoked, and make sure only admin users can execute it
* How do I concatenate two strings given to an endpoint as arguments?
  - Return the concatenated result, and put a space between arguments
* Create an API endpoint that allows me to insert a contact into HubSpot
  - Retrieve hubspot token from config as 'magic:hubspot:token'
* Create an endpoint allowing me to read a sitemap from a domain, and return all URLs found.
* Create an endpoint that first fetches 10 Artist records from chinook database using SQLite, then include all their Album records for each Artist. Add filtering support for artist name.


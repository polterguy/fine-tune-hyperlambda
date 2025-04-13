# Helper project to fine tune OpenAI on Hyperlambda

This project allows you to fine tune OpenAI and their GPT models on Hyperlambda. It creates a database named `fine-tune`, which it will use to store training material and validation material. It contains helper functions to insert from Hyperlambda example files into this database, and it allows you to generate JSONL files from the content of the database.

## Hyper parameters

Below are hyper parameters I've had success with in some example runs for gpt-40-mini.

1. Epochs - **AUTO**
2. Batch size - **AUTO**
3. LR multiplier - **AUTO**

If you're successful, you should have training loss around 0.1 - 0.7, and full validation loss at 0.3 higher than training loss, between 0.4 and 1.0. But you'll need to test the model to make sure it's performing.

Notice, during inference you should use around 0.0 and 0.1 in temperature to tighten results.

## Example test prompts

Below are some example prompts you can run through the model after fine tuning is done to test it.

* How do I convert a string to an integer?
* Generate a list of strings containing names of famous books
  - Add 3 items to it
* Generate a list of objects being employees
  - Loop through them and remove their names
* How do I open a database connection?
* How do I concatenate 2 strings?
* How do I send an email?
* Write an endpoint taking age and name, and responding with a personal greeting
* Select contacts records from my ERP database.
* Create an endpoint taking a message only allowing admin users to execute it, then log the message
* Create an endpoint that allows me to return records from my employees table in my hr database with paging and sorting.
  - Make sorting optional
  - Make paging optional
  - Make both paging and sorting mandatory
  - Create a log entry with all arguments and their values
* Create an endpoint allowing me to create new items in my contacts table in my CRM database.
  - Make email mandatory
  - Make sure email is a valid email address
* Generate an API endpoint allowing me to select users from employees database, with optional filtering for name, email, and phone
* Generate an endpoint that only partner users can execute
* How do I retrieve a configuration value named 'foo' inside of my 'magic' section?
* Select all contacts from CRM, loop through all of these and update these one at the time and change their names to 'REDACTED' and save your changes
* Generate code for an endpoint allowing me to update items in my stock table in my logistics database
* How do I delete a record from contacts in crm database?
* Create an endpoint taking a name filter that's using SQL slots to return customers from my sales db
* Create an endpoint that sends an email with subject, body, name and email as arguments
* Create an endpoint that loads a file specified as an argument and returns its content back to caller.
  - Split the files into lines and return individual lines
* Create an upload file endpoint that saves files to /etc/temp/ folder
* I've got a file at /etc/www/foo.zip. I want you to show me the code required to unzip it
* Create an HTTP endpoint that invokes Chuck Norris Joke API to generate a random joke and return to caller
* I need an endpoint that's invoking Cat fact API and returns the fact to the caller
* How do I update a record in my HR database and its employees table?
* Show me an endpoint concatenating name and age with a greeting and returning the result to caller
* Generate an HTTP endpoint for me that lists all files in /etc/www/ and returns this to the caller
  - Change the folder to /foo/bar/
* How do I concatenate two strings given to an endpoint as arguments?
  - Return the concatenated result, and put a space between arguments
* Create an API endpoint that allows me to insert a contact into HubSpot
* Create an endpoint allowing me to read a sitemap from a domain, and return all URLs found.
* Create an endpoint that first fetches 10 Artist records from chinook database using SQLite, then include all their Album records for each Artist. Add filtering support for artist name.


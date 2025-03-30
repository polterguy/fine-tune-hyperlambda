# Helper project to fine tune OpenAI on Hyperlambda

This project allows you to fine tune OpenAI and their GPT models on Hyperlambda. It creates a database named `fine-tune`, which it will use to store training material and validation material. It contains helper functions to insert from Hyperlambda example files into this database, and it allows you to generate JSONL files from the content of the database.

## Hyper parameters

Below are hyper parameters I've had success with in some example runs for gpt-40-mini.

1. Epochs - 3
2. Batch size - 8
3. LR multiplier - 0.17

If you're successful, you should have training loss around 0.1 - 0.6, and full validation loss at 0.3 higher than training loss, between 0.4 and 0.9.

Notice, during inference you should use around 0.0 and 0.1 in temperature to tighten its result better.

## Example test prompts

Below are some example prompts you can run through the model after fine tuning is done to test it.

* How do I convert a string to an integer?
* How do I open a database connection?
* How do I concatenate 2 strings?
* How do I send an email?
* Write an endpoint taking age and name, and responding with a personal greeting
* Select contacts records from my ERP database.
* Create an endpoin taking a message only allowing admin users to execute it, then log the message
* Create an endpoint that allows me to return records from my employees table in my hr database with paging and sorting.
* Create an endpoint allowing me to create new items in my contacts table in my CRM database.
* Generate an endpoint that only partner users can execute
* Select all contacts from CRM, loop through all of these and update these one at the time and change their names to 'REDACTED' and save your changes
* Generate code for an endpoint allowing me to update items in my stock table in my logistics database
* How do I delete a record from contacts in crm database?
* Create an endpoint taking a name filter that's using SQL slots to return customers from my sales db
* Create an endpoint that sends an email with subject, body, name and email as arguments
* Create an endpoint that loads a file specified as an argument and returns its content back to caller.
* Create an upload file endpoint that saves files to /etc/temp/ folder
* I've got a file at /etc/www/foo.zip. I want you to show me the code required to unzip it in the same folder it exists in
* Create an HTTP endpoint that invokes Chuck Norris Joke API to generate a random joke and return to caller
* I need an endpoint that's invoking Cat fact API and returns the fact to the caller
* How do I update a record in my HR database and its employees table?
* Show me an endpoint concatenating name and age with a greeting and returning the result to caller
* Generate an HTTP endpoint for me that lists all files in /etc/www/ and returns this to the caller
* How do I concatenate two strings given to an endpoint as arguments?

However, the best way to test is to take the file level comment from your validation data, and run through the model afterwards.

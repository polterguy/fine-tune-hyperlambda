# Helper project to fine tune OpenAI on Hyperlambda

This project allows you to fine tune OpenAI and their GPT models on Hyperlambda. It creates a database named `fine-tune`, which it will use to store training material and validation material. It contains helper functions to insert from Hyperlambda example files into this database, and it allows you to generate JSONL files from the content of the database.

## Hyper parameters

Below are hyper parameters I've had success with in some example runs.

1. **auto**
2. **auto**
3. **auto**

If you're successful, you should have training loss around 0.3 - 0.6, and full validation loss at 0.3 higher than training loss, between 0.6 and 0.9.

## Example test prompts

* How do I send an email?
* How do I concatenate 2 strings?
* Select contacts records from my ERP database. My database is SQLite, and I want to use CRUD slots.
* Create an endpoint that sends an email with subject, body, name and email as arguments
* Create an endpoint that loads a file specified as an argument and returns its content back to caller.
* Create an upload file endpoint that saves files to /etc/temp/ folder
* I've got a file at /etc/www/foo.zip. I want you to show me the code required to unzip it in the same folder it exists in
* Create an HTTP endpoint that invokes Chuck Norris Joke API to generate a random joke and return to caller
* Create an endpoint that executes Cat Fact Joke API to and returning a random fact about cats

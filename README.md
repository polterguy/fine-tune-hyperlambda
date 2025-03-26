# Helper project to fine tune OpenAI on Hyperlambda

This project allows you to fine tune OpenAI and their GPT models on Hyperlambda. It creates a database named `fine-tune`, which it will use to store training material and validation material. It contains helper functions to insert from Hyperlambda example files into this database, and it allows you to generate JSONL files from the content of the database.

## Hyper parameters

Below are hyper parameters I've had success with in some example runs.

1. Batch size 32
2. LR multiplier set to 0.05
3. 3 epochs

I used a seed of _"1518472637"_, but the above should give you a rough idea of where to start.

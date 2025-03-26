# Helper project to fine tune OpenAI on Hyperlambda

This project allows you to fine tune OpenAI and their GPT models on Hyperlambda. It creates a database named `fine-tune`, which it will use to store training material and validation material. It contains helper functions to insert from Hyperlambda example files into this database, and it allows you to generate JSONL files from the content of the database.

## Hyper parameters

Below are hyper parameters I've had success with in some example runs.

1. 3 epochs
2. Batch size 5
3. LR multiplier set to 0.5

If you're successful, you should have training loss around 0.5, and full validation loss at 0.3 higher than training loss.


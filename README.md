# Password Strength Analyzer

A Jupyter notebook that checks how strong a password is, saves the result in PostgreSQL and draws a few graphs from everything tested so far.

## How it works

You enter a user ID and a password. The password gets one point for each of these:

- at least 8 characters
- an uppercase letter
- a lowercase letter
- a digit
- a symbol

If the password contains the user's ID (for example `ana.pop2024` for the user `ana.pop`), the score drops to 1, because that's one of the first things an attacker would try. Based on the score, the password is labelled weak, medium or strong. The notebook also checks whether it appears in a list of known leaked passwords (`parole_compromise.txt`).

The result goes into a PostgreSQL table. The password itself is never stored, only its SHA-256 hash, together with the score, the level and whether it was found in the leaked list.

## Graphs

- how many of the tested passwords are weak, medium and strong
- how many were found in the leaked list

## Running it

You need a local PostgreSQL database called `proiect_parola_db` with a `verificare_parola` table, plus `psycopg2`, `pandas` and `matplotlib`. Set your database password at the top of the notebook and run the cells in order.

## What I'd like to add

- a better score, for example an entropy estimate instead of simple rules
- a much larger list of real leaked passwords
- a salted hash instead of plain SHA-256

# Bad files from your bank.

Some banks deliver abysmal CSV files. They have an interest to keep you inside their eco-system and will do anything to stop you from moving to another system. Here are some common problems and their solutions.

## File is not UTF-8

Use an application like Notepad++, Atom, Visual Studio Code or Sublime Text to convert the file to UTF-8. The CSV importer is incapable of doing this for you.

## Not enough info to make rows unique

If you don't specifically configure the importer to import non-unique rows, open the file in Excel or Numbers and add a row with a basic sequence: 1,2,3,4 etc. That should be enough to make the rows unique.

## Transfers aren't merged

The CSV importer is capable of merging two transactions (one from A > B, and one from B < A) if they seem to be the same transaction listed twice. For example, when you import two files: one from your checking account and one from your savings account.

If they don't have the same description, this won't work. You'll have to manually edit your file so the transactions are the same.

## Other issues?

Please open a ticket [on GitHub](https://github.com/firefly-iii/firefly-iii/).

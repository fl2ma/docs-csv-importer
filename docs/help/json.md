# JSON

The Firefly III CSV importer generates an import file each time you import CSV files. You can download the CSV file during or after the import.

## Pre-made import files

There's a repository on GitHub with [import configurations for common banks and financial institutions](https://github.com/firefly-iii/import-configurations).

## Example file

```json
{
    "date": "Ymd",
    "default_account": 1,
    "delimiter": "comma",
    "headers": true,
    "ignore_duplicate_lines": true,
    "ignore_duplicate_transactions": true,
    "rules": true,
    "skip_form": false,
    "specifics": [
        "AppendHash"
    ],
    "roles": [
        "date_transaction",
        "description",
        "amount",
        "account-name",
        "opposing-name",
        "note"
    ],
    "do_mapping": {
        "3": true,
        "4": true,
        "0": false,
        "1": false,
        "2": false,
        "5": false
    },
    "mapping": {
        "3": {
            "Savings Account": 3
        },
        "4": {
            "Savings Account": 3
        }
    },
    "version": 2
}
```

## Explanation

Each field in this file has a function, and they're explained in this table:

### date

Sets the date format of the date entries in the CSV file. For the format, [read this page](https://www.php.net/manual/en/function.date.php).

### default_account

The ID of the default asset accounts into which transactions will be imported if there's no source account.

### delimiter

The delimiter of the entries in the CSV files. Most files use "comma", but you can also use "semicolon" or "tab".

### headers

True or false if the CSV file has headers.

### ignore_duplicate_lines

If the importer should ignore duplicate lines in your CSV file.

### ignore_duplicate_transactions

If checked, Firefly III will give you an error if the transaction already exists.

### rules

Whether or not to apply your rules to the import.

### skip_form

If checked, next time you use the importer it will skip the configuration form.

### specifics

"Specifics" are specific (haha) scripts that can be applied to your import.

### roles

A role for each column.

### do_mapping

Whether or not these columns should be mapped to data in your Firefly III installation.

### mapping

The mapping. The value in brackets is what's found in the CSV file, the ID links to the account in your Firefly III installation.

### version

Should be 2.
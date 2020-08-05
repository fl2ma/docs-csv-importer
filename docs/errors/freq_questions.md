# Frequently Asked Questions

## How do I start over or reset the importer?

Browse to `/flush` on your CSV importer. This will reset it.

## My connection times out, even though the IP addresses are correct

This applies to Docker. Make sure that both containers [are on the same network](https://old.reddit.com/r/FireflyIII/comments/fuur8o/csvimporter_connection_timeout/).

Please open a ticket [on GitHub](https://github.com/firefly-iii/firefly-iii/).

## Why can't I import duplicate transactions?

The Firefly III CSV importer can recognise two different types of duplicate transactions. By default it will refuse to import both of them.

1. Duplicate lines in your CSV files are skipped, unless you explicitely tel the CSV importer to include them.
2. Firefly III itself will refuse to import transactions it believes already exist. You can overrule this.

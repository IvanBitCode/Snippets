# CSV and JSON Files
## Zip files
Pending...

## CSV files
```python
# Creating a CSV file
import csv

with open("data.csv", mode="w") as file:
    csv_writer = csv.writer(file)
    writer.writerow(["transaction_id, product_id, price"])
    writer.writerow(["1000, 1, 5"])
    writer.writerow(["1000, 2, 15"])

# Note: by using the with keyword, we don't need to be worry to close the file object.

# Reading a CSV file
with open("data.csv") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

## JSON files
Pending...
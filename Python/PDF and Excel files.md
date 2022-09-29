# PDF and Excel Files
## PDF Files
### Read and Write PDF Files
First we need to install the pypdf2 module:
`pipenv install pypdf2`

Now in out script file:
```python
import PyPDF2

with open("fisrt.pdf", "rb") as file:  # read file as binary
    reader = PyPDF2.PdfFileReader(file)
    pags = reader.numPages
    page = reader.getPage(0)  # get first page as a page object
    page.rotateClockwise(90)

    writer = PyPDF2.PdfFileWriter()  # create a new pdf file in memory
    writer.addPage(page)  # add a page at the end (in memory)
    with open("rotated.pdf", "wb") as output:
        write.write(output)
```

### Merge Several PDF Files
```python
import PyPDF2
merger = PyPDF2.PdfFileMerger()
file_names = ["first.pdf", "second.pdf"]

# Note: We can iterate over pdf files in a dir.

for file_name in file_names:
    merger.append(file_name)  #merge is in memory
merger.write("combined.pdf")
```

## Excel Files
### Basics
First we need to install the openpyxl module:
`$pipenv install openpyxl`

```python
import openpyxl

wb = openpyxl.Workbook()      # create an empty workbook with one sheet.
wb = openpyxl.load_workbook("transactions.xlsx")  # load and existing workbook
wb.create_sheet("Sheet2", 0)  # create a new sheet before Sheet1
sheet = wb["Sheet1"]          # getting a sheet

# Getting cells
cell = sheet["a1"]
cell = sheet.cell(row=1, column=1)

# Getting cells info
cell.value            # get the value of a cell
cell.value = "other"  # change the value of a cell
call.row              # get the row number of this cell, in this case is 1
cell.column           # get the column of this cell, in this case is A
cell.coordinate       # get the coordinate of this cell, in this case is A1
```

### Iterating Over Used Cells in a Sheet
```python
for row in range(1, sheet.max_row + 1):
    for column in range(1, sheet.max_column + 1):
        cell = sheet.cell(row, column)
```
Note: we are adding 1 because range function starts in row or col 1.

### Accesing to Range of Cells
```python
column = sheet["a"]  #get all cells in column A
cells = sheet["a:c"]  #get all cells in column A to C
cells = sheet["a1:c3"]
```

### Add a Row at the Enfd of the Sheet
```python
sheet.append([1 , 2, 3]) 

Other methods are
sheet.insert_rows()
sheet.insert_columns()
sheet.delete_rows()
sheet.delete_columns()
```

### Save Workbook to Disc
```python
wb = openpyxl.Workbook()
wb.save("transactions.xlsx")
```

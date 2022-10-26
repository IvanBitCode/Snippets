# Create Excel file with ClosedXML library

```cs
XLWorkbook workbook = new XLWorkbook();
IXLWorksheet worksheet = workbook.Worksheets.Add("Cars");

// Add cells text
worksheet.Cell(1, 1).Value = "Column 1";
worksheet.Cell(1, 2).Value = "Column 2";
worksheet.Cell(1, 3).Value = "Column 3";

// Change background color to cells
worksheet.Cell(1, 1).Style.Fill.BackgroundColor = XLColor.BlueGray;
worksheet.Cell(1, 2).Style.Fill.BackgroundColor = XLColor.BlueGray;
worksheet.Cell(1, 3).Style.Fill.BackgroundColor = XLColor.BlueGray;
 
// Change cell vertical aligment
worksheet.Cell(1, 1).Style.Alignment.Vertical = XLAlignmentVerticalValues.Center;
 
worksheet.Columns().AdjustToContents();
workbook.SaveAs("excelFileName.xlsx");
```
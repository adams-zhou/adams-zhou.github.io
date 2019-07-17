1. VBA名字，定义list
> Formulas-Name Manager

2. 深度隐藏SHEET
> Properies中Visible->2-xlSheetVeryHidden

3. 值匹配list
> MATCH(value, list, 0)  0表示等于

4. 偏移
> OFFSET(单元格， 向下n格，向右n格)

5. VBA连接数据库
> Tools-References  增加Microsoft ActiveX Data Objects2.8 Library
```vba
Public adoConn         As ADODB.Connection
set adoConn = New ADODB.Connection
adoConn.Open "XXX用户名密码驱动"
adoConn.CursorLocation = adoUseClient
>
Dim myCmd              As New ADODB.Command
Dim myRst              As ADODB.Recordset
set myCmd.ActiveConnection = adoConn
myCmd.CommandText = "sql语句"
myCmd.CommandType = adCmdText
set myRst = myCmd.Execute
>
If Instr(UCase(strSql), "SELECT") <> 0 Then
	With myRst
		For i=1 to .Fields.Count
		sheet.Cells(XX, XX).value=.Fields(i-1).Name
	Next i
	If .RecordCount > 0 Then
		.MoveFirst
		sheet.Cells(XX, XX).CopyFromRecordset myRst
	End If
	End With
	myRst.Close
End If
set myRst = Nothing
set myCmd = Nothing
```
	VBA事务
	adoConn.BeginTrans
	adoConn.CommitTrans
	adoConn.RollbackTrans

6. VBA选文件
单选
```vba
Dim fdl     As FileDialog
set fdl = Application.FileDialog(msoFileDialogFilePicker)
With fdl
	.InitialFileName = 路径
	.AllowMultiSelect = False
	.Filters.Clear
	.Filters.Add  对话框标题 ，匹配文件（例*.txt）
End With
If fdl.Show = True Then
	return fdl.SelectedItem(1)
End If
set fld = Nothing
```
多选
```vba
Dim fdl     As FileDialog
set fdl = Application.FileDialog(msoFileDialogFilePicker)
With fdl
    .InitialFileName = 路径
    .AllowMultiSelect = False
    .Filters.Clear
    .Filters.Add  对话框标题 ，匹配文件（例*.txt）
End With
If fdl.Show = True Then
	ReDim strSelectedFile(fdl.SelectedItems.Count-1)  As String
	For i=1 To fdl.SelectedItems.Count
	strSelectedFile(i-1) = fdl.SelectedItems(i)
	Next i
End If
set fld = Nothing
```

7. 写文件
```vb
Public Function WriteOutputFile(strTextFile As String, arrData As Variant)
	Dim objF    As Object
	Dim i	As Long
	Dim j	As Long
	Dim strOutputLine    As String
	Dim strCell		 As String
	set objF = CreateObject("ADODB.Stream")
	objF.Type = adTypeText
	objF.Charset = "UTF-8"
	objF.Open
	If IsArray(arrData) Then
	For i = 1 To UBound(arrData, 1)
	    strOutputLine=""
	    For j = 1 To UBound(arrData, 2)
		strCell = arrData(i, j)
		strOutputLine = strOutputLine & strCell
	    Next j
	    strOutputLine = strOutputLine & vbCrlf
	    objF.WriteText strOutputLine
	Next i
	Else
	objF.WriteText = ""
	End If
	objF.SaveToFile strTxtFile
	objF.Close
	set objF = Nothing
End Function
```

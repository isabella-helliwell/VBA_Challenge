# VBA_Challenge

## 1. Project Scope
      Part1:
      The scope of this project is to compare the stockmarket for predefined stocks for years 2017 and 2018
      writing a VBA macro in Excel.
      Part 2:
      The second part of this project is to optimize the VBA code and Runtime
      
### 1.1 Stockmarket Analysis and Results
      The analysis are based on obtaining the yearly return for the predefined stocks.
      The formula used is (endingPrice / startingPrice - 1) for each year and stock.
      Results are shown in Table 1 and Table 2.
 
 Table 1. Yearly return for year 2017
 
![image](https://user-images.githubusercontent.com/85843030/124384753-c69d2e80-dca0-11eb-9eba-b0d7f01f6c8b.png)




Table2. Yearly return for year 2018

![image](https://user-images.githubusercontent.com/85843030/124384801-fea47180-dca0-11eb-861f-8f5bf24c4c5e.png)

Overal, the stocks did much better in 2017 than 2018.

### 1.2 VBA Code
      The overal layout of the VBA code consists of a suberoutine name, and a collection of steps and instructions.
      The name of the Subroutine is set to "VBA_Challenge", and the instructions given is to calculate the yearly return for stocks.
      In the first part of the macro, variable declarations are made to assign the correct data types.
      In the main part of the macro, the actual calculations are carried out utilizing nested foor loops.
      In the last part of the macro, the results are populated into the appropiate cells and sheets.
      There are also some formatting and macro runtime recorded.
      
#### 1.2.1 VBA Code Explained

      The following code is used for the first part of the macro:
##### Sub VBA_Challenge()
##### Dim startTime As Single
##### Dim endtime As Single
##### Dim tickers(12) As String
##### Dim startingPrice As Single
##### Dim endingprice As Single
##### Dim totalvolume As Long
      The above code, is declaring some variables using the following format: [DIM variablename AS DATATYPE],
      
##### yearvalue = InputBox("What year would you like to run the analysis on")
      -MessageBox will ask the user to input year for the Stocks to be analysed and will assign yearvalue the input
      
##### RowCount = Sheets(yearvalue).Cells(Rows.Count, "A").End(xlUp).Row
      - RowCount will open up the Excel tab with the same year as the user year input and select column A,
        and scroll up to the first row with a non blank cell in column A. This will provided how many Rows there is in the sheet opened.
        
##### starttimer = Timer
      -Starts timing the macro
      
##### Worksheets(yearvalue).Activate
      -activates the tab in Excel that the user input year chose in the previous steps
      
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("A1").Value = "All Stocks " & yearvalue
##### Sheets("All_Stocks_Analysis" & yearvalue).Cells(2, 1).Value = "Ticker"
##### Sheets("All_Stocks_Analysis" & yearvalue).Cells(2, 2).Value = "Total Daily Volume"
##### Sheets("All_Stocks_Analysis" & yearvalue).Cells(2, 3).Value = "Return"   
      -Predefining some hearders in the appropiate sheet we have chosen to do our analysis in
 
 
##### tickers(0) = "AY"
##### tickers(1) = "CSIQ"
##### tickers(2) = "DQ"
##### tickers(3) = "ENPH"
##### tickers(4) = "FSLR"
##### tickers(5) = "HASI"
##### tickers(6) = "JKS"
##### tickers(7) = "RUN"
##### tickers(8) = "SEDG"
##### tickers(9) = "SPWR"
##### tickers(10) = "TERP"
##### tickers(11) = "VSLR"
      -tickers hold the information of each stock name. This is used to loop through each stock by assigning a pointer "j" to them
     
##### For j = 0 To 11
      -the loop starts with the pointer "j" pointing at ticker(0), which is stock "AY"
      
##### totalvolume = 0
      -the total volume will be set to 0 before the next stock is looped through
      
##### Ticker = tickers(j)
      -Ticker is assigned the value in tickers(0), which is "AY"

#####     For i = 2 To RowCount
            -the loop starts at Row 2, and will loop until Rowcount, which is now known

#####         If Cells(i, 1).Value = Ticker Then
                  -conditional statement, that says if row 2 in column 1 ="AY",
            
#####             totalvolume = totalvolume + Cells(i, 8).Value
                  -then, totalvolume= previous totalvolume + the value in Row2, Column 8

#####         End If
                  -end of an If statement
                  
                  
#####         If Cells(i - 1, 1).Value <> Ticker And Cells(i, 1).Value = Ticker Then
                  -conditional statement finding the first value of a stock, "AY" in this run, by checking if the
                  previous row and the current row do not have the same stock name


 #####            startingPrice = Cells(i, 6).Value
                  then, the starting price is set to the price in row2, cell 6
                                 
                  
 #####        End If
                  -end of an If statement
 

 #####        If Cells(i + 1, 1).Value <> Ticker And Cells(i, 1).Value = Ticker Then
                  -conditional statement checking to see if the next row and this row are different stocks,
 

 #####            endingprice = Cells(i, 6).Value
                  then, the endingprice for the current stock is the value in row2, column 6

 #####        End If
                  -end of an If statement

#####     Next i
            - now, the macro will move to the next Row, in this example, it will check to see if Row3 is also stock "AY"
      
#####     Sheets("All_Stocks_Analysis" & yearvalue).Cells(3 + j, 1).Value = Ticker
#####     Sheets("All_Stocks_Analysis" & yearvalue).Cells(3 + j, 2).Value = totalvolume
#####     Sheets("All_Stocks_Analysis" & yearvalue).Cells(3 + j, 3).Value = endingprice / startingPrice - 1      
          -After the macro has gone through all the rows containing "AY" Stock, it has finnished its loop, and 
          the results are put in worksheet and cells
          
          
#####   Next j
          -After all the "AY" stocks have been looped through, the j will point to the next ticker, ticker (1), stock "CSIQ"
          and do the above loop again, where instead of "AY" stock, it will look at "CSIQ"



The next part of the code is to format the cells. This is done using the following codes:
    
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("A2:C2").Font.Bold = True
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("A2:C2").Font.Size = 12
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("A2:C2").Borders(xlEdgeBottom).LineStyle = xlContinuous
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("A1").Font.Bold = True
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("A1").Font.Size = 14
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("A2:C2").Font.ColorIndex = 1
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("C:C").numberformat = "0.0%"
##### Sheets("All_Stocks_Analysis" & yearvalue).Range("B:B").numberformat = "#0#"
##### Sheets("All_Stocks_Analysis" & yearvalue).Columns("B").AutoFit


Lastly we will format the yearly returns obtained in our results with a for loop to loop through the cells and highlight any values
less than 0 red and any values more than 0 with green.

##### rowend = Sheets("all_Stocks_Analysis" & yearvalue).Cells(Rows.Count, "A").End(xlUp).Row
##### For i = 3 To rowend

#####       If Sheets("All_stocks_analysis" & yearvalue).Cells(i, 3).Value < 0 Then
#####       Sheets("All_Stocks_Analysis" & yearvalue).Cells(i, 3).Interior.Color = vbRed
        
#####       Else: Sheets("All_Stocks_Analysis" & yearvalue).Cells(i, 3).Interior.Color = vbGreen
#####       End If

##### Next i

After the macro has run, the timer will stop recording the time and a message box with how long the run took will appear.

##### Sheets("All_stocks_analysis" & yearvalue).Activate
#####       endtime = Timer
##### MsgBox "This code ran in " & (endtime - startTime) & " seconds for the year " & (yearvalue)

##### End Sub


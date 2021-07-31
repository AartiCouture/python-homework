```python
import csv
from pathlib import Path
```


```python
file_to_load = Path("budget_data.csv")
file_to_output = Path("analysis", "financial_analysis.txt", "delimiter ','")


```


```python
total_months = 0
net_total = 0
months_change = []
average_change = []
greatest_increase =["",0]
greatest_decrease = [0,9999999]
total_average = 0
pre_val = 0


```


```python
with open(file_to_load) as budget_analysis:
    csvreader = csv.reader(budget_analysis)
    csv_header = next(csvreader)
    for row in csvreader:
        
        
        total_months += 1
        
        net_total += int(row[1])
        change = int(row[1])-pre_val
        if pre_val ==0:
            pre_val = int(row[1])
        else:
            
            months_change.append(change)
            pre_val = int(row[1])

        
        if int(change) > int(greatest_increase[1]) and total_months > 1:
            greatest_increase = row
        
        if int(change) < int(greatest_decrease[1]) and total_months > 1:
            greatest_decrease = row
            
            
       
```


```python
print(net_total)
print(greatest_increase)
print(greatest_decrease)
```

    38382578
    ['Nov-2016', '795914']
    ['Jul-2016', '-1163797']



```python
average_change= sum(months_change)/len(months_change)

          
     
               
```


```python
print(total_months)
```

    86



```python
print(months_change)
```

    [116771, -662642, -391430, 379920, 212354, 510239, -428211, -821271, 693918, 416278, -974163, 860159, -1115009, 1033048, 95318, -308093, 99052, -521393, 605450, 231727, -65187, -702716, 177975, -1065544, 1926159, -917805, 898730, -334262, -246499, -64055, -1529236, 1497596, 304914, -635801, 398319, -183161, -37864, -253689, 403655, 94168, 306877, -83000, 210462, -2196167, 1465222, -956983, 1838447, -468003, -64602, 206242, -242155, -449079, 315198, 241099, 111540, 365942, -219310, -368665, 409837, 151210, -110244, -341938, -1212159, 683246, -70825, 335594, 417334, -272194, -236462, 657432, -211262, -128237, -1750387, 925441, 932089, -311434, 267252, -1876758, 1733696, 198551, -665765, 693229, -734926, 77242, 532869]



```python
print(average_change)
```

    -2315.1176470588234



```python
output = (
    f"\nFinancial Analysis\n"
    f"----------------------------\n"
    f"Total Months: {total_months}\n"
    f"Total: ${net_total}\n"
    f"Average  Change: ${average_change:.2f}\n"
    f"Greatest Increase in Profits: {greatest_increase[0]} (${greatest_increase[1]})\n"
    f"Greatest Decrease in Profits: {greatest_decrease[0]} (${greatest_decrease[1]})\n") 
    


```


```python
print(output)
```

    
    Financial Analysis
    ----------------------------
    Total Months: 86
    Total: $38382578
    Average  Change: $-2315.12
    Greatest Increase in Profits: Nov-2016 ($795914)
    Greatest Decrease in Profits: Jul-2016 ($-1163797)
    



```python
with open("Financial Analysis", "w") as txt_file:
    txt_file.write(output)

```


```python

```

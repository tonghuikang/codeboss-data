# Data Cleansing

**Part I - Phone number data cleansing (60 points)**

Given the phone number dataset ([Phone Numbers.xlsx](https://hackertrail.s3.amazonaws.com/assets/code-boss/Phone_Numbers.xlsx)), identify and reformat the Singapore phone number:
•  The formatted number should be 8-digit with prefix of [3, 6, 8, 9]. Refer to sample in [Cleansed] tab.
•  For identified Singapore phone number, the Country Code should be “SG - Singapore"

You will be evaluated in terms of:

| Task                                                         | Points    |
| ------------------------------------------------------------ | --------- |
| Provide 5 findings and solutions                             | 18 points |
| Cleanse the Singapore phone number and output to [Cleansed] tab | 42 points |

### The five findings 

Following are the findings

## Multiple phone numbers 

Some users gave multiple phone numbers.
The phone numbers are delimited by `',', ';', '/'`. 

The solution is to create new rows, with the same customer information.

    rows_with_duplicates = []
    
    for i,txt in enumerate(df["Phone Number"]):
        # basic universal cleansing
        txt = str(txt).replace(" ","").replace("-", "").replace(".", "")
        txt = txt.lower()
        if txt == "nan":
            txt = ""
            
        if txt == "63392801 TO 04":
            txt = "63392801;63392802;63392803;63392804"
            
        replacements = (',', ';', '/')
        for r in replacements:
            txt = txt.replace(r, '$$$$$')
        if '$$$$$' in txt:
            rows_with_duplicates.append(i)
            for tx in txt.split('$$$$$'):
                row = df.loc[i].copy()
                row["From Multiple"] = True
                row["Phone Number"] = tx
                df_copy = df_copy.append(row)
            else:
                continue
                
    df_copy = df_copy.reset_index(drop=True)
    df_copy = df_copy.drop("ID", axis=1)
    df = df_copy.drop(df.index[rows_with_duplicates])
    del df_copy
```    

We find an entry with such a phone number as an entry: `63392801 TO 04`. According to https://xkcd.com/1205/ It is not reasonable to write code to automate this. Therefore I have hardcode this edge case.

    if txt == "63392801 TO 04":
        txt = "63392801;63392802;63392803;63392804"
```

### Country code in Number


```

```
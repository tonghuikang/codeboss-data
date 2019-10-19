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

Following are the five findings.

### Multiple phone numbers 

Some users gave multiple phone numbers.
The phone numbers are delimited by `',', ';', '/'`. 

The solution is to create new rows, with the same customer information.

We find an entry with such a phone number as an entry: `63392801 TO 04`. According to https://xkcd.com/1205/ It is not reasonable to write code to automate this. Therefore I have hardcode this edge case. 

### Contain Hex
Some phone numbers are given in Hex keys, like `0x1DB562C` or `1A62 197F`. We will parse them into integer if possible.

### Missing information
We will retain the entry. There are 12 people with missing country code and 19 people with missing Phone number. 

If the phone number is valid we will assume that it is a Singapore country code. After this step, only two people have empty country code.

## Results
We have 873 phone numbers that are Singapore-based and valid.
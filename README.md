# Part I - Data Cleansing

**Part I - Phone number data cleansing (60 points)**

Given the phone number dataset ([Phone Numbers.xlsx](https://hackertrail.s3.amazonaws.com/assets/code-boss/Phone_Numbers.xlsx)), identify and reformat the Singapore phone number:

- The formatted number should be 8-digit with prefix of [3, 6, 8, 9]. Refer to sample in [Cleansed] tab.
- For identified Singapore phone number, the Country Code should be “SG - Singapore"

You will be evaluated in terms of:

| Task                                                         | Points    |
| ------------------------------------------------------------ | --------- |
| Provide 5 findings and solutions                             | 18 points |
| Cleanse the Singapore phone number and output to [Cleansed] tab | 42 points |

Following are the five findings. The processing is done in a [notebook](./cleanse.ipynb). The output is [cleansed.csv](./cleansed.csv), which is copied to the input excel file.

### Multiple phone numbers 

Some users gave multiple phone numbers.
The phone numbers are delimited by `',', ';', '/'`. 

The solution is to create new rows, with the same customer information. Each new row will have one of the different phone number.

### Multiple phone numbers - an crazy edge case

We find an entry with such a phone number as an entry: `63392801 TO 04`. According to https://xkcd.com/1205/ It is not reasonable to write code to automate this. Therefore I have hardcode this edge case. 

### Contains Hex
Some phone numbers are given in Hex keys, like `0x1DB562C` or `1A62 197F`. We will parse them into integer if possible.

### Missing information
We will retain the entry. There are 12 people with missing country code and 19 people with missing Phone number.

If the phone number is valid we will assume that it is a Singapore country code. After this step, only two people have empty country code.

### Invalid phone numbers
Some phone numbers are too short (does not have the require 8 numbers for Singapore-based numbers). This will still be used as the Cleaned Phone Number. To identify invalid phone number the downstream processing can read from the column Valid.

### Results and additional measures
We have 873 phone numbers that are Singapore-based and valid.

We want to retain the original information for checking. We also have indicators on how the data is processed, so error accountability and future improvements.


# Part II - Prediction model

For Part II, please read [https://www.kaggle.com/huikang/housing-model](https://www.kaggle.com/huikang/housing-model/edit).
# Datastream API (DSWS) Median Index Data

[This article comes from the Developer Community Portal, where you may find more such articles.](https://developers.refinitiv.com/en/article-catalog/article/dsws-median-index-data)

In this article, we will create a Python function that will take the median measure of all (non 'NaN') values of a specific field for any index (or list of indices) of choice using Refinitiv's [DataStream](https://www.refinitiv.com/en/products/datastream-macroeconomic-analysis) Web Services (DSWS).

## Contents:

* [Get Coding](#GetCoding)
    * [Import Libraries](#ImportLibraries)
    * [Collecting Data: A Simple Example](#CollectingData)
    * [Creating Python Function to programmatically collect data](#CreatingPythonFunctiontoprogrammaticallycollectdata)
        * [Example setting 'track_progress' and 'add_to_global_DF' to True](#Exampletrack_progresandadd_to_global_DFtoTrue)

## Get Coding <a class="anchor" id="GetCoding"></a>

### Import Libraries <a class="anchor" id="ImportLibraries"></a>


For full replication, note that the version of libraries used


```python
import sys # ' sys ' is only needed to display our Pyhon version
print("This code is running on Python version " + sys.version[0:5])
```

    This code is running on Python version 3.7.7
    


We need to gather our data. Since **Refinitiv's [DataStream](https://www.refinitiv.com/en/products/datastream-macroeconomic-analysis) Web Services (DSWS)** allows for access to ESG data covering nearly 70% of global market cap and over 400 metrics, naturally it is more than appropriate. We can access DSWS via the Python library "DatastreamDSWS" that can be installed simply by using $\textit{pip install}$.


```python
import DatastreamDSWS as DSWS

# We can use our Refinitiv's Datastream Web Socket (DSWS) API keys that allows us to be identified by
# Refinitiv's back-end services and enables us to request (and fetch) data:
# Credentials are placed in a text file so that it may be used in this code without showing it itself.
(DSWS_username, DSWS_password) = (open("Datastream_username.txt","r"),
                                  open("Datastream_password.txt","r"))

ds = DSWS.Datastream(username = str(DSWS_username.read()),
                     password = str(DSWS_password.read()))

# It is best to close the files we opened in order to make sure that we don't stop any other
# services/programs from accessing them if they need to.
DSWS_username.close()
DSWS_password.close()


# # Alternatively one can use the following:
# import getpass
# dsusername = input()
# dspassword = getpass.getpass()
# ds = DSWS.Datastream(username = dsusername, password = dspassword)
```

The libraries in the cell bellow are  native to Python.


```python
import calendar # This library will be used to get the last day of any one month.
from datetime import date # ' datetime ' and ' date ' is crucial to manipulate dates.
import datetime # ' datetime ' and ' date ' is crucial to manipulate dates.
```

The libraries in the cell bellow are not native to Python - *id est* (*i.e.*): they are not installed upon Python's installation. This means that they have their own version independently of Python's version used.


```python
import dateutil # ' datetime ' and ' date ' is crucial to manipulate dates.
import numpy as np
import pandas as pd
for i,j in zip(["dateutil", "np","pd"],
               [ dateutil,   np,  pd]):
    print(f"The {i} library imported in this code is version: {j.__version__}")
```

    The dateutil library imported in this code is version: 2.8.1
    The np library imported in this code is version: 1.18.5
    The pd library imported in this code is version: 1.1.4
    

### Collecting Data: A simple Example <a class="anchor" id="CollectingData"></a>

1st: We have to specify our list of fields. In this example, we have:
* EVT1FD12: Enterprise Value's ForwarD contract with 12 month maturity (12FRW).
* EBT1FD12: Earnings Before Taxes' 12FRW.
* EBD1FD12: Earnings Before Depreciation and amortisation's 12FRW.
* X(CPS1FD12)*X(IBNOSH): product of the Cashflow Per Share amount's 12FRW and the Institutional Brokers Estimate Service( i.e.: I/B/E/S pulled from datastream's estimate data)'s Number Of Shares.
* X(MV)~IBCUR: Market Value IBES currency.
* PEFD12: market share Price to Equity ratio's 12FRW.
* SAL1FD12: SALes' 12FRW.
* X(BPS1FD12)*X(IBNOSH): product of the Book value Per Share's 12FRW and the Institutional Brokers Estimate Service's Number Of Shares.

N.B.: X is the variable, so X(...)*X(...) means that we multiply them


```python
list_of_fields = ['EVT1FD12', 'EBT1FD12', 'EBD1FD12', 'X(CPS1FD12)*X(IBNOSH)',
                  'X(MV)~IBCUR', 'PEFD12', 'SAL1FD12', 'X(BPS1FD12)*X(IBNOSH)']
```

Now that we know the fields that we want to capture, we will ask for DSWS to collect such data for all constituents of the [MSCI World Index](https://product.datastream.com/browse/search.aspx?dsid=ZRQW955&AppGroup=DSAddin&q=MSWRLD%24&prev=99_MSCI+World). We need to do a few changed to the mnemonics/tickers used in the DSWS function ' ds.get_data ':
* We need to add an 'L' at the start to indicate that we are requesting for the list of the constituents of the index. 
* We need to remove '\$' as it is not recognised by the backend. We need to remove all currency symbols for this to work.
* We need to add the month and year (in mmyy format) at the end to specify the point in time that we are trying to replicate. This means that we are capturing data for the list of constituents of that index on that month.
* We need to add '|L' at the end to indicate to the DSWS service that we are requesting data for a list, not a single object.

N.B.: ``` start = '2013-08-31' ``` collects data from August 2013. If someone was to use ``` ds.get_data("LMSWRLD0313|L", start = '2014-08-31') ```, they'd be collecting data starting in August 2014 for the constituents listed under the MSWRLD index back in March 2013.


```python
df = ds.get_data("LMSWRLD0313|L",
                 ['NAME',
                  list_of_fields[0]],
                 start = '2013-08-31',
                 kind = 0)
```

Now that we have stored the data we are looking for in the Python object 'df', we can sort through it:


```python
# ' df["Datatype"] == "EVT1FD12" ' here sieves through ' df ' and only
#    returns data where what is in the outer most square brackets is
#    true, i.e.: where values in the 'Datatype' column is 'EVT1FD12'.
df[df["Datatype"] == "EVT1FD12"] # Note that ' "EVT1FD12" ' is the same as ' list_of_fields[0] '
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Instrument</th>
      <th>Datatype</th>
      <th>Value</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1608</th>
      <td>MS:65955</td>
      <td>EVT1FD12</td>
      <td>NA</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1609</th>
      <td>MS:1016</td>
      <td>EVT1FD12</td>
      <td>49373.9</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1610</th>
      <td>MS:388</td>
      <td>EVT1FD12</td>
      <td>52651.6</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1611</th>
      <td>MS:10</td>
      <td>EVT1FD12</td>
      <td>54133.7</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1612</th>
      <td>MS:96942</td>
      <td>EVT1FD12</td>
      <td>77434.2</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3211</th>
      <td>MS:65552</td>
      <td>EVT1FD12</td>
      <td>11510.2</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3212</th>
      <td>MS:3695</td>
      <td>EVT1FD12</td>
      <td>6298.67</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3213</th>
      <td>MS:3698</td>
      <td>EVT1FD12</td>
      <td>NA</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3214</th>
      <td>MS:4502</td>
      <td>EVT1FD12</td>
      <td>NA</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3215</th>
      <td>MS:2138</td>
      <td>EVT1FD12</td>
      <td>82122.3</td>
      <td>2013-08-31</td>
    </tr>
  </tbody>
</table>
<p>1608 rows × 4 columns</p>
</div>



There are a lot of repeated values, let's use ' .unique() ' to only retrieve unique values within the 'Instrument' column:


```python
df[df["Instrument"] == df["Instrument"].unique()[0]] # ' [0] ' here is needed to indicate that we want the 0th unique value in question.
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Instrument</th>
      <th>Datatype</th>
      <th>Value</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MS:65955</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK A</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1608</th>
      <td>MS:65955</td>
      <td>EVT1FD12</td>
      <td>NA</td>
      <td>2013-08-31</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df["Datatype"] == list_of_fields[0]]
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Instrument</th>
      <th>Datatype</th>
      <th>Value</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1608</th>
      <td>MS:65955</td>
      <td>EVT1FD12</td>
      <td>NA</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1609</th>
      <td>MS:1016</td>
      <td>EVT1FD12</td>
      <td>49373.9</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1610</th>
      <td>MS:388</td>
      <td>EVT1FD12</td>
      <td>52651.6</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1611</th>
      <td>MS:10</td>
      <td>EVT1FD12</td>
      <td>54133.7</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>1612</th>
      <td>MS:96942</td>
      <td>EVT1FD12</td>
      <td>77434.2</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3211</th>
      <td>MS:65552</td>
      <td>EVT1FD12</td>
      <td>11510.2</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3212</th>
      <td>MS:3695</td>
      <td>EVT1FD12</td>
      <td>6298.67</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3213</th>
      <td>MS:3698</td>
      <td>EVT1FD12</td>
      <td>NA</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3214</th>
      <td>MS:4502</td>
      <td>EVT1FD12</td>
      <td>NA</td>
      <td>2013-08-31</td>
    </tr>
    <tr>
      <th>3215</th>
      <td>MS:2138</td>
      <td>EVT1FD12</td>
      <td>82122.3</td>
      <td>2013-08-31</td>
    </tr>
  </tbody>
</table>
<p>1608 rows × 4 columns</p>
</div>




```python
print(list_of_fields[0]) # Printing out the field of interest's name
df[df["Datatype"] == list_of_fields[0]][df["Value"] != 'NA']["Value"].median() # ' .median() ' gets us - you guessed it - the median value.
```

    EVT1FD12
    

    C:\Users\U6082174.TEN\AppData\Roaming\Python\Python37\site-packages\ipykernel_launcher.py:2: UserWarning: Boolean Series key will be reindexed to match DataFrame index.
      
    




    11409.6



### Creating Python Function to programmatically collect data <a class="anchor" id="CreatingPythonFunctiontoprogrammaticallycollectdata"></a>


```python
def DSWS_Median_Index_Data(indices = ["MSWRLD"],
                           list_of_fields = ['EVT1FD12', 'EBT1FD12', 'EBD1FD12', 'X(CPS1FD12)*X(IBNOSH)',
                                             'X(MV)~IBCUR', 'PEFD12', 'SAL1FD12', 'X(BPS1FD12)*X(IBNOSH)'], # Don't include non numerical fields like 'GDSCN'.
                          start = '2013-01-01',
                          end = '2021-01-31',
                          track_progress = False,
                          add_to_global_DF = False):
    """
    ' DSWS_Median_Index_Data ' requests data defined in ' list_of_fields ' from Datastream's API - DataStream Web
    Services (DSWS) - for a series of indices of choice - defined in 'indices' - and returns three lists full of Pandas data-frames:
    1st - the raw output from the requests (with columns 'Instrument', 'Datatype', 'Value' and 'Dates');
    2nd - the monthly median from the raw output from the requests (with columns of the requested metrics and an index of dates);
    3rd - the raw data pulled from the DSWS request (and where issues are most likely to lie).
    
    One could re-write this basing themselves off datetime objects, it would be equivalent; its code may look neater too.
    
    indices (list): List of strings of the DSWS mnemonic for the index for which data is requested.
    Default: indices = ["MSWRLD"]
    
    list_of_fields (list): List of strings of the DSWS fields we are after. This has to be comprised of 49 elements or less.
    Don't include non numerical fields like 'GDSCN'. That will result in a printed error
    Default: list_of_fields = ['EVT1FD12', 'EBT1FD12', 'EBD1FD12', 'X(CPS1FD12)*X(IBNOSH)', 'X(MV)~IBCUR', 'PEFD12', 'SAL1FD12', 'X(BPS1FD12)*X(IBNOSH)', '(X(SAL1FD12)*X(IBUNIT))', '354E(X)', 'X(INC1FD12)*X(IBUNIT)', 'X(FCF1FD12)*X(IBNOSH)', 'X(FCF1FD12)*X(IBNOSH)*X(IBUNIT)', 'GDSCN']
    
    start (str): String of the start date from which we are asking for data in 'yyy-mm-dd' format.
    Default: start = '2013-01-01'
    
    end (str): String of the end date until which we are asking for data in 'yyy-mm-dd' format.
    Default: end = '2021-01-31'
    
    track_progress (Boolean): If set to True, the ' DSWS_Median_Index_Data ' function will print out each mnemonic requested of DSWS
    Default: track_progress = False
    
    
    track_progress (Boolean): If set to True, each string of the transformed index will be printed off - remember that there is one per month.
    Default: track_progress = False
    
    add_to_global_DF (Boolean): If set to True, on top of returning the 3 lists of Pandas data-frames described above, this function will append lists named DF, _DF, and debug_df.
    This does mean that you need to include a line such as 'DF, _DF, debug_df = [], [], []' beforehand as a result.
    Default: add_to_global_DF = False
    """
    
    # We would like to keep the name of the companies in question.
    if 'NAME' not in list_of_fields:
        list_of_fields = ['NAME'] + list_of_fields
    
    # We are often going to need to split our dates into more useful objects, that is what 'Proccess_Date' does: 
    def Proccess_Date(date):
        d = date.split("-")
        year, year_2, month = d[0], d[0][2:4], d[1]
        day = calendar.monthrange(int(year), int(month))[1] # gets last day for that month
        return(year, year_2, month, day)
    
    # Finding the number of months between ' start ' and ' end '.
    from_year, from_year_2, from_month, from_day = Proccess_Date(date = start)
    to_year, to_year_2, to_month, to_day = Proccess_Date(date = end)
    start_date = datetime.datetime(int(from_year), int(from_month), int(from_day))
    end_date = datetime.datetime(int(to_year), int(to_month), int(to_day))
    num_months = (end_date.year - start_date.year) * 12 + (end_date.month - start_date.month) + 1 # ' + 1 ' to include the last month.
    
    if add_to_global_DF == True:
        # If the user is afraid that the function could fail halfway through,
        #    (s)he can append an existing data-frame via this if statement.
        global DF
        global _DF
        global debug_df
    else:
        DF, _DF, debug_df = [], [], [] # These ate the lists of the data-frames of interest that will be populated in the following loop.
    
    for a in indices: # Iterating through the list of indices:
        df_list = [] # List to be appended/populated with the for loop bellow.
        # for d in range(num_months+2): # ' +1 ' since the ' range ' function is exclusive with respect to its upper limit, and an additional 1 for go over the month inclusive n the range of the argument.
        for d in range(num_months):
            _start_date = start_date + dateutil.relativedelta.relativedelta(months=+d)
            from_year, from_year_2, from_month, from_day = Proccess_Date(date = _start_date.strftime("%Y-%m-%d"))

            if track_progress == True:
                print(f"L{a}{from_month}{from_year_2}|L")

            df_list.append(
                ds.get_data(
                    tickers = f"L{a}{from_month}{from_year_2}|L",
                    fields = list_of_fields,
                    start = _start_date.strftime("%Y-%m-%d"),
                    kind = 0))

        df = pd.concat(df_list).reset_index(drop = True)
        
        date_range = df[df["Dates"].notna()]["Dates"].unique()
        
        debug_df.append(df)
        
        # This try loop is in case a field value requests non-numerical data that would break the code (since a median value could then not be computed).
        try:
            _df = pd.DataFrame(
                data = [[df[df["Value"] != "NA"][df["Datatype"] == i][df["Dates"] == j]["Value"].median()
                         for i in list_of_fields[1:]] for j in date_range], # ' list_of_fields[1:] ' as opposed to ' list_of_fields ' because we don't want 'NAME'.
                columns = pd.MultiIndex.from_product([[a], list_of_fields[1:]],
                                                     names = ['Index', 'Metrics']),
                index = date_range)
        except:
            for i in list_of_fields[1:]:
                for j in date_range:
                    try:
                        df[df["Value"] != "NA"][df["Datatype"] == i][df["Dates"] == j]["Value"].median()
                    except:
                        print(f"field '{i}' does not return numerical data; a median could thus not be computed for it.")
                        print("The program has stopped. Please run it again without this field.")
        
        DF.append(df)
        _DF.append(_df)
    return DF, _DF, debug_df
```

#### Example setting 'track_progress' and 'add_to_global_DF' to True: <a class="anchor" id="Exampletrack_progresandadd_to_global_DFtoTrue"></a>

Note that - in this example - we made sure to normalize all currency-denominated values to the same currency (USD), otherwise taking the median value of different currencies wouldn't make much sense.


```python
DF, _DF, debug_df = [], [], []

test1, test1_df, test1_deb_df = DSWS_Median_Index_Data(
    indices = ["MSWRLD", "S&PCOMP"],
    list_of_fields = ['X(EVT1FD12)~USD', 'X(EBT1FD12)~USD', 'X(EBD1FD12)~USD', 'X(CPS1FD12)~USD*X(IBNOSH)',
                      'X(MV)~USD', 'X(PEFD12)', 'X(SAL1FD12)~USD', 'X(BPS1FD12)~USD*X(IBNOSH)'],
    start = '2013-01-01',
    end = '2013-03-01',
    track_progress = True,
    add_to_global_DF = True)
```

    LMSWRLD0113|L
    LMSWRLD0213|L
    LMSWRLD0313|L
    

    C:\Users\U6082174.TEN\AppData\Roaming\Python\Python37\site-packages\ipykernel_launcher.py:96: UserWarning: Boolean Series key will be reindexed to match DataFrame index.
    

    LS&PCOMP0113|L
    LS&PCOMP0213|L
    LS&PCOMP0313|L
    


```python
test1[0]
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Instrument</th>
      <th>Datatype</th>
      <th>Value</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MS:65955</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK A</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>MS:1016</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK B</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MS:388</td>
      <td>NAME</td>
      <td>ABB LTD N</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MS:10</td>
      <td>NAME</td>
      <td>ABBOTT LABORATORIES</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MS:96942</td>
      <td>NAME</td>
      <td>ABBVIE</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>43447</th>
      <td>MS:65552</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>6266.1</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43448</th>
      <td>MS:3695</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>3074.03</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43449</th>
      <td>MS:3698</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>34543.6</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43450</th>
      <td>MS:4502</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>4837.31</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43451</th>
      <td>MS:2138</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>20133.9</td>
      <td>2013-03-31</td>
    </tr>
  </tbody>
</table>
<p>43452 rows × 4 columns</p>
</div>




```python
test1_df[0]
```





<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Index</th>
      <th colspan="8" halign="left">MSWRLD</th>
    </tr>
    <tr>
      <th>Metrics</th>
      <th>X(EVT1FD12)~USD</th>
      <th>X(EBT1FD12)~USD</th>
      <th>X(EBD1FD12)~USD</th>
      <th>X(CPS1FD12)~USD*X(IBNOSH)</th>
      <th>X(MV)~USD</th>
      <th>X(PEFD12)</th>
      <th>X(SAL1FD12)~USD</th>
      <th>X(BPS1FD12)~USD*X(IBNOSH)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-31</th>
      <td>9768.0295</td>
      <td>1008.731</td>
      <td>1159.4745</td>
      <td>1033.7630</td>
      <td>9083.045</td>
      <td>13.9340</td>
      <td>5136.3315</td>
      <td>5321.7885</td>
    </tr>
    <tr>
      <th>2013-02-28</th>
      <td>9748.7150</td>
      <td>993.057</td>
      <td>1166.6150</td>
      <td>1045.0710</td>
      <td>9107.255</td>
      <td>14.3305</td>
      <td>5113.3065</td>
      <td>5254.4770</td>
    </tr>
    <tr>
      <th>2013-03-31</th>
      <td>9876.2530</td>
      <td>1000.378</td>
      <td>1151.1720</td>
      <td>1037.7785</td>
      <td>9345.155</td>
      <td>14.8205</td>
      <td>5117.3000</td>
      <td>5243.3455</td>
    </tr>
  </tbody>
</table>
</div>




```python
test1_df[1]
```





<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Index</th>
      <th colspan="8" halign="left">S&amp;PCOMP</th>
    </tr>
    <tr>
      <th>Metrics</th>
      <th>X(EVT1FD12)~USD</th>
      <th>X(EBT1FD12)~USD</th>
      <th>X(EBD1FD12)~USD</th>
      <th>X(CPS1FD12)~USD*X(IBNOSH)</th>
      <th>X(MV)~USD</th>
      <th>X(PEFD12)</th>
      <th>X(SAL1FD12)~USD</th>
      <th>X(BPS1FD12)~USD*X(IBNOSH)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-31</th>
      <td>14746.49</td>
      <td>1403.990</td>
      <td>1956.5220</td>
      <td>1353.3355</td>
      <td>13275.135</td>
      <td>14.0380</td>
      <td>9011.652</td>
      <td>5988.997</td>
    </tr>
    <tr>
      <th>2013-02-28</th>
      <td>15450.20</td>
      <td>1404.525</td>
      <td>1910.5655</td>
      <td>1371.0870</td>
      <td>13112.900</td>
      <td>14.4570</td>
      <td>9073.121</td>
      <td>5870.180</td>
    </tr>
    <tr>
      <th>2013-03-31</th>
      <td>15799.75</td>
      <td>1411.040</td>
      <td>1921.3090</td>
      <td>1368.2955</td>
      <td>13821.085</td>
      <td>14.8685</td>
      <td>9089.930</td>
      <td>5936.011</td>
    </tr>
  </tbody>
</table>
</div>




```python
test1_deb_df[0]
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Instrument</th>
      <th>Datatype</th>
      <th>Value</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MS:65955</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK A</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>MS:1016</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK B</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MS:388</td>
      <td>NAME</td>
      <td>ABB LTD N</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MS:10</td>
      <td>NAME</td>
      <td>ABBOTT LABORATORIES</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MS:96942</td>
      <td>NAME</td>
      <td>ABBVIE</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>43447</th>
      <td>MS:65552</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>6266.1</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43448</th>
      <td>MS:3695</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>3074.03</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43449</th>
      <td>MS:3698</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>34543.6</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43450</th>
      <td>MS:4502</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>4837.31</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43451</th>
      <td>MS:2138</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>20133.9</td>
      <td>2013-03-31</td>
    </tr>
  </tbody>
</table>
<p>43452 rows × 4 columns</p>
</div>




```python
DF[0]
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Instrument</th>
      <th>Datatype</th>
      <th>Value</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MS:65955</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK A</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>MS:1016</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK B</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MS:388</td>
      <td>NAME</td>
      <td>ABB LTD N</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MS:10</td>
      <td>NAME</td>
      <td>ABBOTT LABORATORIES</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MS:96942</td>
      <td>NAME</td>
      <td>ABBVIE</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>43447</th>
      <td>MS:65552</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>6266.1</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43448</th>
      <td>MS:3695</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>3074.03</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43449</th>
      <td>MS:3698</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>34543.6</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43450</th>
      <td>MS:4502</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>4837.31</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43451</th>
      <td>MS:2138</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>20133.9</td>
      <td>2013-03-31</td>
    </tr>
  </tbody>
</table>
<p>43452 rows × 4 columns</p>
</div>




```python
_DF[0]
```





<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Index</th>
      <th colspan="8" halign="left">MSWRLD</th>
    </tr>
    <tr>
      <th>Metrics</th>
      <th>X(EVT1FD12)~USD</th>
      <th>X(EBT1FD12)~USD</th>
      <th>X(EBD1FD12)~USD</th>
      <th>X(CPS1FD12)~USD*X(IBNOSH)</th>
      <th>X(MV)~USD</th>
      <th>X(PEFD12)</th>
      <th>X(SAL1FD12)~USD</th>
      <th>X(BPS1FD12)~USD*X(IBNOSH)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-31</th>
      <td>9768.0295</td>
      <td>1008.731</td>
      <td>1159.4745</td>
      <td>1033.7630</td>
      <td>9083.045</td>
      <td>13.9340</td>
      <td>5136.3315</td>
      <td>5321.7885</td>
    </tr>
    <tr>
      <th>2013-02-28</th>
      <td>9748.7150</td>
      <td>993.057</td>
      <td>1166.6150</td>
      <td>1045.0710</td>
      <td>9107.255</td>
      <td>14.3305</td>
      <td>5113.3065</td>
      <td>5254.4770</td>
    </tr>
    <tr>
      <th>2013-03-31</th>
      <td>9876.2530</td>
      <td>1000.378</td>
      <td>1151.1720</td>
      <td>1037.7785</td>
      <td>9345.155</td>
      <td>14.8205</td>
      <td>5117.3000</td>
      <td>5243.3455</td>
    </tr>
  </tbody>
</table>
</div>




```python
debug_df[0]
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Instrument</th>
      <th>Datatype</th>
      <th>Value</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MS:65955</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK A</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>MS:1016</td>
      <td>NAME</td>
      <td>A P MOLLER MAERSK B</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MS:388</td>
      <td>NAME</td>
      <td>ABB LTD N</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MS:10</td>
      <td>NAME</td>
      <td>ABBOTT LABORATORIES</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MS:96942</td>
      <td>NAME</td>
      <td>ABBVIE</td>
      <td>2013-01-31</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>43447</th>
      <td>MS:65552</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>6266.1</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43448</th>
      <td>MS:3695</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>3074.03</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43449</th>
      <td>MS:3698</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>34543.6</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43450</th>
      <td>MS:4502</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>4837.31</td>
      <td>2013-03-31</td>
    </tr>
    <tr>
      <th>43451</th>
      <td>MS:2138</td>
      <td>X(BPS1FD12)~USD*X(IBNOSH)</td>
      <td>20133.9</td>
      <td>2013-03-31</td>
    </tr>
  </tbody>
</table>
<p>43452 rows × 4 columns</p>
</div>



You can find information inscribed inbetween the triple double quotes (*i.e.*:""" """) above with the Python functino ' help() ':


```python
help(DSWS_Median_Index_Data)
```

    Help on function DSWS_Median_Index_Data in module __main__:
    
    DSWS_Median_Index_Data(indices=['MSWRLD'], list_of_fields=['EVT1FD12', 'EBT1FD12', 'EBD1FD12', 'X(CPS1FD12)*X(IBNOSH)', 'X(MV)~IBCUR', 'PEFD12', 'SAL1FD12', 'X(BPS1FD12)*X(IBNOSH)'], start='2013-01-01', end='2021-01-31', track_progress=False, add_to_global_DF=False)
        ' DSWS_Median_Index_Data ' requests data defined in ' list_of_fields ' from Datastream's API - DataStream Web
        Services (DSWS) - for a series of indices of choice - defined in 'indices' - and returns three lists full of Pandas data-frames:
        1st - the raw output from the requests (with columns 'Instrument', 'Datatype', 'Value' and 'Dates');
        2nd - the monthly median from the raw output from the requests (with columns of the requested metrics and an index of dates);
        3rd - the raw data pulled from the DSWS request (and where issues are most likely to lie).
        
        One could re-write this basing themselves off datetime objects, it would be equivalent; its code may look neater too.
        
        indices (list): List of strings of the DSWS mnemonic for the index for which data is requested.
        Default: indices = ["MSWRLD"]
        
        list_of_fields (list): List of strings of the DSWS fields we are after. This has to be comprised of 49 elements or less.
        Don't include non numerical fields like 'GDSCN'. That will result in a printed error
        Default: list_of_fields = ['EVT1FD12', 'EBT1FD12', 'EBD1FD12', 'X(CPS1FD12)*X(IBNOSH)', 'X(MV)~IBCUR', 'PEFD12', 'SAL1FD12', 'X(BPS1FD12)*X(IBNOSH)', '(X(SAL1FD12)*X(IBUNIT))', '354E(X)', 'X(INC1FD12)*X(IBUNIT)', 'X(FCF1FD12)*X(IBNOSH)', 'X(FCF1FD12)*X(IBNOSH)*X(IBUNIT)', 'GDSCN']
        
        start (str): String of the start date from which we are asking for data in 'yyy-mm-dd' format.
        Default: start = '2013-01-01'
        
        end (str): String of the end date until which we are asking for data in 'yyy-mm-dd' format.
        Default: end = '2021-01-31'
        
        track_progress (Boolean): If set to True, the ' DSWS_Median_Index_Data ' function will print out each mnemonic requested of DSWS
        Default: track_progress = False
        
        
        track_progress (Boolean): If set to True, each string of the transformed index will be printed off - remember that there is one per month.
        Default: track_progress = False
        
        add_to_global_DF (Boolean): If set to True, on top of returning the 3 lists of Pandas data-frames described above, this function will append lists named DF, _DF, and debug_df.
        This does mean that you need to include a line such as 'DF, _DF, debug_df = [], [], []' beforehand as a result.
        Default: add_to_global_DF = False
    
    


```python

```

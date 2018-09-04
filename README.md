# HW1.2
import pandas as pd
import numpy as np


data = pd.read_csv('/Users/Yihe/Desktop/Input.csv', index_col = 0)

# Have a glance of the original data frame
data.head(5)
shape = data.shape
num_of_columns = len(data.columns)
num_of_row = len(data.index)


# Reshape the data frame
yearlist = list(data.columns.values)
statelist = list(data.index.values)
divorce_list = list(data.columns.values)[0:15]
marriage_list = list(data.columns.values)[15:31]

def data_by_state(state):
    d = pd.DataFrame(0, index=np.arange(15), columns=["State","Year","Divorce rate", "Marriage rate"])
    d["State"] = state
    d["Divorce rate"] = list(data[j][state] for j in divorce_list)
    d["Marriage rate"] = list(data[j][state] for j in marriage_list)
    d["Year"] = [2011, 2010, 2009,2008,2007,2006,2005,2004,2003,2002,2001, 2000, 1999, 1995, 1990]
    return d
list3 = list(data_by_state(state) for state in statelist[1:])
new_df = data_by_state("Alabama").append(list3,ignore_index=True)

# export to local path

new_df.to_csv('/Users/Yihe/Desktop/data science- traffic pattern/Output.csv', sep=',',encoding='utf-8')

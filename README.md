```import pandas as pd
import numpy as np
import warnings
warnings.filterwarnings('ignore')
df=pd.read_csv(r"C:\Users\InGo Electric\Downloads\Ingorawdata.CAN",sep=";")
df.fillna(0,inplace=True)
df.replace(['0x',''], ['',''], regex=True,inplace=True)
df.drop(columns="Unnamed: 12",inplace=True)
df1=df[df['ID'].str.contains('115')]
def res(D0):
    if D0=="80":
        return "Success"
    elif D0=="60":
        return "Failure"
df1["Ack Responce"]=df1["D0"].apply(res)
df1['Voltage'] = df1['D2'] + df1['D1']
df1["Voltage"]=df1["Voltage"].apply(lambda x:str(int(str(x),16)))
df1['Voltage'] = df1['Voltage'].astype(float) *0.001
df1['Current'] = df1['D4']+df1['D3']
df1["Current"]=df1["Current"].apply(lambda x:str(int(str(x),16)))
df1['Current'] = df1['Current'].astype(float) *0.001
df1['D5'] = [chr(int(x, 16)) for x in df1['D5']]
def res(D5):
    if D5=="C":
        return "Charging"
    elif D5=="D":
        return "Dis Charging"
    elif D5=="N":
        return "idle"
df1["Current Response"]=df1["D5"].apply(res)
df1["Temperature"]=df1["D6"].apply(lambda x:str(int(str(x),16)))
df1["SOC"]=df1["D7"].apply(lambda x:str(int(str(x),16)))
df2=df[df['ID'].str.contains('116')]
df2['B'] = df2['D6'] + df2['D5']
df2["B"]=df2["B"].apply(int, base=16).apply(bin)
df3=df2.replace(["0b",""],["",""],regex=True)
df3['B'].str.split()
df3['B'].str.split()
df4=df3['B'].str.split(pat = '', expand = True)
cols = [0,14,15,16,17]
df4.drop(df4.columns[cols], axis=1, inplace=True)
df4.columns =['cell1','cell2','cell3','cell4','cell5','cell6','cell7','cell8','cell9','cell10','cell11','cell12','cell13']
given_set={"0"}
df4['cells working'] = df4.isin(given_set).sum(1)
given_set={"1"}
df4['gone cells'] = df4.isin(given_set).sum(1)
def res(cell1):
    if cell1=="1":
        return "Detected"
    elif cell1=="0":
        return "not Detected"
df4["OCDL"]=df4["cell1"].apply(res)
def res(cell2):
    if cell2=="1":
        return "Detected"
    elif cell2=="0":
        return "not Detected"
df4["OTF"]=df4["cell2"].apply(res)
def res(cell3):
    if cell3=="1":
        return "Detected"
    elif cell3=="0":
        return "not Detected"
df4["AFE alert"]=df4["cell3"].apply(res)
def res(cell4):
    if cell4=="1":
        return "Detected"
    elif cell4=="0":
        return "not Detected"
df4["UTD"]=df4["cell4"].apply(res)
def res(cell5):
    if cell5=="1":
        return "Detected"
    elif cell5=="0":
        return "not Detected"
df4["UTC"]=df4["cell5"].apply(res)
def res(cell6):
    if cell6=="1":
        return "Detected"
    elif cell6=="0":
        return "not Detected"
df4["OTD"]=df4["cell6"].apply(res)
def res(cell7):
    if cell7=="1":
        return "Detected"
    elif cell7=="0":
        return "not Detected"
df4["OTC"]=df4["cell7"].apply(res)
def res(cell8):
    if cell8=="1":
      return "Detected"
    elif cell8=="0":
      return "not Detected"
df4["ASCDL"]=df4["cell8"].apply(res)
def res(cell9):
    if cell9=="1":
        return "Detected"
    elif cell9=="0":
        return "NotDetected"
df4["ASCD"]=df4["cell9"].apply(res)
def res(cell10):
    if cell10=="1":
        return "Detected"
    elif cell10=="0":
        return "NotDetected"
df4["AOLDL"]=df4["cell10"].apply(res)
def res(cell11):
    if cell11=="1":
        return "Detected"
    elif cell11=="0":
        return "NotDetected"
df4["AOLD"]=df4["cell11"].apply(res)
def res(cell12):
    if cell12=="1":
        return "Detecetd"
    elif cell12=="0":
        return "NotDetected"
df4["OCD"]=df4["cell12"].apply(res)
def res(cell13):
    if cell13=="1":
        return "Detecetd"
    elif cell13=="0":
        return "NotDetected"
df4["OCC"]=df4["cell13"].apply(res)
df4.reset_index(drop=True, inplace=True)
df1.reset_index(drop=True, inplace=True)
final = pd.concat([df1,df4], axis = 1)```

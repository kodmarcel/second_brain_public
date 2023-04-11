---  
share: true  
tag: public  
---  
# Pandas  
  
## Show whole dataframe  
pandas show whole dataframe  
~~~  
search_output.to_string()  
search_output.to_markdown()  
print(search_output.to_csv()) # pobably the besty  
~~~  
  
  
## How to get a list from csv field  
[pandas list from csv](https://stackoverflow.com/questions/45758646/pandas-convert-string-into-list-of-strings)  
  
You can split the string manually:  
  
```python  
>>> df['Tags'] = df.Tags.apply(lambda x: x[1:-1].split(','))  
>>> df.Tags[0]  
['Tag1', 'Tag2']  
```  
  
Or apply it on load...`df = pd.read_csv('file.csv', sep='|', converters={'Tags': lambda x: x[1:-1].split(',')})`  
  
@JonClements, `converters={'Tags': lambda x: x[1:-1].split(',')}` just saved me so much headache. Thanks for this.  
  
  
### in case of tvdb for mediabiz i can use:  
```  
data.genre[0][2:-2].split("', '")  
data.title[0][2:-2].split("', '")  
```  

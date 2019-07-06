

```python
import numpy as np

import pandas as pd
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)

print('Imported Lib')
```

    Imported Lib



```python
tables = pd.read_html('https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M', header=0)

required_cols = ['Postcode', 'Borough','Neighbourhood']

for table in tables:
    if(str(np.array_equal(np.array(table.columns),np.array(required_cols)))=="True"):
        pstl_data_df = pd.DataFrame(table)    
    break
print("Dataframe: ",pstl_data_df.shape)
pstl_data_df.head()
```

    Dataframe:  (288, 3)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Postcode</th>
      <th>Borough</th>
      <th>Neighbourhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1A</td>
      <td>Not assigned</td>
      <td>Not assigned</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M2A</td>
      <td>Not assigned</td>
      <td>Not assigned</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Harbourfront</td>
    </tr>
  </tbody>
</table>
</div>




```python
pstl_data_df = pstl_data_df[pstl_data_df.Borough!="Not assigned"]
print("Shape of Dataframe is - ",pstl_data_df.shape)
pstl_data_df.head()
```

    Shape of Dataframe is -  (211, 3)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Postcode</th>
      <th>Borough</th>
      <th>Neighbourhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Harbourfront</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Regent Park</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Heights</td>
    </tr>
  </tbody>
</table>
</div>




```python
pstl_data_df['new_nghbr'] = np.where(pstl_data_df['Neighbourhood']=='Not assigned',pstl_data_df['Borough'],pstl_data_df['Neighbourhood'])
pstl_data_df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Postcode</th>
      <th>Borough</th>
      <th>Neighbourhood</th>
      <th>new_nghbr</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Harbourfront</td>
      <td>Harbourfront</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Regent Park</td>
      <td>Regent Park</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Heights</td>
      <td>Lawrence Heights</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Manor</td>
      <td>Lawrence Manor</td>
    </tr>
    <tr>
      <th>8</th>
      <td>M7A</td>
      <td>Queen's Park</td>
      <td>Not assigned</td>
      <td>Queen's Park</td>
    </tr>
    <tr>
      <th>10</th>
      <td>M9A</td>
      <td>Etobicoke</td>
      <td>Islington Avenue</td>
      <td>Islington Avenue</td>
    </tr>
    <tr>
      <th>11</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Rouge</td>
      <td>Rouge</td>
    </tr>
    <tr>
      <th>12</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Malvern</td>
      <td>Malvern</td>
    </tr>
  </tbody>
</table>
</div>




```python
can_postal_cd_df = pd.DataFrame(pstl_data_df.groupby(['Postcode','Borough'])['new_nghbr'].apply(','.join).reset_index())

can_postal_cd_df = can_postal_cd_df.rename(columns = {"Postcode": "PostalCode","new_nghbr":"Neighborhood"})
```


```python
print(can_postal_cd_df.head())
print("\n Dataframe: ",can_postal_cd_df.shape)
```

      PostalCode      Borough                          Neighborhood
    0        M1B  Scarborough                         Rouge,Malvern
    1        M1C  Scarborough  Highland Creek,Rouge Hill,Port Union
    2        M1E  Scarborough       Guildwood,Morningside,West Hill
    3        M1G  Scarborough                                Woburn
    4        M1H  Scarborough                             Cedarbrae
    
     Dataframe:  (103, 3)



```python

```

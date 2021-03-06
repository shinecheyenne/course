# Chapter 1.2 chipotle 주문 데이터 분석


```python
import pandas as pd
import numpy as np
%matplotlib inline 
#주피터 노트북에서 그래프 출력 가능하도록 선언
import matplotlib.pyplot as plt
```

(1) 기초정보


```python
#read_csv()함수로 데이터를 Dataframe형태로 불러옴
file_path = '../data/chipotle.tsv'
chipo = pd.read_csv(file_path, sep='\t')

print(chipo.shape)
print("-----------------------------------------------------------------")
print(chipo.info())
print("-----------------------------------------------------------------")
print(chipo.columns)
print("-----------------------------------------------------------------")
print(chipo.head(10))
print("-----------------------------------------------------------------")
print(chipo.index)
print("-----------------------------------------------------------------")

#type 변환
chipo['order_id']=chipo['order_id'].astype(str)

#수치형 피처 기초통계량 확인
print(chipo.describe())

#범주형 피처 개수 출력
print(len(chipo['order_id'].unique()))
print(len(chipo['item_name'].unique()))
```

    (4622, 5)
    -----------------------------------------------------------------
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4622 entries, 0 to 4621
    Data columns (total 5 columns):
     #   Column              Non-Null Count  Dtype 
    ---  ------              --------------  ----- 
     0   order_id            4622 non-null   int64 
     1   quantity            4622 non-null   int64 
     2   item_name           4622 non-null   object
     3   choice_description  3376 non-null   object
     4   item_price          4622 non-null   object
    dtypes: int64(2), object(3)
    memory usage: 180.7+ KB
    None
    -----------------------------------------------------------------
    Index(['order_id', 'quantity', 'item_name', 'choice_description',
           'item_price'],
          dtype='object')
    -----------------------------------------------------------------
       order_id  quantity                              item_name  \
    0         1         1           Chips and Fresh Tomato Salsa   
    1         1         1                                   Izze   
    2         1         1                       Nantucket Nectar   
    3         1         1  Chips and Tomatillo-Green Chili Salsa   
    4         2         2                           Chicken Bowl   
    5         3         1                           Chicken Bowl   
    6         3         1                          Side of Chips   
    7         4         1                          Steak Burrito   
    8         4         1                       Steak Soft Tacos   
    9         5         1                          Steak Burrito   
    
                                      choice_description item_price  
    0                                                NaN     $2.39   
    1                                       [Clementine]     $3.39   
    2                                            [Apple]     $3.39   
    3                                                NaN     $2.39   
    4  [Tomatillo-Red Chili Salsa (Hot), [Black Beans...    $16.98   
    5  [Fresh Tomato Salsa (Mild), [Rice, Cheese, Sou...    $10.98   
    6                                                NaN     $1.69   
    7  [Tomatillo Red Chili Salsa, [Fajita Vegetables...    $11.75   
    8  [Tomatillo Green Chili Salsa, [Pinto Beans, Ch...     $9.25   
    9  [Fresh Tomato Salsa, [Rice, Black Beans, Pinto...     $9.25   
    -----------------------------------------------------------------
    RangeIndex(start=0, stop=4622, step=1)
    -----------------------------------------------------------------
              quantity
    count  4622.000000
    mean      1.075725
    std       0.410186
    min       1.000000
    25%       1.000000
    50%       1.000000
    75%       1.000000
    max      15.000000
    1834
    50
    

(2) 탐색 및 시각화


```python
#value_counts()함수: 시리즈 객체에만 적용
#DataFrame['column']: 시리즈 객체 반환

item_count = chipo['item_name'].value_counts()[:10]

# print(item_count)

for idx, (val, cnt) in enumerate(item_count.iteritems(), 1):
    print("Top", idx, ":", val, cnt)
```

    Top 1 : Chicken Bowl 726
    Top 2 : Chicken Burrito 553
    Top 3 : Chips and Guacamole 479
    Top 4 : Steak Burrito 368
    Top 5 : Canned Soft Drink 301
    Top 6 : Steak Bowl 211
    Top 7 : Chips 211
    Top 8 : Bottled Water 162
    Top 9 : Chicken Soft Tacos 115
    Top 10 : Chips and Fresh Tomato Salsa 110
    


```python
#아이템별 주문 개수
order_count = chipo.groupby('item_name')['order_id'].count()
order_count[:10]
```




    item_name
    6 Pack Soft Drink         54
    Barbacoa Bowl             66
    Barbacoa Burrito          91
    Barbacoa Crispy Tacos     11
    Barbacoa Salad Bowl       10
    Barbacoa Soft Tacos       25
    Bottled Water            162
    Bowl                       2
    Burrito                    6
    Canned Soda              104
    Name: order_id, dtype: int64




```python
#아이템별 주문 총량
item_quantity = chipo.groupby('item_name')['quantity'].sum()
item_quantity[:10]
```




    item_name
    6 Pack Soft Drink         55
    Barbacoa Bowl             66
    Barbacoa Burrito          91
    Barbacoa Crispy Tacos     12
    Barbacoa Salad Bowl       10
    Barbacoa Soft Tacos       25
    Bottled Water            211
    Bowl                       4
    Burrito                    6
    Canned Soda              126
    Name: quantity, dtype: int64




```python
#시각화
item_name_list = item_quantity.index.tolist()
x_pos = np.arange(len(item_name_list))
order_cnt = item_quantity.values.tolist()

plt.bar(x_pos, order_cnt, align = 'center')
plt.title('Distribution of all ordered item')
plt.ylabel('ordered_item_count')

plt.show()
```


    
![png](output_8_0.png)
    



```python
plt.scatter(x_pos, order_cnt, c="r", alpha=0.4, label='scatter point', marker='^')
plt.ylabel('ordered_item_count')
plt.title('Distribution of all ordered item')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_9_0.png)
    


(3) 데이터 전처리


```python
#apply()함수는 시리즈 단위의 연산 처리하는 기능을 수행
chipo['item_price']=chipo['item_price'].apply(lambda x: float(x[1:]))
chipo.describe()
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
      <th>quantity</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4622.000000</td>
      <td>4622.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.075725</td>
      <td>7.464336</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.410186</td>
      <td>4.245557</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1.090000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000000</td>
      <td>3.390000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
      <td>8.750000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>9.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>15.000000</td>
      <td>44.250000</td>
    </tr>
  </tbody>
</table>
</div>



(4) 탐색적 분석


```python
#주문당 평균 계산금액
chipo.groupby('order_id')['item_price'].sum().describe()

#한 주문에 10달러 이상 지불한 주문 번호

chipo_orderid_group = chipo.groupby('order_id').sum()
results =chipo_orderid_group[chipo_orderid_group.item_price >=10]
print(results[:10])
print(results.index.values)

```

              quantity  item_price
    order_id                      
    1                4       11.56
    10               2       13.20
    100              2       10.08
    1000             2       20.50
    1001             2       10.08
    1002             2       10.68
    1003             2       13.00
    1004             2       21.96
    1005             3       12.15
    1006             8       71.40
    ['1' '10' '100' ... '997' '998' '999']
    


```python
#각 아이템의 가격 구하기
#sort_values(): series 데이터 정렬
chipo_one_item = chipo[chipo.quantity ==1]
price_per_item = chipo_one_item.groupby('item_name').min()
price_per_item.sort_values(by = 'item_price', ascending = False)[:10]
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
      <th>order_id</th>
      <th>quantity</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
    <tr>
      <th>item_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Steak Salad Bowl</th>
      <td>1032</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa, Lettuce]</td>
      <td>9.39</td>
    </tr>
    <tr>
      <th>Barbacoa Salad Bowl</th>
      <td>1283</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa, Guacamole]</td>
      <td>9.39</td>
    </tr>
    <tr>
      <th>Carnitas Salad Bowl</th>
      <td>1035</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>9.39</td>
    </tr>
    <tr>
      <th>Carnitas Soft Tacos</th>
      <td>1011</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa (Mild), [Black Beans, Rice...</td>
      <td>8.99</td>
    </tr>
    <tr>
      <th>Carnitas Crispy Tacos</th>
      <td>1774</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...</td>
      <td>8.99</td>
    </tr>
    <tr>
      <th>Steak Soft Tacos</th>
      <td>1054</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa (Mild), [Cheese, Sour Cream]]</td>
      <td>8.99</td>
    </tr>
    <tr>
      <th>Carnitas Salad</th>
      <td>1500</td>
      <td>1</td>
      <td>[[Fresh Tomato Salsa (Mild), Roasted Chili Cor...</td>
      <td>8.99</td>
    </tr>
    <tr>
      <th>Carnitas Bowl</th>
      <td>1007</td>
      <td>1</td>
      <td>[Fresh Tomato (Mild), [Guacamole, Lettuce, Ric...</td>
      <td>8.99</td>
    </tr>
    <tr>
      <th>Barbacoa Soft Tacos</th>
      <td>1103</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa, [Black Beans, Cheese, Let...</td>
      <td>8.99</td>
    </tr>
    <tr>
      <th>Barbacoa Crispy Tacos</th>
      <td>110</td>
      <td>1</td>
      <td>[Fresh Tomato Salsa, Guacamole]</td>
      <td>8.99</td>
    </tr>
  </tbody>
</table>
</div>




```python
#가격 분포 그래프
item_name_list = price_per_item.index.tolist()
x_pos=np.arange(len(item_name_list))
item_price = price_per_item['item_price'].tolist()

plt.bar(x_pos, item_price, align ='edge', color='green', alpha=0.6)
plt.ylabel('item price($)')
plt.title('Distribution of item price')
plt.show()

#가격 히스토그램
plt.hist(item_price, color='yellowgreen', alpha=0.6)
plt.ylabel('counts')
plt.title('Histogram of item price')
plt.show()
```


    
![png](output_15_0.png)
    



    
![png](output_15_1.png)
    



```python
#가장 비싼 주문에서 몇 개의 아이템이 팔렸나?
chipo.groupby('order_id').sum().sort_values(by='item_price', ascending=False)[:5]
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
      <th>quantity</th>
      <th>item_price</th>
    </tr>
    <tr>
      <th>order_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>926</th>
      <td>23</td>
      <td>205.25</td>
    </tr>
    <tr>
      <th>1443</th>
      <td>35</td>
      <td>160.74</td>
    </tr>
    <tr>
      <th>1483</th>
      <td>14</td>
      <td>139.00</td>
    </tr>
    <tr>
      <th>691</th>
      <td>11</td>
      <td>118.25</td>
    </tr>
    <tr>
      <th>1786</th>
      <td>20</td>
      <td>114.30</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Veggie Salad Bowl은 몇 번 주문되었나?
chipo_salad = chipo[chipo['item_name']=='Veggie Salad Bowl']
#한 주문 내 중복집계된 item_name 제거
chipo_salad = chipo_salad.drop_duplicates(['item_name', 'order_id'])
print(len(chipo_salad))
```

    18
    


```python
#Chicken Bowl 2개 이상 주문한 주문 횟수는?
chipo_chicken = chipo[chipo['item_name']=='Chicken Bowl']
chipo_chicken_ordersum = chipo_chicken.groupby('order_id').sum()['quantity']
chipo_chicken_result = chipo_chicken_ordersum[chipo_chicken_ordersum>=2]

print(len(chipo_chicken_result))
chipo_chicken_result.head()
```

    114
    




    order_id
    1004    2
    1023    2
    1072    2
    1078    2
    1091    2
    Name: quantity, dtype: int64



```python
from bs4 import BeautifulSoup as bs
import requests
import pandas as pd 
```

# Write a python program to scrape first 10 product details which include product name , price , Image URL from
https://www.bewakoof.com/bestseller?sort=popular.


```python
url = 'https://www.bewakoof.com/bestseller?sort=popular%20'

```


```python
page = requests.get(url)
page
```




    <Response [200]>




```python
soup = bs(page.content,'html.parser')
```


```python
print(soup.title.text)
```

    Bestseller
    


```python
 PRODUCT_NAME = []

for i in soup.find_all('div',class_="productNaming bkf-ellipsis"):
    PRODUCT_NAME.append(i.text.strip())
    
```


```python
 PRODUCT_NAME
```




    ["bewakoof x dcMen's Black Adam Graphic Printed T-shirt",
     "Bewakoof®Men's Black Warriors Graphic Printed Oversized T-shirt",
     "bewakoof x house of the dragonMen's Black House Of The Dragon Iconic Graphic Printed T-shirt",
     "Bewakoof®Women's Black Anti Hero Graphic Printed Oversized T-shirt",
     "bewakoof x tom & jerryWomen's Blue Moody Jerry Graphic Printed Oversized T-shirt",
     "Bewakoof®Women's White & Purple Camo Printed Oversized T-shirt",
     "bewakoof x marvelMen's Green Wakanda Forever Graphic Printed Oversized T-shirt",
     "Bewakoof®Men's White Wander Geometry T-shirt",
     "bewakoof x tom & jerryWomen's Green Weirdos Forever Graphic Printed Oversized T-shirt",
     "Bewakoof®Men's Blue Rider Vroom Panda Graphic Printed T-shirt"]




```python
PRICE = []

for i in soup.find_all('div', class_="discountedPriceText clr-p-black false"):
    PRICE.append(i.text.replace('₹','£'))
    
print(PRICE)
```

    ['£499', '£499', '£399', '£499', '£499', '£439', '£499', '£499', '£499', '£499']
    


```python
IMAGE = []

for i in soup.find_all('img'):
    IMAGE.append(i['src'])  # data-src does not exist then i used src
    
IMAGE
```




    ['https://images.bewakoof.com/web/ic-desktop-bwkf-trademark-logo.svg',
     'https://images.bewakoof.com/web/ic-web-head-primary-back.svg',
     'https://images.bewakoof.com/web/ic-web-head-bwk-primary-logo-eyes.svg',
     'https://images.bewakoof.com/web/ic-web-head-search.svg',
     'https://images.bewakoof.com/web/ic-web-head-wishlist.svg',
     'https://images.bewakoof.com/web/ic-web-head-cart.svg',
     'https://images.bewakoof.com/t640/men-s-black-adam-graphic-printed-t-shirt-541266-1709214736-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/men-s-black-warriors-graphic-printed-oversized-t-shirt-519149-1715257507-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/men-s-black-house-of-the-dragon-iconic-graphic-printed-t-shirt-519411-1715257899-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/women-s-black-anti-hero-graphic-printed-oversized-t-shirt-556742-1717060309-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/women-s-blue-moody-jerry-graphic-printed-oversized-t-shirt-585902-1715257595-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/women-aop-oversize-t-shirt-12-580375-1684862463-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/men-s-green-wakanda-forever-graphic-printed-oversized-t-shirt-637169-1721201559-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/men-s-white-wander-geometry-t-shirt-391327-1715257555-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/women-s-green-weirdos-forever-graphic-printed-oversized-t-shirt-592030-1707292567-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/t640/men-s-blue-rider-vroom-panda-graphic-printed-t-shirt-387282-1717060217-1.jpg',
     'https://images.bewakoof.com/web/Wishlist.svg',
     'https://images.bewakoof.com/web/app_android_v1.png',
     'https://images.bewakoof.com/web/android-2x.png',
     'https://images.bewakoof.com/web/app_ios_v1.png',
     'https://images.bewakoof.com/web/apple-2x.png',
     'https://images.bewakoof.com/web/secure-payments-image.png']




```python
PRODUCT_NAME=  PRODUCT_NAME[:10]
PRICE = PRICE[:10]
IMAGE = IMAGE[:10]
```


```python
# print length

print(len( PRODUCT_NAME),len(PRICE),len(IMAGE))
```

    10 10 10
    


```python
df= pd.DataFrame({' PRODUCT_NAME': PRODUCT_NAME,'IMAGE':IMAGE,'PRICE':PRICE})
df

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
      <th>PRODUCT_NAME</th>
      <th>IMAGE</th>
      <th>PRICE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>bewakoof x dcMen's Black Adam Graphic Printed ...</td>
      <td>https://images.bewakoof.com/web/ic-desktop-bwk...</td>
      <td>£499</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bewakoof®Men's Black Warriors Graphic Printed ...</td>
      <td>https://images.bewakoof.com/web/ic-web-head-pr...</td>
      <td>£499</td>
    </tr>
    <tr>
      <th>2</th>
      <td>bewakoof x house of the dragonMen's Black Hous...</td>
      <td>https://images.bewakoof.com/web/ic-web-head-bw...</td>
      <td>£399</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bewakoof®Women's Black Anti Hero Graphic Print...</td>
      <td>https://images.bewakoof.com/web/ic-web-head-se...</td>
      <td>£499</td>
    </tr>
    <tr>
      <th>4</th>
      <td>bewakoof x tom &amp; jerryWomen's Blue Moody Jerry...</td>
      <td>https://images.bewakoof.com/web/ic-web-head-wi...</td>
      <td>£499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Bewakoof®Women's White &amp; Purple Camo Printed O...</td>
      <td>https://images.bewakoof.com/web/ic-web-head-ca...</td>
      <td>£439</td>
    </tr>
    <tr>
      <th>6</th>
      <td>bewakoof x marvelMen's Green Wakanda Forever G...</td>
      <td>https://images.bewakoof.com/t640/men-s-black-a...</td>
      <td>£499</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bewakoof®Men's White Wander Geometry T-shirt</td>
      <td>https://images.bewakoof.com/web/Wishlist.svg</td>
      <td>£499</td>
    </tr>
    <tr>
      <th>8</th>
      <td>bewakoof x tom &amp; jerryWomen's Green Weirdos Fo...</td>
      <td>https://images.bewakoof.com/t640/men-s-black-w...</td>
      <td>£499</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Bewakoof®Men's Blue Rider Vroom Panda Graphic ...</td>
      <td>https://images.bewakoof.com/web/Wishlist.svg</td>
      <td>£499</td>
    </tr>
  </tbody>
</table>
</div>



# Please visit https://www.keaipublishing.com/en/journals/artificial-intelligence-in-agriculture/most-downloadedarticles/ and scrapa) Paper title
 b) date
c) Author


```python
url = 'https://www.keaipublishing.com/en/journals/artificial-intelligence-in-agriculture/most-downloaded-articles/'
```


```python
page = requests.get(url)
page
```




    <Response [200]>




```python
soup = bs(page.content,'html.parser')

```


```python
Paper_title = []
for i in soup.find_all('h2'):
    Paper_title.append(i.text.strip())#
    
Paper_title

```




    ['Implementation of artificial intelligence in agriculture for optimisation of irrigation and application of pesticides and herbicides',
     'Review of agricultural IoT technology',
     'Automation and digitization of agriculture using artificial intelligence and internet of things',
     'A comprehensive review on automation in agriculture using artificial intelligence',
     'Applications of electronic nose (e-nose) and electronic tongue (e-tongue) in food quality-related properties determination: A review',
     'Towards sustainable agriculture: Harnessing AI for global food security',
     'Fruit ripeness classification: A survey',
     'Deep learning based computer vision approaches for smart agricultural applications',
     'A review of imaging techniques for plant disease detection',
     'Transfer Learning for Multi-Crop Leaf Disease Image Classification using Convolutional Neural Network VGG',
     'Comparison of CNN-based deep learning architectures for rice diseases classification',
     'DeepRice: A deep learning and deep feature based classification of Rice leaf disease subtypes',
     'Computer vision in smart agriculture and precision farming: Techniques and applications',
     'Image classification on smart agriculture platforms: Systematic literature review',
     'Using an improved lightweight YOLOv8 model for real-time detection of multi-stage apple fruit in complex orchard environments',
     'How artificial intelligence uses to achieve the agriculture sustainability: Systematic review',
     'LeafSpotNet: A deep learning framework for detecting leaf spot disease in jasmine plants',
     'Plant disease detection using hybrid model based on convolutional autoencoder and convolutional neural network',
     'Cross-comparative review of Machine learning for plant disease detection: apple, cassava, cotton and potato plants',
     'A comprehensive survey on weed and crop classification using machine learning and deep learning',
     'A systematic review of machine learning techniques for cattle identification: Datasets, methods and future directions',
     'Machine learning in nutrient management: A review',
     'Deep convolutional neural network models for weed detection in polyhouse grown bell peppers',
     'A review on computer vision systems in monitoring of poultry: A welfare perspective',
     'Explainable artificial intelligence and interpretable machine learning for agricultural data analysis',
     'Stay Informed',
     'KeAi',
     'All Journals',
     'Publishing guide',
     'Editorial information',
     'Reviewer information',
     'All events']




```python
DATE = []

for i in soup.find_all('p',class_="article-date"):
    DATE.append(i.text.strip())
    
print(DATE)
```

    ['2020', '2022', '2021', 'June 2019', '2020', 'June 2024', 'March 2023', '2022', '2020', '2022', 'September 2023', 'March 2024', 'September 2024', 'September 2024', 'March 2024', 'June 2023', 'June 2024', '2021', 'June 2024', 'September 2024', '2022', 'September 2023', '2022', '2020', '2022']
    


```python
AUTHOR = []

for i in soup.find_all('p',class_="article-authors"):
    AUTHOR.append(i.text)
    
print(AUTHOR)
```

    [' Tanha Talaviya |  Dhara Shah |  Nivedita Patel |  Hiteshri Yagnik |  Manan Shah', ' Jinyuan Xu |  Baoxing Gu |  Guangzhao Tian', ' A. Subeesh |  C.R. Mehta', ' Kirtan Jha |  Aalap Doshi |  Poojan Patel |  Manan Shah', ' Juzhong Tan |  Jie Xu', ' Dhananjay K. Pandey |  Richa Mishra', ' Matteo Rizzo |  Matteo Marcuzzo |  Alessandro Zangari |  Andrea Gasparetto |  Andrea Albarelli', ' V.G. Dhanya |  A. Subeesh |  N.L. Kushwaha |  Dinesh Kumar Vishwakarma |  T. Nagesh Kumar |  G. Ritika |  A.N. Singh', ' Vijai Singh |  Namita Sharma |  Shikha Singh', ' Ananda S. Paymode |  Vandana B. Malode', ' Md Taimur Ahad |  Yan Li |  Bo Song |  Touhid Bhuiyan', ' P. Isaac Ritharson |  Kumudha Raimond |  X. Anitha Mary |  Jennifer Eunice Robert |  Andrew J', ' Sumaira Ghazal |  Arslan Munir |  Waqar S. Qureshi', ' Juan Felipe Restrepo-Arias |  John W. Branch-Bedoya |  Gabriel Awad', ' Baoling Ma |  Zhixin Hua |  Yuchen Wen |  Hongxing Deng |  Yongjie Zhao |  Liuru Pu |  Huaibo Song', ' Vilani Sachithra |  L.D.C.S. Subhashini', ' Shwetha V |  Arnav Bhagwat |  Vijaya Laxmi', ' Punam Bedi |  Pushkar Gole', ' James Daniel Omaye |  Emeka Ogbuju |  Grace Ataguba |  Oluwayemisi Jaiyeoba |  Joseph Aneke |  Francisca Oladipo', ' Faisal Dharma Adhinata |   Wahyono |  Raden Sumiharto', ' Md Ekramul Hossain |  Muhammad Ashad Kabir |  Lihong Zheng |  Dave L. Swain |  Shawn McGrath |  Jonathan Medway', ' Oumnia Ennaji |  Leonardus Vergütz |  Achraf El Allali', ' A. Subeesh |  S. Bhole |  K. Singh |  N.S. Chandel |  Y.A. Rajwade |  K.V.R. Rao |  S.P. Kumar |  D. Jat', ' Cedric Okinda |  Innocent Nyalala |  Tchalla Korohou |  Celestine Okinda |  Jintao Wang |  Tracy Achieng |  Patrick Wamalwa |  Tai Mang |  Mingxia Shen', ' Masahiro Ryo']
    


```python
print(len(Paper_title),len(DATE),len(AUTHOR))
```

    32 25 25
    


```python
PaperTitle = Paper_Title[:25]
Date = DATE[:25]
Author = AUTHOR[:25]
```


```python
df = pd.DataFrame({'Date':DATE,'PaperTitle':Paper_Title,'Author':AUTHOR})
df
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
      <th>Date</th>
      <th>PaperTitle</th>
      <th>Author</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020</td>
      <td>Implementation of artificial intelligence in a...</td>
      <td>Tanha Talaviya |  Dhara Shah |  Nivedita Pate...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022</td>
      <td>Review of agricultural IoT technology</td>
      <td>Jinyuan Xu |  Baoxing Gu |  Guangzhao Tian</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2021</td>
      <td>Automation and digitization of agriculture usi...</td>
      <td>A. Subeesh |  C.R. Mehta</td>
    </tr>
    <tr>
      <th>3</th>
      <td>June 2019</td>
      <td>A comprehensive review on automation in agricu...</td>
      <td>Kirtan Jha |  Aalap Doshi |  Poojan Patel |  ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020</td>
      <td>Applications of electronic nose (e-nose) and e...</td>
      <td>Juzhong Tan |  Jie Xu</td>
    </tr>
    <tr>
      <th>5</th>
      <td>June 2024</td>
      <td>Towards sustainable agriculture: Harnessing AI...</td>
      <td>Dhananjay K. Pandey |  Richa Mishra</td>
    </tr>
    <tr>
      <th>6</th>
      <td>March 2023</td>
      <td>Fruit ripeness classification: A survey</td>
      <td>Matteo Rizzo |  Matteo Marcuzzo |  Alessandro...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2022</td>
      <td>Deep learning based computer vision approaches...</td>
      <td>V.G. Dhanya |  A. Subeesh |  N.L. Kushwaha | ...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2020</td>
      <td>A review of imaging techniques for plant disea...</td>
      <td>Vijai Singh |  Namita Sharma |  Shikha Singh</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2022</td>
      <td>Transfer Learning for Multi-Crop Leaf Disease ...</td>
      <td>Ananda S. Paymode |  Vandana B. Malode</td>
    </tr>
    <tr>
      <th>10</th>
      <td>September 2023</td>
      <td>Comparison of CNN-based deep learning architec...</td>
      <td>Md Taimur Ahad |  Yan Li |  Bo Song |  Touhid...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>March 2024</td>
      <td>DeepRice: A deep learning and deep feature bas...</td>
      <td>P. Isaac Ritharson |  Kumudha Raimond |  X. A...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>September 2024</td>
      <td>Computer vision in smart agriculture and preci...</td>
      <td>Sumaira Ghazal |  Arslan Munir |  Waqar S. Qu...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>September 2024</td>
      <td>Image classification on smart agriculture plat...</td>
      <td>Juan Felipe Restrepo-Arias |  John W. Branch-...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>March 2024</td>
      <td>Using an improved lightweight YOLOv8 model for...</td>
      <td>Baoling Ma |  Zhixin Hua |  Yuchen Wen |  Hon...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>June 2023</td>
      <td>How artificial intelligence uses to achieve th...</td>
      <td>Vilani Sachithra |  L.D.C.S. Subhashini</td>
    </tr>
    <tr>
      <th>16</th>
      <td>June 2024</td>
      <td>LeafSpotNet: A deep learning framework for det...</td>
      <td>Shwetha V |  Arnav Bhagwat |  Vijaya Laxmi</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2021</td>
      <td>Plant disease detection using hybrid model bas...</td>
      <td>Punam Bedi |  Pushkar Gole</td>
    </tr>
    <tr>
      <th>18</th>
      <td>June 2024</td>
      <td>Cross-comparative review of Machine learning f...</td>
      <td>James Daniel Omaye |  Emeka Ogbuju |  Grace A...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>September 2024</td>
      <td>A comprehensive survey on weed and crop classi...</td>
      <td>Faisal Dharma Adhinata |   Wahyono |  Raden S...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2022</td>
      <td>A systematic review of machine learning techni...</td>
      <td>Md Ekramul Hossain |  Muhammad Ashad Kabir | ...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>September 2023</td>
      <td>Machine learning in nutrient management: A review</td>
      <td>Oumnia Ennaji |  Leonardus Vergütz |  Achraf ...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2022</td>
      <td>Deep convolutional neural network models for w...</td>
      <td>A. Subeesh |  S. Bhole |  K. Singh |  N.S. Ch...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2020</td>
      <td>A review on computer vision systems in monitor...</td>
      <td>Cedric Okinda |  Innocent Nyalala |  Tchalla ...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2022</td>
      <td>Explainable artificial intelligence and interp...</td>
      <td>Masahiro Ryo</td>
    </tr>
  </tbody>
</table>
</div>




```python
#df.to_csv('C:\\Users\\USER\\Desktop\\artificialintelligence.csv',index=False)
```


```python

```

```python
import pandas as pd
import numpy as np
import requests
from bs4 import BeautifulSoup
import re
import seaborn as sns
import matplotlib.pyplot as plt

pd.options.display.max_rows = 500

r = requests.get('https://www.the-numbers.com/box-office-records/worldwide/all-movies/cumulative/sequel')
soup = BeautifulSoup(r.content)
col = soup.find('table')
the = col.tbody.text
split = the.split("\n\n")
```




```python
array = []
for i in range(len(split)):
    if split[i] != '':
        array.append(split[i].split("\n"))
        
for i in range(len(array)):
    if array[i][0] == '':
        array[i].remove('')
```

# All Time Worldwide Sequel Box Office


```python
table = pd.DataFrame(data = array, columns = ["Rank","Released","Movie","Worldwide Box Office","Domestic Box Office","International Box Office"])
n = table.sort_values(by = 'Movie')
updated_table = n.drop(index = [46,98,95,71,62,85,27,5,47,91,10,61,81,92,80,83,68,96,17,44,74,11,97,69,66,52,75])
updated_table.Movie[88] = 'Fast and Furious 5'
updated_table.Movie[4] = 'Fast and Furious 7'
updated_table
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
      <th>Rank</th>
      <th>Released</th>
      <th>Movie</th>
      <th>Worldwide Box Office</th>
      <th>Domestic Box Office</th>
      <th>International Box Office</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>89</th>
      <td>89</td>
      <td>2018</td>
      <td>Ant-Man and the Wasp</td>
      <td>$623,144,660</td>
      <td>$216,648,740</td>
      <td>$406,495,920</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>$1,395,316,979</td>
      <td>$459,005,868</td>
      <td>$936,311,111</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2019</td>
      <td>Avengers: Endgame</td>
      <td>$2,797,800,564</td>
      <td>$858,373,000</td>
      <td>$1,939,427,564</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2018</td>
      <td>Avengers: Infinity War</td>
      <td>$2,044,540,523</td>
      <td>$678,815,482</td>
      <td>$1,365,725,041</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>2016</td>
      <td>Captain America: Civil War</td>
      <td>$1,151,918,521</td>
      <td>$408,084,349</td>
      <td>$743,834,172</td>
    </tr>
    <tr>
      <th>70</th>
      <td>71</td>
      <td>2014</td>
      <td>Captain America: The Winter Soldier</td>
      <td>$714,401,889</td>
      <td>$259,746,958</td>
      <td>$454,654,931</td>
    </tr>
    <tr>
      <th>30</th>
      <td>31</td>
      <td>2013</td>
      <td>Despicable Me 2</td>
      <td>$975,216,835</td>
      <td>$368,065,385</td>
      <td>$607,151,450</td>
    </tr>
    <tr>
      <th>25</th>
      <td>26</td>
      <td>2017</td>
      <td>Despicable Me 3</td>
      <td>$1,032,596,894</td>
      <td>$264,624,300</td>
      <td>$767,972,594</td>
    </tr>
    <tr>
      <th>88</th>
      <td>88</td>
      <td>2011</td>
      <td>Fast and Furious 5</td>
      <td>$630,163,454</td>
      <td>$210,031,325</td>
      <td>$420,132,129</td>
    </tr>
    <tr>
      <th>59</th>
      <td>60</td>
      <td>2013</td>
      <td>Fast and Furious 6</td>
      <td>$789,300,444</td>
      <td>$238,679,850</td>
      <td>$550,620,594</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2015</td>
      <td>Fast and Furious 7</td>
      <td>$1,517,179,709</td>
      <td>$353,007,020</td>
      <td>$1,164,172,689</td>
    </tr>
    <tr>
      <th>45</th>
      <td>46</td>
      <td>2002</td>
      <td>Harry Potter and the Chamber of Secrets</td>
      <td>$876,508,805</td>
      <td>$262,233,381</td>
      <td>$614,275,424</td>
    </tr>
    <tr>
      <th>34</th>
      <td>35</td>
      <td>2010</td>
      <td>Harry Potter and the Deathly Hallows: Part I</td>
      <td>$955,371,891</td>
      <td>$296,131,568</td>
      <td>$659,240,323</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2011</td>
      <td>Harry Potter and the Deathly Hallows: Part II</td>
      <td>$1,334,392,544</td>
      <td>$381,193,157</td>
      <td>$953,199,387</td>
    </tr>
    <tr>
      <th>41</th>
      <td>42</td>
      <td>2005</td>
      <td>Harry Potter and the Goblet of Fire</td>
      <td>$891,320,084</td>
      <td>$290,201,752</td>
      <td>$601,118,332</td>
    </tr>
    <tr>
      <th>38</th>
      <td>39</td>
      <td>2009</td>
      <td>Harry Potter and the Half-Blood Prince</td>
      <td>$930,673,167</td>
      <td>$302,089,278</td>
      <td>$628,583,889</td>
    </tr>
    <tr>
      <th>36</th>
      <td>37</td>
      <td>2007</td>
      <td>Harry Potter and the Order of the Phoenix</td>
      <td>$940,743,940</td>
      <td>$292,137,260</td>
      <td>$648,606,680</td>
    </tr>
    <tr>
      <th>58</th>
      <td>59</td>
      <td>2004</td>
      <td>Harry Potter and the Prisoner of Azkaban</td>
      <td>$789,961,033</td>
      <td>$249,757,726</td>
      <td>$540,203,307</td>
    </tr>
    <tr>
      <th>43</th>
      <td>44</td>
      <td>2012</td>
      <td>Ice Age: Continental Drift</td>
      <td>$879,765,137</td>
      <td>$161,321,843</td>
      <td>$718,443,294</td>
    </tr>
    <tr>
      <th>42</th>
      <td>43</td>
      <td>2009</td>
      <td>Ice Age: Dawn of the Dinosaurs</td>
      <td>$886,686,817</td>
      <td>$196,573,705</td>
      <td>$690,113,112</td>
    </tr>
    <tr>
      <th>84</th>
      <td>84</td>
      <td>2006</td>
      <td>Ice Age: The Meltdown</td>
      <td>$651,899,282</td>
      <td>$195,330,621</td>
      <td>$456,568,661</td>
    </tr>
    <tr>
      <th>90</th>
      <td>90</td>
      <td>2010</td>
      <td>Iron Man 2</td>
      <td>$621,156,389</td>
      <td>$312,433,331</td>
      <td>$308,723,058</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>2013</td>
      <td>Iron Man 3</td>
      <td>$1,215,392,272</td>
      <td>$408,992,272</td>
      <td>$806,400,000</td>
    </tr>
    <tr>
      <th>55</th>
      <td>56</td>
      <td>2019</td>
      <td>Jumanji: The Next Level</td>
      <td>$800,128,637</td>
      <td>$316,831,246</td>
      <td>$483,297,391</td>
    </tr>
    <tr>
      <th>31</th>
      <td>32</td>
      <td>2017</td>
      <td>Jumanji: Welcome to the Jungle</td>
      <td>$961,540,207</td>
      <td>$404,508,916</td>
      <td>$557,031,291</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2015</td>
      <td>Jurassic World</td>
      <td>$1,669,979,967</td>
      <td>$652,306,625</td>
      <td>$1,017,673,342</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>2018</td>
      <td>Jurassic World: Fallen Kingdom</td>
      <td>$1,308,334,005</td>
      <td>$417,719,760</td>
      <td>$890,614,245</td>
    </tr>
    <tr>
      <th>67</th>
      <td>68</td>
      <td>2012</td>
      <td>Madagascar 3: Europe's Most Wanted</td>
      <td>$746,921,271</td>
      <td>$216,391,482</td>
      <td>$530,529,789</td>
    </tr>
    <tr>
      <th>94</th>
      <td>94</td>
      <td>2008</td>
      <td>Madagascar: Escape 2 Africa</td>
      <td>$599,680,774</td>
      <td>$180,174,880</td>
      <td>$419,505,894</td>
    </tr>
    <tr>
      <th>99</th>
      <td>99</td>
      <td>2000</td>
      <td>Mission: Impossible 2</td>
      <td>$549,588,516</td>
      <td>$215,409,889</td>
      <td>$334,178,627</td>
    </tr>
    <tr>
      <th>60</th>
      <td>61</td>
      <td>2018</td>
      <td>Mission: ImpossibleâFallout</td>
      <td>$787,176,729</td>
      <td>$220,159,104</td>
      <td>$567,017,625</td>
    </tr>
    <tr>
      <th>76</th>
      <td>76</td>
      <td>2011</td>
      <td>Mission: ImpossibleâGhost Protocol</td>
      <td>$694,713,230</td>
      <td>$209,397,903</td>
      <td>$485,315,327</td>
    </tr>
    <tr>
      <th>78</th>
      <td>78</td>
      <td>2015</td>
      <td>Mission: ImpossibleâRogue Nation</td>
      <td>$688,858,992</td>
      <td>$195,042,377</td>
      <td>$493,816,615</td>
    </tr>
    <tr>
      <th>32</th>
      <td>33</td>
      <td>2007</td>
      <td>Pirates of the Caribbean: At Worldâs End</td>
      <td>$960,996,492</td>
      <td>$309,420,425</td>
      <td>$651,576,067</td>
    </tr>
    <tr>
      <th>23</th>
      <td>24</td>
      <td>2006</td>
      <td>Pirates of the Caribbean: Dead Manâs Chest</td>
      <td>$1,066,179,725</td>
      <td>$423,315,812</td>
      <td>$642,863,913</td>
    </tr>
    <tr>
      <th>56</th>
      <td>57</td>
      <td>2017</td>
      <td>Pirates of the Caribbean: Dead Men Tell No Tales</td>
      <td>$794,861,794</td>
      <td>$172,558,876</td>
      <td>$622,302,918</td>
    </tr>
    <tr>
      <th>24</th>
      <td>25</td>
      <td>2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>$1,045,713,802</td>
      <td>$241,071,802</td>
      <td>$804,642,000</td>
    </tr>
    <tr>
      <th>37</th>
      <td>38</td>
      <td>2004</td>
      <td>Shrek 2</td>
      <td>$935,253,978</td>
      <td>$441,226,247</td>
      <td>$494,027,731</td>
    </tr>
    <tr>
      <th>65</th>
      <td>66</td>
      <td>2010</td>
      <td>Shrek Forever After</td>
      <td>$756,244,673</td>
      <td>$238,736,787</td>
      <td>$517,507,886</td>
    </tr>
    <tr>
      <th>54</th>
      <td>55</td>
      <td>2007</td>
      <td>Shrek the Third</td>
      <td>$807,330,936</td>
      <td>$322,719,944</td>
      <td>$484,610,992</td>
    </tr>
    <tr>
      <th>57</th>
      <td>58</td>
      <td>2004</td>
      <td>Spider-Man 2</td>
      <td>$794,697,557</td>
      <td>$373,524,485</td>
      <td>$421,173,072</td>
    </tr>
    <tr>
      <th>40</th>
      <td>41</td>
      <td>2007</td>
      <td>Spider-Man 3</td>
      <td>$894,860,230</td>
      <td>$336,530,303</td>
      <td>$558,329,927</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>2019</td>
      <td>Spider-Man: Far From Home</td>
      <td>$1,131,219,645</td>
      <td>$390,532,085</td>
      <td>$740,687,560</td>
    </tr>
    <tr>
      <th>26</th>
      <td>27</td>
      <td>1999</td>
      <td>Star Wars Ep. I: The Phantom Menace</td>
      <td>$1,027,044,677</td>
      <td>$474,544,677</td>
      <td>$552,500,000</td>
    </tr>
    <tr>
      <th>82</th>
      <td>82</td>
      <td>2002</td>
      <td>Star Wars Ep. II: Attack of the Clones</td>
      <td>$656,695,615</td>
      <td>$310,676,740</td>
      <td>$346,018,875</td>
    </tr>
    <tr>
      <th>50</th>
      <td>51</td>
      <td>2005</td>
      <td>Star Wars Ep. III: Revenge of the Sith</td>
      <td>$848,998,877</td>
      <td>$380,270,577</td>
      <td>$468,728,300</td>
    </tr>
    <tr>
      <th>100</th>
      <td>100</td>
      <td>1980</td>
      <td>Star Wars Ep. V: The Empire Strikes Back</td>
      <td>$549,001,242</td>
      <td>$291,738,960</td>
      <td>$257,262,282</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2015</td>
      <td>Star Wars Ep. VII: The Force Awakens</td>
      <td>$2,065,369,276</td>
      <td>$936,662,225</td>
      <td>$1,128,707,051</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>2017</td>
      <td>Star Wars Ep. VIII: The Last Jedi</td>
      <td>$1,332,539,889</td>
      <td>$620,181,382</td>
      <td>$712,358,507</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22</td>
      <td>2019</td>
      <td>Star Wars: The Rise of Skywalker</td>
      <td>$1,072,944,222</td>
      <td>$515,202,542</td>
      <td>$557,741,680</td>
    </tr>
    <tr>
      <th>64</th>
      <td>65</td>
      <td>2012</td>
      <td>The Amazing Spider-Man</td>
      <td>$757,890,267</td>
      <td>$262,030,663</td>
      <td>$495,859,604</td>
    </tr>
    <tr>
      <th>72</th>
      <td>73</td>
      <td>2014</td>
      <td>The Amazing Spider-Man 2</td>
      <td>$708,996,336</td>
      <td>$202,853,933</td>
      <td>$506,142,403</td>
    </tr>
    <tr>
      <th>29</th>
      <td>30</td>
      <td>2008</td>
      <td>The Dark Knight</td>
      <td>$999,046,281</td>
      <td>$533,720,947</td>
      <td>$465,325,334</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>2012</td>
      <td>The Dark Knight Rises</td>
      <td>$1,082,228,107</td>
      <td>$448,139,099</td>
      <td>$634,089,008</td>
    </tr>
    <tr>
      <th>28</th>
      <td>29</td>
      <td>2012</td>
      <td>The Hobbit: An Unexpected Journey</td>
      <td>$1,017,003,568</td>
      <td>$303,003,568</td>
      <td>$714,000,000</td>
    </tr>
    <tr>
      <th>35</th>
      <td>36</td>
      <td>2014</td>
      <td>The Hobbit: The Battle of the Five Armies</td>
      <td>$943,328,905</td>
      <td>$255,119,788</td>
      <td>$688,209,117</td>
    </tr>
    <tr>
      <th>33</th>
      <td>34</td>
      <td>2013</td>
      <td>The Hobbit: The Desolation of Smaug</td>
      <td>$960,238,087</td>
      <td>$258,241,522</td>
      <td>$701,996,565</td>
    </tr>
    <tr>
      <th>48</th>
      <td>49</td>
      <td>2013</td>
      <td>The Hunger Games: Catching Fire</td>
      <td>$864,868,047</td>
      <td>$424,668,047</td>
      <td>$440,200,000</td>
    </tr>
    <tr>
      <th>63</th>
      <td>64</td>
      <td>2014</td>
      <td>The Hunger Games: Mockingjay - Part 1</td>
      <td>$766,575,131</td>
      <td>$337,135,885</td>
      <td>$429,439,246</td>
    </tr>
    <tr>
      <th>86</th>
      <td>86</td>
      <td>2015</td>
      <td>The Hunger Games: Mockingjay - Part 2</td>
      <td>$648,986,787</td>
      <td>$281,723,902</td>
      <td>$367,262,885</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>2003</td>
      <td>The Lord of the Rings: The Return of the King</td>
      <td>$1,120,224,046</td>
      <td>$377,845,905</td>
      <td>$742,378,141</td>
    </tr>
    <tr>
      <th>39</th>
      <td>40</td>
      <td>2002</td>
      <td>The Lord of the Rings: The Two Towers</td>
      <td>$919,148,764</td>
      <td>$342,548,984</td>
      <td>$576,599,780</td>
    </tr>
    <tr>
      <th>77</th>
      <td>77</td>
      <td>2011</td>
      <td>The Twilight Saga: Breaking Dawn, Part 1</td>
      <td>$689,420,051</td>
      <td>$281,287,133</td>
      <td>$408,132,918</td>
    </tr>
    <tr>
      <th>53</th>
      <td>54</td>
      <td>2012</td>
      <td>The Twilight Saga: Breaking Dawn, Part 2</td>
      <td>$829,724,737</td>
      <td>$292,324,737</td>
      <td>$537,400,000</td>
    </tr>
    <tr>
      <th>73</th>
      <td>74</td>
      <td>2010</td>
      <td>The Twilight Saga: Eclipse</td>
      <td>$706,102,828</td>
      <td>$300,531,751</td>
      <td>$405,571,077</td>
    </tr>
    <tr>
      <th>79</th>
      <td>79</td>
      <td>2009</td>
      <td>The Twilight Saga: New Moon</td>
      <td>$687,557,727</td>
      <td>$296,623,634</td>
      <td>$390,934,093</td>
    </tr>
    <tr>
      <th>49</th>
      <td>50</td>
      <td>2017</td>
      <td>Thor: Ragnarok</td>
      <td>$850,482,778</td>
      <td>$315,058,289</td>
      <td>$535,424,489</td>
    </tr>
    <tr>
      <th>87</th>
      <td>87</td>
      <td>2013</td>
      <td>Thor: The Dark World</td>
      <td>$644,602,516</td>
      <td>$206,362,140</td>
      <td>$438,240,376</td>
    </tr>
    <tr>
      <th>22</th>
      <td>23</td>
      <td>2010</td>
      <td>Toy Story 3</td>
      <td>$1,068,879,522</td>
      <td>$415,004,880</td>
      <td>$653,874,642</td>
    </tr>
    <tr>
      <th>20</th>
      <td>21</td>
      <td>2019</td>
      <td>Toy Story 4</td>
      <td>$1,073,080,329</td>
      <td>$434,038,008</td>
      <td>$639,042,321</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>2014</td>
      <td>Transformers: Age of Extinction</td>
      <td>$1,104,054,072</td>
      <td>$245,439,076</td>
      <td>$858,614,996</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>2011</td>
      <td>Transformers: Dark of the Moon</td>
      <td>$1,123,794,079</td>
      <td>$352,390,543</td>
      <td>$771,403,536</td>
    </tr>
    <tr>
      <th>51</th>
      <td>52</td>
      <td>2009</td>
      <td>Transformers: Revenge of the Fallen</td>
      <td>$836,519,699</td>
      <td>$402,111,870</td>
      <td>$434,407,829</td>
    </tr>
    <tr>
      <th>93</th>
      <td>93</td>
      <td>2017</td>
      <td>Transformers: The Last Knight</td>
      <td>$602,893,340</td>
      <td>$130,168,683</td>
      <td>$472,724,657</td>
    </tr>
  </tbody>
</table>
</div>




```python
# all the sequels in this table
Sequels = ['Avengers','Captain America','Despicable Me','Fast and Furious','Harry Potter','Ice Age','Iron Man','Jumanji','Jurassic World','Madagascar','Mission: impossible','Shrek','Spider-Man','Star Wars','The Amazing Spider-man','Dark Knight','The Hobbit','The Hunger Games','The Lord of the Rings','The Twilight Saga','Thor','Toy Story','Transformers']
```


```python

#this is calculating the differenc between year and in boxoffice amount of the different sequels
year_diff = []
amount_diff = []
each_movie_percent = []
for i in Sequels:
    i = "Star Wars"
    each_movie_table = updated_table[updated_table['Movie'].str.contains(i, regex=False, case=False, na=False)]
    each_movie_table = each_movie_table.sort_values(by = "Released")
    
    each_movie = each_movie_table.Released
    each_movie_money =  each_movie_table['Worldwide Box Office']
    #removing the $ and the , so that i can change into an int
    
    each_movie_money = each_movie_money.str.replace(r'$', '')
    each_movie_money = each_movie_money.str.replace(r',','')
    int (each_movie_money)
    size = len(each_movie_table)
    #print(int(np.array(each_movie)[size-1]))
    #print(int(np.array(each_movie)[size-size]))
    
    year_diff.append(abs(int(np.array(each_movie)[size-1]) - int(np.array(each_movie)[size-size])))
    amount_diff.append(abs(int(np.array(each_movie_money)[size-1]) - int(np.array(each_movie_money)[size-size])))
    each_movie_percent.append(round((abs(int(np.array(each_movie_money)[size-1]) - int(np.array(each_movie_money)[size-size]))/int(np.array(each_movie_money)[size-1])),3)*100
)
```

    <ipython-input-5-b41c72394b20>:14: FutureWarning: The default value of regex will change from True to False in a future version. In addition, single character regular expressions will*not* be treated as literal strings when regex=True.
      each_movie_money = each_movie_money.str.replace(r'$', '')



    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-5-b41c72394b20> in <module>
         14     each_movie_money = each_movie_money.str.replace(r'$', '')
         15     each_movie_money = each_movie_money.str.replace(r',','')
    ---> 16     int (each_movie_money)
         17     size = len(each_movie_table)
         18     #print(int(np.array(each_movie)[size-1]))


    /opt/conda/lib/python3.8/site-packages/pandas/core/series.py in wrapper(self)
        137         if len(self) == 1:
        138             return converter(self.iloc[0])
    --> 139         raise TypeError(f"cannot convert the series to {converter}")
        140 
        141     wrapper.__name__ = f"__{converter.__name__}__"


    TypeError: cannot convert the series to <class 'int'>



```python
#putting the new values into a table
Seq_diff = pd.DataFrame(data = [], columns = ["Movie", "Next/last Sequel..Year Diff","Diff in sequence amount","Perc"])
Seq_diff["Movie"] = Sequels
Seq_diff["Next/last Sequel..Year Diff"] = year_diff
Seq_diff["Diff in sequence amount"] = amount_diff
Seq_diff["Perc"] = each_movie_percent
Seq_diff
```


```python
#separating the table by early sequence

early_sequels = Seq_diff[Seq_diff["Next/last Sequel..Year Diff"] <= 7 ]
#early_sequels.sort_values(by = "Next/last Sequel..Year Diff")
early_sequels = early_sequels.sort_values(by = "Diff in sequence amount")
early_sequels
```


```python
#Separating by late sequel
late_sequels = Seq_diff[Seq_diff["Next/last Sequel..Year Diff"] > 7 ]
late_sequels = late_sequels.sort_values(by = "Diff in sequence amount")
late_sequels
```


```python

```


```python
c = sns.scatterplot(data=early_sequels, x="Next/last Sequel..Year Diff", y="Perc",hue = "Movie")

plt.title('Worldwide Early Sequels')
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)

plt.show
```


```python
sns.scatterplot(data=late_sequels, x="Next/last Sequel..Year Diff", y="Perc",hue = "Movie")
plt.title('Worldwide Late Sequels')
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
plt.show
```


```python
Seq_diff
```


```python
sns.scatterplot(data=Seq_diff, x="Next/last Sequel..Year Diff", y="Perc",hue = "Movie")
plt.title('Worldwide Sequels')
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
plt.show
```


```python

```


```python

```

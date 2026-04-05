# 第9章のソースコード (修正・データの更新済）


#### p266 リスト 9.7 シーザー暗号解読プログラム
```python:シーザー暗号解読プログラム
import codecs
#### 暗号文:「Naq Lr Funyy Xabj gur Gehgu naq gur Gehgu 」Funyy Znxr Lbh Serr」
problem = "Naq Lr Funyy Xabj gur Gehgu naq gur Gehgu Funyy Znxr Lbh Serr"
text = codecs.decode(problem, 'rot_13')
print(text)
```
#### p270 リスト 9.12 Cartopyの世界地図表示テスト
```python:catopytest
!pip install cartopy #　はじめてcartopyをインポートする場合はこちらを加えてください
import cartopy.crs as ccrs
import matplotlib.pyplot as plt

fig = plt.figure(figsize=(12, 8))
ax = plt.axes(projection=ccrs.PlateCarree())
ax.coastlines()

plt.show()
```
#### p271 リスト 9.13 ひまわり9号の衛星の位置を表示するプログラム
　　（ひまわり９号のTLEを更新してあります）
```python:Himawari9A
#### ライブラリー導入
!pip install pyephem 
import ephem
import datetime
import numpy as np
from math import degrees as deg

#### TLE
himawari9="""HIMAWARI-9              
1 41836U 16064A   26095.53614311 -.00000273  00000+0  00000+0 0  9996
2 41836   0.0494 107.0589 0001267 293.0070 127.5527  1.00270979 34481"""

tle0, tle1, tle2 = himawari9.split("\n")
satellite = ephem.readtle(tle0, tle1, tle2)

#### 観測地点の設定
tokyo_station = ephem.Observer()
tokyo_station.lat = '35.6846'
tokyo_station.lon = '139.7106'
tokyo_station.elevation = 3
tokyo_station.date = datetime.datetime.utcnow() 

#### 観測地点の表示
print('観測地点の名前:', '東京駅')
print('観測地点の緯度:', tokyo_station.lat) 
print('観測地点の経度:', tokyo_station.lon) 
print('観測地点の高度:', tokyo_station.elevation,'m') 

#### 衛星の表示
satellite.compute(datetime.datetime.utcnow())
print('衛星の名前:', tle0)
print('衛星の緯度:', deg(satellite.sublat)) 
print('衛星の経度:', deg(satellite.sublong)) 
print('衛星の高度:', satellite.elevation,'m') 

satellite.compute(tokyo_station)
print('観測地点から見た衛星の仰角:', deg(satellite.alt))
print('観測地点から見た衛星の方位:', deg(satellite.az))

#### 衛星が可視範囲内に現れる時間と方位
rise_t, az_rise, max_t, alt_max, set_t, az_set = tokyo_station.next_pass(satellite)

print('衛星が地平線の上に昇る時刻:', ephem.localtime(rise_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_rise)))
print('衛星が最大仰角になる時刻:', ephem.localtime(max_t), 'そのときの最大仰角: {0:.1f}'.format(np.rad2deg(alt_max)))
print('衛星が地平線の下に沈む時刻:', ephem.localtime(set_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_set)))
```
#### p275 リスト 9.15 ひまわり9号の航跡を表示するプログラム
　　（ひまわり９号のTLEを更新してあります）
```python:Himawari9B
### ライブラリー導入
!pip install pyephem
!pip install matplotlib
!pip install cartopy
import ephem
import datetime
import numpy as np
import matplotlib.pyplot as plt
from math import degrees as deg

####TLE取得および分割
himawari9="""HIMAWARI-9             
1 41836U 16064A   24218.86785269 -.00000282  00000+0  00000+0 0  9998
2 41836   0.0411 225.3017 0000837 296.4887 246.2739  1.00273005 28384"""

tle0, tle1, tle2 = himawari9.split("\n")
satellite = ephem.readtle(tle0, tle1, tle2)

#### 航跡を表示するプログラム
import cartopy.crs as ccrs
from datetime import datetime, timedelta

#### TLEからエポックを計算
tle1split = tle1.split()
epochraw = float(tle1split[3]) / 1000
epochstr = str(epochraw)
epochlist = epochstr.split('.')
year = int(epochlist[0]) + 2000
doy = float(epochlist[1]) / 100000000

dt0 = datetime(year, 1, 1) + timedelta(days=doy)
time_list = [(dt0 + timedelta(hours=i/60)) for i in range(0,60*12)]

#### エポックの表示
print('西暦年:', year)
print('エポック:', doy)

#### 世界地図描画
fig = plt.figure(figsize=(12, 8))
ax = plt.axes(projection=ccrs.PlateCarree())
ax.coastlines()
ax.set_title("Satellite Trak")
ax.set_global()

#### 衛星の航跡をプロット
for dt in time_list:
    dot = dt.strftime("%Y/%m/%d %H:%M:%S")
    satellite.compute(f'{dot}')
    latitude = satellite.sublat / ephem.degree
    longitude = satellite.sublong / ephem.degree
    plt.plot(longitude, latitude,
         color='blue', marker='.',
         transform=ccrs.Geodetic(),
         )

#### 表示
print('衛星の航跡:') 
plt.show()       
```
#### p277 リスト 9.16 NOAA15号の位置を計算し航跡を表示するプログラム
  (NOAA15運用終了にともない、現在エラーがでます、下記の修正版を使用してください。）
```python:NOAA15A
### ライブラリー導入
!pip install pyephem 
!pip install matplotlib
!pip install cartopy
import ephem
import datetime
import numpy as np
import matplotlib.pyplot as plt
from math import degrees as deg

####TLE取得および分割
noaa15="""NOAA 15                 
1 25338U 98030A   24219.17306584  .00000415  00000+0  18954-3 0  9992
2 25338  98.5670 245.2526 0010496 172.1414 187.9932 14.26648677364568"""

tle0, tle1, tle2 = noaa15.split("\n")
satellite = ephem.readtle(tle0, tle1, tle2)

#### 観測地点の表示
print('観測地点の名前:', '東京駅')
print('観測地点の緯度:', tokyo_station.lat) 
print('観測地点の経度:', tokyo_station.lon) 
print('観測地点の高度:', tokyo_station.elevation,'m') 

#### Epochの表示
print('西暦年:', year)
print('エポック:', doy)

#### 衛星の表示
satellite.compute(datetime.datetime.now(datetime.UTC))
print('衛星の名前:', tle0)
print('衛星の緯度:', deg(satellite.sublat)) 
print('衛星の経度:', deg(satellite.sublong)) 
print('衛星の高度:', satellite.elevation,'m') 

satellite.compute(tokyo_station)
print('観測地点から見た衛星の仰角:', deg(satellite.alt))
print('観測地点から見た衛星の方位:', deg(satellite.az))

#### 衛星が可視範囲内に現れる時間と方位
rise_t, az_rise, max_t, alt_max, set_t, az_set = tokyo_station.next_pass(satellite)

print('衛星が地平線の上に昇る時刻:', ephem.localtime(rise_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_rise)))
print('衛星が最大仰角になる時刻:', ephem.localtime(max_t), 'そのときの最大仰角: {0:.1f}'.format(np.rad2deg(alt_max)))
print('衛星が地平線の下に沈む時刻:', ephem.localtime(set_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_set)))

#### 航跡を表示するプログラム
import cartopy.crs as ccrs
from datetime import datetime, timedelta

#### TLEからエポックを計算
tle1split = tle1.split()
epochraw = float(tle1split[3]) / 1000
epochstr = str(epochraw)
epochlist = epochstr.split('.')
year = int(epochlist[0]) + 2000
doy = float(epochlist[1]) / 100000000

dt0 = datetime(year, 1, 1) + timedelta(days=doy)
time_list = [(dt0 + timedelta(hours=i/60)) for i in range(0,60*12)]

#### 世界地図描画
fig = plt.figure(figsize=(12, 8))
ax = plt.axes(projection=ccrs.PlateCarree())
ax.coastlines()
ax.set_title("Satellite Trak")
ax.set_global()

#### 衛星の航跡をプロット
for dt in time_list:
    dot = dt.strftime("%Y/%m/%d %H:%M:%S")
    satellite.compute(f'{dot}')
    latitude = satellite.sublat / ephem.degree
    longitude = satellite.sublong / ephem.degree
    plt.plot(longitude, latitude,
         color='blue', marker='.',
         transform=ccrs.Geodetic(),
         )

#### 表示
print('NOAA 15の航跡:') 
plt.show()
```

#### p277 リスト 9.16 修正版
  (NOAA20に変更しています。）
```python:NOAA20

### ライブラリー導入
!pip install pyephem
!pip install matplotlib
!pip install cartopy
import ephem
import datetime
import numpy as np
import matplotlib.pyplot as plt
from math import degrees as deg

####TLE取得および分割
noaa20="""NOAA 20 (JPSS-1)
1 43013U 17073A   26095.54221320  .00000118  00000+0  77049-4 0  9990
2 43013  98.7724  35.6676 0002041 101.4114 258.7291 14.19543446434165"""

tle0, tle1, tle2 = noaa20.split("\n")
satellite = ephem.readtle(tle0, tle1, tle2)

#### 観測地点の設定
tokyo_station = ephem.Observer()
tokyo_station.lat = '35.6846'
tokyo_station.lon = '139.7106'
tokyo_station.elevation = 3
tokyo_station.date = datetime.datetime.now(datetime.UTC) # Fix for DeprecationWarning

#### 観測地点の表示
print('観測地点の名前:', '東京駅')
print('観測地点の緯度:', tokyo_station.lat)
print('観測地点の経度:', tokyo_station.lon)
print('観測地点の高度:', tokyo_station.elevation,'m')

#### Epochの表示
actual_tle_epoch_dt = ephem.date(satellite.epoch).datetime()
print('TLEエポック:', actual_tle_epoch_dt.strftime("%Y/%m/%d %H:%M:%S UTC"))

#### 衛星の表示
satellite.compute(datetime.datetime.now(datetime.UTC)) # Fix for DeprecationWarning
print('衛星の名前:', tle0)
print('衛星の緯度:', deg(satellite.sublat))
print('衛星の経度:', deg(satellite.sublong))
print('衛星の高度:', satellite.elevation,'m')

satellite.compute(tokyo_station)
print('観測地点から見た衛星の仰角:', deg(satellite.alt))
print('観測地点から見た衛星の方位:', deg(satellite.az))

#### 衛星が可視範囲内に現れる時間と方位
rise_t, az_rise, max_t, alt_max, set_t, az_set = tokyo_station.next_pass(satellite)

print('衛星が地平線の上に昇る時刻:', ephem.localtime(rise_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_rise)))
print('衛星が最大仰角になる時刻:', ephem.localtime(max_t), 'そのときの最大仰角: {0:.1f}'.format(np.rad2deg(alt_max)))
print('衛星が地平線の下に沈む時刻:', ephem.localtime(set_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_set)))

#### 航跡を表示するプログラム
import cartopy.crs as ccrs
from datetime import datetime, timedelta

#### TLEからエポックを計算
dt0 = ephem.date(satellite.epoch).datetime()
time_list = [(dt0 + timedelta(minutes=i)) for i in range(0, 60*12)]

#### 世界地図描画
fig = plt.figure(figsize=(12, 8))
ax = plt.axes(projection=ccrs.PlateCarree())
ax.coastlines()
ax.set_title("Satellite Trak")
ax.set_global()

#### 衛星の航跡をプロット
for dt in time_list:
    satellite.compute(dt) # Directly pass the datetime object
    latitude = satellite.sublat / ephem.degree
    longitude = satellite.sublong / ephem.degree
    plt.plot(longitude, latitude,
         color='blue', marker='.',transform=ccrs.Geodetic(),
         )

#### 表示
print('NOAA 20の航跡:')
plt.show()
```

#### p283 リスト 9.19 CelesTrakからTLEを取得しNOAA15号の位置を計算し航跡を表示するプログラム
bot対策のため、URLは(ここを変えてください)に変更しています。文字通り、この部分を正しいURLに変更してください。
  (NOAA20に変更しています。）

```python:NOAA15C
### ライブラリー導入
!pip install pyephem
!pip install matplotlib
!pip install cartopy
import ephem
import datetime
import numpy as np
import matplotlib.pyplot as plt
from math import degrees as deg

#### 衛星のデータを取得する関数の定義
def fetch_satellite_data():
    url = "(ここを変えてください)"
    response = requests.get(url)    
    
    if response.status_code != 200:
        print("Failed to fetch data from the website.")
        return None

    lines = response.text.strip().split('\n')
    satellite_data = {}

    for i in range(0, len(lines), 3):
        if i + 2 < len(lines):
            satellite_name = lines[i].strip()
            data1 = lines[i + 1].strip()
            data2 = lines[i + 2].strip()
            satellite_data[satellite_name] = [data1, data2]

    return satellite_data

#### 衛星の指定
satellite_name = "NOAA 20 (JPSS-1)"

#### 観測地点の設定
tokyo_station = ephem.Observer()
tokyo_station.lat = '35.6846'
tokyo_station.lon = '139.7106'
tokyo_station.elevation = 3
tokyo_station.date = datetime.datetime.now(datetime.UTC) # Fix for DeprecationWarning

#### 衛星データの取得
data = fetch_satellite_data()
tle0, tle1, tle2 = satellite_name, data[satellite_name][0], data[satellite_name][1]

#### 観測地点の表示
print('観測地点の名前:', '東京駅')
print('観測地点の緯度:', tokyo_station.lat)
print('観測地点の経度:', tokyo_station.lon)
print('観測地点の高度:', tokyo_station.elevation,'m')

#### Epochの表示
actual_tle_epoch_dt = ephem.date(satellite.epoch).datetime()
print('TLEエポック:', actual_tle_epoch_dt.strftime("%Y/%m/%d %H:%M:%S UTC"))

#### 衛星の表示
satellite.compute(datetime.datetime.now(datetime.UTC)) # Fix for DeprecationWarning
print('衛星の名前:', tle0)
print('衛星の緯度:', deg(satellite.sublat))
print('衛星の経度:', deg(satellite.sublong))
print('衛星の高度:', satellite.elevation,'m')

satellite.compute(tokyo_station)
print('観測地点から見た衛星の仰角:', deg(satellite.alt))
print('観測地点から見た衛星の方位:', deg(satellite.az))

#### 衛星が可視範囲内に現れる時間と方位
rise_t, az_rise, max_t, alt_max, set_t, az_set = tokyo_station.next_pass(satellite)

print('衛星が地平線の上に昇る時刻:', ephem.localtime(rise_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_rise)))
print('衛星が最大仰角になる時刻:', ephem.localtime(max_t), 'そのときの最大仰角: {0:.1f}'.format(np.rad2deg(alt_max)))
print('衛星が地平線の下に沈む時刻:', ephem.localtime(set_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_set)))

#### 航跡を表示するプログラム
import cartopy.crs as ccrs
from datetime import datetime, timedelta

#### TLEからエポックを計算
dt0 = ephem.date(satellite.epoch).datetime()
time_list = [(dt0 + timedelta(minutes=i)) for i in range(0, 60*12)]

#### 世界地図描画
fig = plt.figure(figsize=(12, 8))
ax = plt.axes(projection=ccrs.PlateCarree())
ax.coastlines()
ax.set_title("Satellite Trak")
ax.set_global()

#### 衛星の航跡をプロット
for dt in time_list:
    satellite.compute(dt) # Directly pass the datetime object
    latitude = satellite.sublat / ephem.degree
    longitude = satellite.sublong / ephem.degree
    plt.plot(longitude, latitude,
         color='blue', marker='.',transform=ccrs.Geodetic(),
         )

#### 表示
print('NOAA 20の航跡:')
plt.show()
```
#### p287 リスト 9.21 NOAA15号の航跡を表示するプログラム(basemap版)
```python:NOAA15D
#### ライブラリー導入
!pip install pyephem
!pip install matplotlib
import ephem
import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap
from datetime import datetime, timedelta

####TLE取得および分割
noaa15="""NOAA 15
1 25338U 98030A   24219.17306584  .00000415  00000+0  18954-3 0  9992
2 25338  98.5670 245.2526 0010496 172.1414 187.9932 14.26648677364568"""

tle0, tle1, tle2 = noaa15.split("\n")
satellite = ephem.readtle(tle0, tle1, tle2)

#### TLEからエポックを計算
tle1split = tle1.split()
epochraw = float(tle1split[3]) / 1000
epochstr = str(epochraw)
epochlist = epochstr.split('.')
year = int(epochlist[0]) + 2000
doy = float(epochlist[1]) / 100000000

dt0 = datetime(year, 1, 1) + timedelta(days=doy)
time_list = [(dt0 + timedelta(hours=i/60)) for i in range(0,60*12)]

#### 世界地図
fig = plt.figure(figsize=(12, 8)) # 画像サイズを指定(単位はインチ)
m = Basemap()
m.drawcoastlines()

#### TLEの読み込みと表示
tle0, tle1, tle2 = satellite_name, data[satellite_name][0], data[satellite_name][1]
print("衛星のデータ:")
print(tle0, tle1, tle2, sep="\n")
satellite = ephem.readtle(tle0, tle1, tle2)

#### 航跡をプロットする
for dt in time_list:
    dot = dt.strftime("%Y/%m/%d %H:%M:%S")
    satellite.compute(f"{dot}")
    latitude = satellite.sublat / ephem.degree
    longitude = satellite.sublong / ephem.degree
    x1,y1 = m(longitude, latitude)
    m.plot(x1, y1, "m.", markersize=1)

#### 表示
print("衛星の航跡:")
plt.show()
```

#### 練習問題: ISSの航跡 答え
```python:ISS
### ライブラリー導入
!pip install pyephem
!pip install matplotlib
!pip install cartopy
import ephem
import datetime
import numpy as np
import matplotlib.pyplot as plt
from math import degrees as deg

####TLE取得および分割
ISSZ="""ISS (ZARYA)             
1 25544U 98067A   26095.55331950  .00008543  00000+0  16420-3 0  9998
2 25544  51.6328 299.5432 0006351 274.8255  85.2008 15.487869805604925"""

tle0, tle1, tle2 = ISSZ.split("\n")
satellite = ephem.readtle(tle0, tle1, tle2)

#### 観測地点の設定
tokyo_station = ephem.Observer()
tokyo_station.lat = '35.6846'
tokyo_station.lon = '139.7106'
tokyo_station.elevation = 3
tokyo_station.date = datetime.datetime.now(datetime.UTC) # Fix for DeprecationWarning

#### 観測地点の表示
print('観測地点の名前:', '東京駅')
print('観測地点の緯度:', tokyo_station.lat)
print('観測地点の経度:', tokyo_station.lon)
print('観測地点の高度:', tokyo_station.elevation,'m')

#### Epochの表示
actual_tle_epoch_dt = ephem.date(satellite.epoch).datetime()
print('TLEエポック:', actual_tle_epoch_dt.strftime("%Y/%m/%d %H:%M:%S UTC"))

#### 衛星の表示
satellite.compute(datetime.datetime.now(datetime.UTC)) # Fix for DeprecationWarning
print('衛星の名前:', tle0)
print('衛星の緯度:', deg(satellite.sublat))
print('衛星の経度:', deg(satellite.sublong))
print('衛星の高度:', satellite.elevation,'m')

satellite.compute(tokyo_station)
print('観測地点から見た衛星の仰角:', deg(satellite.alt))
print('観測地点から見た衛星の方位:', deg(satellite.az))

#### 衛星が可視範囲内に現れる時間と方位
rise_t, az_rise, max_t, alt_max, set_t, az_set = tokyo_station.next_pass(satellite)

print('衛星が地平線の上に昇る時刻:', ephem.localtime(rise_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_rise)))
print('衛星が最大仰角になる時刻:', ephem.localtime(max_t), 'そのときの最大仰角: {0:.1f}'.format(np.rad2deg(alt_max)))
print('衛星が地平線の下に沈む時刻:', ephem.localtime(set_t), 'そのときの方位: {0:.1f}'.format(np.rad2deg(az_set)))

#### 航跡を表示するプログラム
import cartopy.crs as ccrs
from datetime import datetime, timedelta

#### TLEからエポックを計算
dt0 = ephem.date(satellite.epoch).datetime()
time_list = [(dt0 + timedelta(minutes=i)) for i in range(0, 60*12)]

#### 世界地図描画
fig = plt.figure(figsize=(12, 8))
ax = plt.axes(projection=ccrs.PlateCarree())
ax.coastlines()
ax.set_title("Satellite Trak")
ax.set_global()

#### 衛星の航跡をプロット
for dt in time_list:
    satellite.compute(dt) # Directly pass the datetime object
    latitude = satellite.sublat / ephem.degree
    longitude = satellite.sublong / ephem.degree
    plt.plot(longitude, latitude,
         color='blue', marker='.',transform=ccrs.Geodetic(),
         )

#### 表示
print('ISSの航跡:')
plt.show()
```

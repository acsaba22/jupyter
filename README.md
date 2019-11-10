# Jupyter lab gyors ismerkedes

## Linkek

[Who Data](https://www.who.int/healthinfo/statistics/mortality_rawdata/en/)

[pandas.DataFrame](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html)

[Ploting API axes](https://matplotlib.org/3.1.1/api/axes_api.html)

[styles](https://matplotlib.org/3.1.1/gallery/style_sheets/style_sheets_reference.html)

## Lehetseges celok

* csv vagy excelt beolvasni
* plotolni adatokat
* transformalni amig megkapjuk ami erdekel
* exportalni hogy megmutassuk masnak [html,md,pdf] 

## Installalas

Valasz egy konyvtarat ahova a Jupyter-t instalalod. kb. 300M. Pl. `~/work/jupyterenv`
Minden amit instalalunk egy virtualis environmentbe megy, ha letorlod a konyvtarat akkor eltunik.

Es valasz egy konyvtarat ahova fejlesztesz. Pl. `~/work/datatry`

Hozzunk letre egy virtualis environmentet:

```
$ python3 --version
$ cd ~/work
$ sudo apt install python3-pip
$ python3 -m venv jupyterenv
$ pip list
$ source jupyterenv/bin/activate
$ pip list
$ pip install jupyterlab pandas numpy matplotlib xlrd
$ pip list
$ deactivate
$ pip list
$ mkdir ~/work/datatry
$ cd ~/work/datatry
$ source ~/work/jupyterenv/bin/activate
$ jupyter lab
```

Ez valoszinuleg megnyitja a browseredben, de ha nem akkor nyisd meg a linket amit kiir a konzolra.

## Gyors Demo

Csaba a gepen megmutatja:

* jupyterlab elinditas
* Uj python notebook
* cellak, navigacio, md/code
* a 3x3-as matrixot letrehozunk, sliceoljuk, query-zuk, transofmaljuk, plotoljuk.
* Ora menetenek megbeszelese

## jupyter cheet sheet

shortcutok:

* enter, shft-enter, esc
* a, dd, cv, m, y, 
* ctrl-shft-\[ ; ctrl-shft-\]

## Magyar lakossag

* A WHO-tol tolts le a pop, country_codes, documentation-t fileokat
* Hozzal letre uj python notebookot
* elso cellaban importok es alap beallitas

```
import numpy as np
import pandas as pd
import matplotlib as mpl
import matplotlib.pyplot as plt

mpl.style.use('seaborn')
plt.rcParams['figure.figsize'] = [20, 7]
```

* Olvasd be a pop es country_codes fileokat `pd.read_csv`, irasd ki a tartalmukat
* country_codes-ok kozott keresd meg hungary-t `df[df.column == 'str']`
* !Egyeztessunk
* Egeszitsd ki a pop DataFramet egy 'CountryName' oszloppal (`pop['Country'].replace(name_map)`)
* Pop1-ben van az osszlakossag. Plotold ki magyarorszag lakossagat 1950-tol mostanig. `df.plot(kind='scatter', x='Year', y='Pop1')`
* !Egyeztessunk
* csinalj `hun` DataFramet ami csak magyarorszagot tartalmazza, utana `hun.set_index('Year')`
* csinalj hunmf DataFramet, sorok evek, 2 column: ferfi, no. `hunmf.plot()`
* !Egyeztessunk - Uj feladat: Nezzuk meg hany eveseknel van ferfi-noi kulombseg
* Csaba tegye ki a csv dokumentaciot
* Visszaterunk a hun DF-re. Dobj ki minden column-ot kiveve Sex, Pop2..Pop23 (meg persze year index marad) `df.drop(columns=)` `inplace=True`
* pop2..pop23 helyett oszlop nevek legyenek 0,1,2,3,4,5,10,15,...80,85 `df.rename(columns = {'Pop' + str(i+2): j for i, j in enumerate([0,1,2,3,4] + [i*5 for i in range(1, 18)])})` `inplace=True`
* adj hozza egy "tmp" oszlopot a 0,1,2,3,4 oszlopok osszegevel `df.sum(axis=1)`
* torold le a 0,1,2,3,4 oszlopokat (`df.drop(columns)`). Add hozza nevezd at a tmp oszlopot 0-ra (`rename(columns)`)
* !Egyeztessunk
* csinalj egy hunys DataFramet amelyiknek ket indexe van: Year, Sex. `hun.reset_index().set_index`
* Plotold ki a 1950, 1960, 1970-et a hunys-bol. Csunya? `sort_index(axis=1, inplace=True)`
* !Egyeztessunk
* Csinalj "elet" DataFrame-et ket oszloppal (ferfi, no) es sorok: 0(1950/0eves), 5(1955/5eves), 10(1960/10eves), stb...
* Plotold ki, egy grafikonon hogyan oregedtek az 1950-ben szuletett ferfik/nok
* Plotold ki az aranyukat.

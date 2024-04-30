**INICI DE PREPARACIÓ DE L'ENTORN .VENV EN EL MEU DISPOSITIU**

El primer que fem es descarregar un arxiu zip que conté les instruccions del nou [entorn virtual](https://docs.python.org/es/3/library/venv.html), i el crearem en el directori on treballarem.  

Després de crear el nostre propi entorn el que farem serà activar-lo, assegurar-nos que tots els arxius que hem importat del zip es troben allà i instal·lar tot el programari de l'arxiu txt anomenat "requirements.txt".



Quan tenim l'entorn venv configurat només ens queda instal·lar flask i feedparser per a que poguem començar a crear el nostre projecte. 

A continuació es mostra un exemple de com s'hauria de veure aquesta instal·lació:

```
(.venv) agonzalvezc@PCALUMNE:~/Documents/Python_Projecte_Flask_LM$ pip install flask
        pip install feedparser
Collecting flask
  Using cached flask-3.0.3-py3-none-any.whl (101 kB)
Collecting itsdangerous>=2.1.2
  Using cached itsdangerous-2.2.0-py3-none-any.whl (16 kB)
Collecting Jinja2>=3.1.2
  Using cached Jinja2-3.1.3-py3-none-any.whl (133 kB)
Collecting importlib-metadata>=3.6.0
  Using cached importlib_metadata-7.1.0-py3-none-any.whl (24 kB)
Collecting blinker>=1.6.2
  Downloading blinker-1.8.1-py3-none-any.whl (9.5 kB)
Collecting Werkzeug>=3.0.0
  Using cached werkzeug-3.0.2-py3-none-any.whl (226 kB)
Collecting click>=8.1.3
  Using cached click-8.1.7-py3-none-any.whl (97 kB)
Collecting zipp>=0.5
  Using cached zipp-3.18.1-py3-none-any.whl (8.2 kB)
Collecting MarkupSafe>=2.0
  Using cached MarkupSafe-2.1.5-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Installing collected packages: zipp, MarkupSafe, Werkzeug, Jinja2, itsdangerous, importlib-metadata, click, blinker, flask
Successfully installed Jinja2-3.1.3 MarkupSafe-2.1.5 Werkzeug-3.0.2 blinker-1.8.1 click-8.1.7 flask-3.0.3 importlib-metadata-7.1.0 itsdangerous-2.2.0 zipp-3.18.1
Collecting feedparser
  Using cached feedparser-6.0.11-py3-none-any.whl (81 kB)
Collecting sgmllib3k
  Using cached sgmllib3k-1.0.0-py3-none-any.whl
Installing collected packages: sgmllib3k, feedparser
Successfully installed feedparser-6.0.11 sgmllib3k-1.0.0

```





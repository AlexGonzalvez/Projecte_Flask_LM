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

Per activar l'entorn virtual i començar a treballar, només hem de posar la següent instrucció: 

**source .venv/bin/activate** (s'ha de substituir la paraula .venv (si és necessari) pel nom que l'haguem posat al nostre entorn virtual. 

El primer que hem de fer es veure què tenim al nostre arxiu zip que hem descarregat i importat al nostre projecte, per a fer-ho hem d'activar el nostre entorn Flask. Només hem d'executar el següent a la nostra terminal: **flask run --debug**. Ara ja podem consultar la pàgina sobre la que hem de treballar. En aquest cas consultem la pàgina **index.html** on afegirem dues seccions simples més. 

D'aquesta manera, el codi sense modificar (el de la nostra aplicació) que hauriem de trobar al Visual Studio o entorn similar es el següent: 


```
from flask import Flask, request, render_template, redirect, url_for, flash
from flask import request
import feedparser

app = Flask(__name__)
app.secret_key = '¡3248 97320983 bkjxdlrkfj k2 r9p874989387 98p78oiyylkhçç'

#
# Exemples inicials de flask
#
@app.route("/demo0")
def demo0():
    return "<h1>Hola em dic Alfonso</h1>"

@app.route("/demo1")
def demo1():
    return render_template("exemples/demo/hola.html")

@app.route("/demo2")
def demo2():
    return render_template("exemples/demo/edat.html", nom="Alfonso", edat=26)

@app.route("/demo3/<nom_usuari>/<int:edat>")
def demo3(nom_usuari, edat):
    return render_template("exemples/demo/edat.html", nom = nom_usuari, edat = edat)

@app.route("/demo4")
def demo4():
    nom = request.args.get('nom', default = "Desconegut/a", type = str)
    edat = request.args.get('edat', default = 0, type = int)
    return render_template("exemples/demo/edat.html", nom = nom, edat = edat)

@app.route("/demo5")
def demo5():
    # pàgina mostrant un exemple amb bootstrap
    return render_template("exemples/demo/boostrap.html")

#
# Petit exemple amb flask [SEGUIMENT]
#
@app.route("/hola1")
def hola1():
    return render_template("exemples/hola/salutacio_form.html")

@app.route("/hola2")
def hola2():
    valor_salutacio = request.args.get('salutacio', default = "WTF!", type = str)
    valor_quantes = request.args.get('quantes', default = 1, type = int)
    valor_color_de_fons = request.args.get('color-de-fons', default = "white", type = str)
    valor_gatete = request.args.get('gatete', default = False, type = bool)
    return render_template("exemples/hola/salutacio_resultat.html", 
                           salutacio = valor_salutacio, 
                           quantes = valor_quantes,
                           color_de_fons = valor_color_de_fons,
                           gatete = valor_gatete
                           )

#
# Exemple de formulari amb post
#
@app.route("/insert", methods=['GET', 'POST'])
def insert():
    if request.method == 'GET':
        return render_template("exemples/insert/insert_form.html")
    else:
        # POST
        producte = request.form.get('producte', type = str)
        quantitat = request.form.get('quantitat', type = int)

        # Aquí hauríem de fer alguna cosa amb producte i quantitat
        # com per exemple un insert a la base de dades

        # https://www.seobility.net/es/wiki/Post/Redirect/Get
        flash(f"El producte {producte} amb quantitat {quantitat} s'ha inserit correctament")
        return redirect(url_for('insert'))

@app.route('/')
def index():
    return render_template("index.html")

@app.route('/lavanguardia/<seccio>')
def lavanguardia(seccio):
    rss = get_rss_lavanguardia(seccio)
    return render_template("lavanguardia.html", rss = rss)

def get_rss_lavanguardia(seccio):
    # MODE REMOT: versió on descarrega l'XML de la web
    # xml = f"https://www.lavanguardia.com/rss/{seccio}.xml"
    
    # MODE LOCAL: versió que fa servir l'XML descarregat
    xml = f"./rss/lavanguardia/{seccio}.xml"
    
    rss = feedparser.parse(xml)
    return rss

```



Aquest és només el codi de la nostra connexió i no l'hem de modificar encara, sinó que el que hem de fer és modifica l'index.html, codi que és el següent: 

```
<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="/static/css/style.css">
    <title>Diaris!</title>
</head>
<body>
    <p>Mira les noticies de La Vanguardia:</p>
    <ul>
        <li><a href="/lavanguardia/deportes">Deportes</a></li>
        <li><a href="/lavanguardia/politica">Política</a></li>
        <li><a href="/lavanguardia/vida">Vida</a></li>
    </ul>
    <img src="/static/img/diaris.jpg" alt="Diaris" />
</body>
</html>

```

De tot això només ens hem de fixar en la ruta d'index.html. Si accedim després d'obrir l'entorn Flask, hauriem de veure una pàgina similar a aquesta: 


![Imatge sobre com hauria de ser la nostra pàgina inicial](https://github.com/AlexGonzalvez/Projecte_Flask_LM/blob/master/diaris_init.png)


Ara és el moment d'afegir dues seccions més a la nostra pàgina, que en aquest cas seràn "política" i "vida". Per a fer-ho creem dos arxius XML més amb el nom d'aquestes seccions a l'apartat "rss/vanguardia". Una vegada creats, només hem de posar el codi XML que veiem a la pàgina de la vanguardia. En concret, l'XML que s'ha insertat en el projecte és el seguent: 

-Pàgina de la secció "política": [https://www.lavanguardia.com/rss/politica.xml](https://www.lavanguardia.com/rss/politica.xml)

-Pàgina de la secció "vida": [https://www.lavanguardia.com/rss/vida.xml](https://www.lavanguardia.com/rss/vida.xml)

Una vegada hem realitzat això hem de modificar la plantilla principal de "lavanguardia.html" per mostrar tota la informació dels XML (logo del channel i la url del channel, i per cada item: descripció, dates de creació i de modificació, autor i categoria). Per a fer això hem d'utilitzar feedparser (si es necessita qualsevol informació rellevant, sempre es pot consultar a la seva [documentació oficial](https://www.google.com/url?q=https://feedparser.readthedocs.io/en/latest/common-rss-elements.html&sa=D&source=docs&ust=1715356008391302&usg=AOvVaw1GQQaEX8dtIwGlbr1vzCFK).

Amb feedparser podem obtenir les dades que necessitem de manera sencilla. Primer creem, com si fos un HTML, l'estructura on anirà l'element que volem (és a dir, etiquetes de tipus img, p, etc) i, al moment de posar el valor, l'estil {{ rss.feed.(dada que volem) }} (per exemple, per a obtenir el valor de la imatge del XML, farem un {{ rss.feed.image.url }} (per obtenir la URL d'on surt la imatge) i un {{ rss.feed.image.title }} (per mostrar el títol). Si el que necessitem es mostrar totes les imatges que hi ha a la pàgina, necessitarem un bucle FOR, per recorrer cada item (element) que tenim a la nostra llista d'elements d'on treurem totes les dades necessàries (url, link, descripció, etc.). 

Si ho hem fet bé el nostre codi hauria de semblar-se al següent:

```

<!DOCTYPE html>  <!--Feedparser utiliza el rss que hemos creado en app.py y, poniendole una serie de atributos que corresponden a las etiquetas de nuestro xml, podemos obtener los datos de manera sencilla-->
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>La Vanguardia - {{rss.feed.title}}</title>
    <link rel="stylesheet" href="/static/css/style.css">
</head>
<body>
    <h1>La Vanguardia - <small>{{rss.feed.title}}</small></h1>
    <img src="{{ rss.feed.image.url }}" alt="{{ rss.feed.image.title }}">
    <p><a href="{{ rss.feed.image.link }}">{{ rss.feed.image.link }}</a></p>
    {% for item in rss.entries %}  <!--rss.entries es una lista de páginas que tenemos en la sección de notícias. Aquí se establece que se ha de hacer un recorrido por todas las notícias, y por cada una su información independiente.-->
        <p>
            <a href="{{item.link}}">{{item.title}}</a>
            {% for media in item.media_content %}
                <p><img src="{{media.url}}" alt="{{item.title}}" /></p>
            {% endfor %}
        </p>
    

    <p>Descripción de la notícia - {{item.description}}</p>  <!--Finalmente, mostramos por pantalla la descripción de la notícia, fecha de publicación, modificación, autor, categoría de las notícia-->
    <p>Fecha de publicación - {{item.published}}</p>
    <p>Fecha de modificación - {{item.updated}}</p>
    <p>Autor - {{item.author}}</p>
    <p>Categoría de la notícia- {{item.category}}</p>
    {% endfor %}
</body>
</html>

```
I la nostra pàgina de resultats ens hauria de permetre veure les imatges, amb descripció, títol i dades necessàries. Hauria de ser semblant a la següent:





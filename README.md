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

D'aquesta manera, el codi sense modificar (el de la nostra aplicació) que hauriem de trobar al Visual Studio o entorn similar es el següent (s'han afegit comentaris explicatius per apuntar una mica el que fa cada línea (sobretot les finals, que són les que realment aplicarem en el nostre projecte).

Podem dividir-ho en dues parts: la primera son proves, i la segona ja aplica el projecte:

Primera part:


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

```

Segona part amb comentaris explicatius (la part on ens haurem de centrar): 

```

@app.route('/')
def index():
    return render_template("index.html")   #Esta es la ruta principal (/) en la que usaremos como "template" index.html. Es el inicio de todo

@app.route('/lavanguardia/<seccio>')  #Con cada ruta que generamos creamos una función justo debajo de la ruta, a la que le pasamos como parámetro una sección, que le pasa el usuario desde el ordenador
def lavanguardia(seccio):
    rss = get_rss_lavanguardia(seccio) #Desde aquí creamos el rss, que llama a la función de abajo y simplemente guarda la información del rss, que se obtiene de manera remota (internet) o local
    print(rss.entries[0]) #Esto se usa para buscar datos exactos, los que no coincidan con las etiquetas.
    return render_template("lavanguardia.html", rss = rss) #Esta es la plantilla que se devuelve, con el rss final que pasaremos a nuestro html

def get_rss_lavanguardia(seccio): #Esto define como se obtiene el rss local o de web, que forma el rss final.
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

![Imatge sobre com hauria de ser la nostra pàgina inicial](https://github.com/AlexGonzalvez/Projecte_Flask_LM/blob/master/apunts_2.png)

**BOOTSTRAP**

Ara per continuar amb el nostre projecte, farem servir Boostrap, un framework que servei per donar un estil responsive i únic a les nostres pàgines web. A continuació, s'aniràn documentant unes pràctiques que ens ajudaràn a entendre millor com funciona i que ens poden servir per continuar amb el nostre projecte, ja que mostren les seves funcionalitats principals. 

1. PÀGINA PRINCIPAL:

Per crear una pàgina principal amb Bootstrap, la manera més senzilla és fer-ho amb un codi semblant al següent:

```
<!doctype html>
<html lang="ca">

<head> 
    <!-- Meta tags necessaris -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- CSS del framework bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">

    <title>Estructura inicial</title>
</head>

<body>

    <p>Pàgina amb bootstrap, tot i que no vegis res especial</p>

    <!-- JavaScript del framework bootstrap -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
        crossorigin="anonymous"></script>
</body>

</html>

```
Bootstrap inicia amb les etiquetes HTML principals. A l'etiqueta "head" hem de posar els anomenats "Meta tags" que ens facilitaràn la tasca de visualització, mostrant a cada usuari de manera responsive el contingut de la pàgina segons el dispositiu que estigui utilitzant. És important posar al nostre projecte el CSS del framework de bootstrap en un link "href" tal i com es mostra per importar el seu full d'estil. Finalment, ens hem d'enrecordar de posar l'etiqueta "script" amb el framework de Bootstrap per que puguem utilitzar totes les seves funcionalitats. 

2. CONTAINERS

Els containers a Bootstrap ens facilitaràn molt la feina d'organitzar tota la informació que volem posar a la nostra web. Gràcies a aquesta funció podem posar el text que necessitem en diverses parts i editar-les sense que hi hagi conflictes. Per si fos poc, també ens ajuda a que cadascuna de les parts tingui el seu propi estil, ja que podem ajustar-lo al color i mida que vulguem, (el que pot ser útil per establir la mida del contenidor segons la mida de la pantalla de l'usuari de manera responsive). D'aquesta manera els contenidors són essencials per poder tenir el nostre text creatiu i original. A continuació es mostra un codi on es creen aquests contenidors de diferents mides i que contenen el seu propi text (que descriu si és un contenidor petit, mitjà, gran o molt gran). 

```
<!doctype html>
<html lang="ca">

<head>
    <!-- Meta tags necessaris -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- CSS del framework bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">

    <title>Containers</title>
</head>

<body>

    <div class="container-fluid text-white bg-primary p-5 text-center"> <!--Ocupa todo el espacio-->
        <h1>Hola!</h1>
        <p class="lead">Això és un <mark>container </mark>fluid</p>
    </div>

    <div class="container-sm mt-5 p-4 border border-danger border-5"> <!--Ocupa todo el espacio (mt=margin top, s=start (right), b=bottom, e=end (right)) Valores de separación del 0 al 5-->
        <h1>Hola!</h1>
        <p>Això és un container petit</p>
    </div>

    <div class="container-md"> <!--Ocupa todo el espacio-->
        <h1>Hola!</h1>
        <p>Això és un container mitjà</p>
    </div>

    <div class="container-lg"> <!--Ocupa todo el espacio-->
        <h1>Hola!</h1>
        <p>Això és un container gran</p>
    </div>

    <div class="container-xl"> <!--Ocupa todo el espacio-->
        <h1>Hola!</h1>
        <p>Això és un container molt gran</p>
    </div>

    <div class="container-xxl"> <!--Ocupa todo el espacio-->
        <h1>Hola!</h1>
        <p>Això és un container molt molt gran</p>
    </div>



    <div class="container"> <!--Se ajusta a cada pantalla, y deja márgenes-->
        <h1>Hola de nou!</h1>
        <p>I aquest és un container normal</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Vitae impedit rerum consequuntur, non dicta
            perferendis harum laborum quae fugiat. Sequi explicabo labore ad blanditiis, error consequatur assumenda a
            delectus porro.</p>
    </div>

    <!-- JavaScript del framework bootstrap -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
        crossorigin="anonymous"></script>
</body>

</html>

```
Resultat per pantalla: ![Imatge resultat](https://github.com/AlexGonzalvez/Projecte_Flask_LM/blob/master/Containers.png)


3. GRID

La funcionalitat anomenada "grid" ens permet afegir files i columnes. Aquestes files i columnes van dins de contenidors, el que ens permet modificar les seves propietats (com el seu text, color de vora i distribució de les cel·les en general). Dins de cada contenidor hi ha una etiqueta "div" que conté cada camp, així que és possible modificar cadascún dels camps per separat per personalitzar-lo com vulguem. A continuació hi ha un exemple de codi de com crear un esquema de quadrícules senzill: 

```

<!doctype html>
<html lang="ca">

<head>
    <!-- Meta tags necessaris -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- CSS del framework bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">

    <title>Grid</title>
</head>

<body>

    <div class="container-fluid text-center p-3 bg-primary text-bg-primary">
        <h1>Grid</h1>
    </div>

    <div class="container text-center mt-5 border border-danger">
        <div class="row"> <!--Cada línea tiene 3 columnas-->
            <div class="col border">
                Andorra
            </div>
            <div class="col border"> <!--Se reparte por igual el tamaño en el máximo de la pantalla-->
                Bèlgica
            </div>
            <div class="col border">
                Canadà
            </div>
        </div>
        <div class="row">
            <div class="col border">
                Dinamarca
            </div>
            <div class="col-7 border"> <!--Ocupa 7 columnas en este, a diferencia de las otras dos columnas-->
                Estats Units
            </div>
            <div class="col border">
                França
            </div>
        </div>
        <div class="row">
            <div class="col border">
                Georgia
            </div>
            <div class="col-5 border">
                Holanda
            </div>
            <div class="col-5 border">
                Islàndia
            </div>
        </div>
    </div>

    <div class="container text-center mt-5 border border-warning"> <!--Las columnas que no quepan se irán hacia abajo, ya que al superar el tamaño de la pantalla bajarán-->
        <div class="row">
            <div class="col-md-6 col-lg-4 col-xl-3 border"> 
                Alvocat
            </div>
            <div class="col-md-6 col-lg-4 col-xl-3 border">
                Banana
            </div>
            <div class="col-md-6 col-lg-4 col-xl-3 border">
                Cirera
            </div>
            <div class="col-md-6 col-lg-12 col-xl-3 border">
                Dàtil
            </div>
        </div>
    </div>

    <!-- JavaScript del framework bootstrap -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
        crossorigin="anonymous"></script>
</body>

</html>

```
Resultat per pantalla: Resultat per pantalla: ![Imatge resultat](https://github.com/AlexGonzalvez/Projecte_Flask_LM/blob/master/grid.png)


4. BARRES DE NAVEGACIÓ:

Per crear barres de navegació amb Bootstrap hem de posar els següents atributs a la nostra etiqueta "<body>"

```
<body data-bs-spy="scroll" data-bs-target=".navbar" data-bs-offset="100">
```
D'aquesta manera estem començant a configurar la nostra barra de navegació, però encara hem d'indicar com volem que s'expandeixi o es colapsi. Per això, hem de posar la següent etiqueta:

```
<nav class="navbar navbar-expand-sm bg-primary navbar-dark sticky-top "> <!--Le ponemos a nav una clase de bootrsap (navbar). Con expand indica cuando se expande o cuando se colapsa. Navbar light es para fondos claros, y navbar dark para los oscuros. -->
```
Per centrar el text de la nostra secció de navegació, l'hem de posar a dins d'un contenidor, i a partir d'allà podem posar els botons i items com vulguem. Per fer-ho, no ens podem oblidar de posar etiquetes nav-item on a dins podem posar etiquetes nav que s'ajustin al que necessitem (com per exemple, nav-link, que ens posaria un link href a la direcció web que vulguem).

A continuació es mostra un codi d'exemple que mostra aquesta funcionalitat: 

```
<!doctype html>
<html lang="ca">

<head>
  <!-- Meta tags necessaris -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- CSS del framework bootstrap -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
  <style>
    html {
      scroll-padding-top: 70px;
    }
  </style>
  <title>Exemple</title>
</head>

<body data-bs-spy="scroll" data-bs-target=".navbar" data-bs-offset="100">
    <!--ES preferible poner un nav para empezar la navegación, pero se podría poner un div-->
  <nav class="navbar navbar-expand-sm bg-primary navbar-dark sticky-top "> <!--Le ponemos a nav una clase de bootrsap (navbar). Con expand indica cuando se expande o cuando se colapsa. Navbar light es para fondos claros, y navbar dark para los oscuros. -->
    <div class="container-fluid"> <!--Para centrar el texto tenemos que ponerlo en el contenedor.-->
      <a class="navbar-brand" href="#">Components Arduino</a> <!--Navbar-brand es para que resalte -->
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#collapsibleNavbar">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="collapsibleNavbar">
        <ul class="navbar-nav"> <!--Con ul podemos poner los ítems de la barra de navegación.-->
          <li class="nav-item">
            <a class="nav-link" href="#item-1">Item 1</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#item-2">Item 2</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#item-3">Item 3</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <div class="container-fluid p-5 bg-warning text-bg-warning">
    <h1>Hola?</h1>
    <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rerum atque laborum pariatur rem tempore dolorum
      veritatis quibusdam voluptas deserunt, nulla ratione inventore voluptate est earum facere! Tenetur
      perspiciatis rem eligendi.</p>
  </div>
  
  <div class="container mt-3 p-4 border rounded">
    <h1 id="item-1">Item 1</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
  </div>

  <div class="container mt-3 p-4 border rounded">
    <h1 id="item-2">Item 2</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
  </div>

  <div class="container mt-3 p-4 border rounded">
    <h1 id="item-3">Item 3</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores illo ab provident quos modi vero expedita
      quidem error nihil ipsum possimus iure odio, cumque laudantium quo, ullam ipsa dicta quis?</p>
  </div>

  <!-- JavaScript del framework bootstrap -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
    integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
    crossorigin="anonymous"></script>
</body>

</html>

```
Resultat per pantalla: ![Imatge resultat](https://github.com/AlexGonzalvez/Projecte_Flask_LM/blob/master/navegacio.png)



5. TAULES

Per últim en aquesta part de documentació essencial de Bootstrap, veurem la creació de taules. És una mica semblant al grid, i per a diferenciar-ho podem pensar en això com una funcionalitat no tan flexible com un grid, que ens servirà per donar una disposició uniforme a les nostres dades. Podem imaginar que utilitzem aquest mètode per mostrar les dades d'una base de dades, mentre que utilitzariem grid per dividir les dades en el tamany i disposició que vulguem per mostrar-les d'una manera més creativa. 

La manera de crear-les també és similar al grid, ja que cada text va dins d'un div de columna on especifiquem, gràcies a un atribut "class" les seves característiques úniques. Aquest div de columna hi és dins d'un div de fila (row) i aquest es troba a dins d'un container. 

Un exemple de codi que mostra com crear una taula senzilla podría ser el següent: 

```
<!doctype html>
<html lang="ca">

<head>
  <!-- Meta tags necessaris -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- CSS del framework bootstrap -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
  <style>
    html {
      scroll-padding-top: 70px;
    }
  </style>
  <title>Exemple</title>
</head>

<body data-bs-spy="scroll" data-bs-target=".navbar" data-bs-offset="100">
    <table class="table table-success table-striped">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">First</th>
            <th scope="col">Last</th>
            <th scope="col">Handle</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th scope="row">1</th>
            <td>Mark</td>
            <td>Otto</td>
            <td>@mdo</td>
          </tr>
          <tr>
            <th scope="row">2</th>
            <td>Jacob</td>
            <td>Thornton</td>
            <td>@fat</td>
          </tr>
          <tr>
            <th scope="row">3</th>
            <td>Larry</td>
            <td>the Bird</td>
            <td>@twitter</td>
          </tr>
        </tbody>
      </table>
 <!-- JavaScript del framework bootstrap -->
 <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
 integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
 crossorigin="anonymous"></script>
</body>

</html>

```
Resultat per pantalla: ![Imatge resultat](https://github.com/AlexGonzalvez/Projecte_Flask_LM/blob/master/tablas.png)



Ara que ja hem vist les funcionalitats principals de Bootstrap, podem continuar amb el nostre projecte.


**PART FINAL DEL PROJECTE: DECORACIÓ AMB BOOTSTRAP**

Hem aprés com funciona Bootstrap a través de les petites pràctiques, així que només ens queda acabar d'ajustar la nostra web per a que sigui visual, original i fàcil de llegir. 

El primer que modificarem serà el menú principal *index.html*. Li afegirem colors, posarem les seccions ordenades i farem diversos carrusels: un mostrarà les notícies de manera general, i per a que no quedi tan pobre aquesta pàgina principal, s'afegiràn uns quants més que mostraràn les portades de notícies principals de cada secció per separat. Anem per parts:

1. **INCORPOREM UN MENÚ DE NAVEGACIÓ**

Per realitzar aquest pas haurem de fer ús de l'eina que proporciona Bootstrap *navbar*, que l'afegirem a la part de damunt del tot de la nostra pàgina per a que l'usuari pugui escollir directament a quina secció de notícies li agradaria anar. També s'afegeix la opció de tornar al menú principal (aquest) a través de l'enllaç *home* (per si es troba en una altra pàgina diferent de la principal), i posarem el logo oficial de *La Vanguardia*, amb l'opció de visitar la seva pàgina oficial directament. 

En concret, la línea de codi que es posa per establir un disseny general d'aquest menú és la següent: 

```
navbar navbar-expand-sm bg-primary navbar-dark
```
Per una banda, *navbar-expand* ens indica fins a quant volem que s'expandeixi la nostra barra de navegació, *bg-primary* indica el color que utilitzem per aquesta (en el meu cas, el blau), i *navbar-dark* posa les lletres de color blanc per a poder-les llegir correctament.

A partir d'ara, els elements de la barra de navegació van dins d'un *container-fluid* per a que es puguin ajustar correctament. Dins del contenidor hi ha les etiquetes *navbar-brand* que ens aportarà unes lletres que ressaltin més, i després es posa un altre div que engloba una llista no ordenada d'elements *navbar-item* que són cadascún dels items de la nostra barra de navegació. També tenen incorporat una etiqueta *nabvar-link* que ens serà molt útil i necessari per a portar a l'usuari fins a la pàgina que desitgi només apretant aquest enllaç. 

Podem verificar que la nostra barra de navegació l'hem creat correctament si el nostre codi s'assembla al següent: 

```
<body class="bg-primary-subtle text-black data-bs-spy scroll" data-bs-target=".navbar" data-bs-offset="100">

        <!--ES preferible poner un nav para empezar la navegación, pero se podría poner un div-->

      <nav class="navbar navbar-expand-sm bg-primary navbar-dark "> <!--Le ponemos a nav una clase de bootrsap (navbar). Con expand indica cuando se expande o cuando se colapsa. Navbar light es para fondos claros, y navbar dark para los oscuros. -->
        <div class="container-fluid"> <!--Para centrar el texto tenemos que ponerlo en el contenedor.-->
          <a class="navbar-brand" href="#">Periódicos de La Vanguardia</a> <!--Navbar-brand es para que resalte -->
          <div class="collapse navbar-collapse" id="collapsibleNavbar">
            <ul class="navbar-nav"> <!--Con ul podemos poner los ítems de la barra de navegación.-->
              <li class="nav-item">
                <a class="nav-link" href="/">Home</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/deportes">Deportes</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/politica">Política</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/vida">Vida</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/opinion">Opinión</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/internacional">Internacional</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="https://www.lavanguardia.com/"><img class="logo_vanguardia" src="/static/img/logo_vanguardia.jpeg"/></a>
              </li>
            </ul>
          </div>
        </div>
      </nav>

```
Com es pot comprobar a l'anterior codi, tot aquest menú de navegació hi és dins d'una etiqueta *body* que conté els atributs necessaris per a que *navbar* es mostri correctament, a més d'un afegit: el color de fons de la nostra web! Ara ja tenim un color escollit, que en el meu cas es un blau més fluix. Poc a poc, anem personalitzant la web a la nostra manera. 

La nostra barra de navegació ha quedat de la següent manera: 

Resultat per pantalla: ![Imatge del resultat]()


2. **CREANT EL NOSTRE CARRUSEL**

Per a crear un carrúsel hem de posar les nostres classes i dades dins d'un contenidor, tot seguit d'una sèrie d'etiquetes *</div*. Primer posem un div on identifiquem l'ID del nostre carrusel, i seguidament incorporem un div que s'anomena *carousel-inner* que ens indicarà la unitat del nostre carrúsel, és a dir, a partir d'aquí comencem a incorporar elements que formaràn el nostre propi carrusel. 

Aquests elements són els anomenats *carousel-item* i són això, les imatges (items) que formen el nostre carrusel. Per a incorporar-lo només hem de continuar afegint etiquetes div, primer una que és *carousel-active* que indica quina és la imatge que es mostra primer a l'usuari, de totes les que hi ha al carrusel. Llavors, dins s'aquest *carousel-active* posem una etiqueta *img* i una descripció d'aquesta imatge amb una etiqueta *p*. Les altres etiquetes div a partir d'aqui només necessitaràn anomenar-se *carousel-item* no *carousel-active*, ja que hem especificat ja quina serà la imatge activa per defecte. 

Abans de tancar el nostre *carousel-inner* hem de posar un parell d'etiquetes més, que són les anomenades *button*. No son més que els botons dret i esquerre que permeten que l'usuari passi d'una imatge a una altra. Una vegada hem posar aquests dos botons, podem tancar finalment aquesta etiqueta. 

**IMPORTANT**: És molt important que tinguem al nostre HTML l'script framework de Bootstrap, que ens permetrà executar aquestes funcions. Sense això no funcionarà mai. Sembla una tonteria, (i ho és), però m'he passat unes quantes hores intentant entendre perquè no funcionava el carrusel, per després veure que era només això. El que hem de posar en **tots** els HTML en els que fem servir funcionalitats pròpies de Bootstrap és el següent: 

```
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
      crossorigin="anonymous"></script>
```

El nostre carrusel ja hauria d'estar completament configurat i preparat per funcionar. Podem comprobar si el que hem fet podria funcionar o no si s'ajusta més o menys al següent codi, que és la creació del carrusel: 

```
 <div class="container-fluid">
        <div id="carouselPortada" class="carousel slide" data-bs-ride="carousel">
          <div class="carousel-inner">
            <div class="carousel-item active">
              <img src="/static/img/deportes.jpeg" class="d-block w-100" alt="Imagen de la sección de Deportes">
              <p class="texto_img">Carlos Sainz: "Estoy seguro de que mañana podré subirme al coche y hacerlo bien"</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/internacional.jpeg" class="d-block w-100" alt="Imagen de la sección Internacional">
              <p class="texto_img">El plan de atacar Rafah de Netanyahu obstaculiza un acuerdo con Hamas</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/opinion.jpeg" class="d-block w-100" alt="Imagen de la sección de Opinión">
              <p class="texto_img">Pese a la inflamada retórica de nuestros políticos, no percibo un ambiente guerracivilista</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/politica.jpeg" class="d-block w-100" alt="Imagen de la sección de Política">
              <p class="texto_img">El PSC ganaría las elecciones mientras ERC y Junts se disputarían la segunda plaza, según el sondeo de la Generalitat</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/vida.jpeg" class="d-block w-100" alt="Imagen de la sección de Vida">
              <p class="texto_img">'Rise of the Ronin': "Queremos que los jugadores disfruten de ser un samurái"</p>
            </div>

          </div>
            <button class="carousel-control-prev" type="button" data-bs-target="#carouselPortada" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselPortada" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </button>
        </div>
    </div>

```
Una demostració estàtica de com s'hauria de veure un carrusel funcional podria ser aquesta imatge: 

Resultat per pantalla: ![Imatge del resultat]()

A partir d'aquí, a la pàgina principal he continuat utilitzant el mateix mètode de creació de carrusels, per crear diversos que puguessin mostrar cada secció. Com em sembla massa repetitiu mostrar un procés igual tota l'estona, em limitaré a indicar que l'únic que es fa a partir d'aquí es posar l'estil a la pàgina web a través de titols que contenen estils CSS, i una barra de navegació a sota que mostra el meu nom amb un enllaç al meu Github al pulsar-ho. 

Encara i així deixo el codi final de com queda aquesta pàgina principal amb el seu estil propi, per si és d'interés (encara que sempre es pot veure com queda a la versió final entregada a través del Moodle): 

```
<!DOCTYPE html>
<html lang="ca" >
  
  <head>
      <!-- Meta tags necessaris -->

      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1">

      <!-- CSS del framework bootstrap -->

      <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
      integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
      
      <style>

        .titulo{
          font-size: 20%;
          position:relative;
          margin-left: 30%;
          margin-top:5%;
          font-size:250%;
          margin-bottom: 5%;
          font-family: "Times New Roman", Times, serif;
        }
        .titulo_2{
          font-size: 20%;
          position:relative;
          margin-left: 12%;
          margin-top:10%;
          font-size:250%;
          margin-bottom: 5%;
          font-family: "Times New Roman", Times, serif;
        }
        .titol_destacats{
          margin-top:5%;
          margin-bottom:10%;
          margin-left:10%;
          font-size:180%;
          font-family: "Times New Roman", Times, serif;
          font-weight:bold;
        }

        .titol_seccion{
          margin-top:5%;
          margin-bottom:10%;
          margin-left:25%;
          font-size:180%;
          font-family: "Times New Roman", Times, serif;
          font-weight:bold;
        }



        .img_vida{
          margin-right:0%;
          margin-top:0%;
          width:60%;

        }

        .titol_vida{
          margin-top:5%;
          margin-bottom:3%;
          margin-left:0%;
          font-size:180%;
          font-family: "Times New Roman", Times, serif;
          font-weight:bold;
        }

        .texto_img{
          margin-top:3%;
          font-size:130%;
          font-family: "Times New Roman", Times, serif;
          text-align:center;
        }

        footer{
          position: absolute;
          bottom: -410%; 
        }

        .logo_vanguardia{
          width:15%;
          margin-left:130%;
        }


          
      </style>
        <title>PERIÓDICOS DE LA VANGUARDIA</title>
    </head>
    <body class="bg-primary-subtle text-black data-bs-spy scroll" data-bs-target=".navbar" data-bs-offset="100">

        <!--ES preferible poner un nav para empezar la navegación, pero se podría poner un div-->

      <nav class="navbar navbar-expand-sm bg-primary navbar-dark "> <!--Le ponemos a nav una clase de bootrsap (navbar). Con expand indica cuando se expande o cuando se colapsa. Navbar light es para fondos claros, y navbar dark para los oscuros. -->
        <div class="container-fluid"> <!--Para centrar el texto tenemos que ponerlo en el contenedor.-->
          <a class="navbar-brand" href="#">Periódicos de La Vanguardia</a> <!--Navbar-brand es para que resalte -->
          <div class="collapse navbar-collapse" id="collapsibleNavbar">
            <ul class="navbar-nav"> <!--Con ul podemos poner los ítems de la barra de navegación.-->
              <li class="nav-item">
                <a class="nav-link" href="/">Home</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/deportes">Deportes</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/politica">Política</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/vida">Vida</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/opinion">Opinión</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/lavanguardia/internacional">Internacional</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="https://www.lavanguardia.com/"><img class="logo_vanguardia" src="/static/img/logo_vanguardia.jpeg"/></a>
              </li>
            </ul>
          </div>
        </div>
      </nav>

      <h1 class="titulo">PERIÓDICOS DE LA VANGUARDIA</h1>

    <div class="container-fluid">
        <div id="carouselPortada" class="carousel slide" data-bs-ride="carousel">
          <div class="carousel-inner">
            <div class="carousel-item active">
              <img src="/static/img/deportes.jpeg" class="d-block w-100" alt="Imagen de la sección de Deportes">
              <p class="texto_img">Carlos Sainz: "Estoy seguro de que mañana podré subirme al coche y hacerlo bien"</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/internacional.jpeg" class="d-block w-100" alt="Imagen de la sección Internacional">
              <p class="texto_img">El plan de atacar Rafah de Netanyahu obstaculiza un acuerdo con Hamas</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/opinion.jpeg" class="d-block w-100" alt="Imagen de la sección de Opinión">
              <p class="texto_img">Pese a la inflamada retórica de nuestros políticos, no percibo un ambiente guerracivilista</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/politica.jpeg" class="d-block w-100" alt="Imagen de la sección de Política">
              <p class="texto_img">El PSC ganaría las elecciones mientras ERC y Junts se disputarían la segunda plaza, según el sondeo de la Generalitat</p>
            </div>
            <div class="carousel-item">
              <img src="/static/img/vida.jpeg" class="d-block w-100" alt="Imagen de la sección de Vida">
              <p class="texto_img">'Rise of the Ronin': "Queremos que los jugadores disfruten de ser un samurái"</p>
            </div>

          </div>
            <button class="carousel-control-prev" type="button" data-bs-target="#carouselPortada" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselPortada" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </button>
        </div>
    </div>
    <div class="container-fluid">
      <h1 class="titulo_2">BIENVENIDO A LA PÁGINA WEB DE LA VANGUARDIA</h1>
      <h1 class="titol_destacats">A CONTINUACIÓN PUEDE ECHAR UN BREVE VISTADO A NUESTRAS SECCIONES PRINCIPALES</h1> 
    </div>

    <div class="container-fluid">
      <div class="row">
        <div class="col-md">
          <h1 class="titol_seccion">SECCIÓN DE DEPORTES</h1>
          <div id="carouselDeportes" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-inner">
              <div class="carousel-item active">
                <img src="/static/img/deportes_1.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">La UCO investiga al expresidente de la RFEF por corrupción</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/deportes_2.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Los diez futbolistas mejor pagados pertenecen al Paris Saint-Germain</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/deportes_3.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Luis Rubiales volverá a España el próximo 6 de abril, según la agencia EFE</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/deportes_4.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Durant, octavo máximo anotador de la NBA y Draymond Green se encara con Santi Aldama</p>
              </div>
            </div> 

            <button class="carousel-control-prev" type="button" data-bs-target="#carouselDeportes" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselDeportes" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </button>
      
          </div> 
        </div>
        <div class="col-md">
          <h1 class="titol_seccion">SECCIÓN INTERNACIONAL</h1>
          <div id="carouselInternacional" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-inner">
              <div class="carousel-item active">
                <img src="/static/img/internacional_1.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Una nueva investigación rastrea el origen de importaciones cruciales</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/internacional_2.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">La policía desmantela el campamento de la UCLA y arresta a unas 200 personas</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/internacional_3.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Biden condena la “violencia” en las protestas y dice que no van a cambiar su apoyo a Israel</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/internacional_4.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">El hombre que mató a un niño con una espada en Londres tiene nacionalidad española y brasileña
                </p>
              </div>
            </div> 

            <button class="carousel-control-prev" type="button" data-bs-target="#carouselInternacional" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselInternacional" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </button>
      
        </div>
      </div>
      <div class="row">
        <div class="col-md">
          <h1 class="titol_seccion">SECCIÓN DE OPINIÓN</h1>
          <div id="carouselOpinion" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-inner">
              <div class="carousel-item active">
                <img src="/static/img/opinion1.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Los ensayos de Esquirol invitan a un horizonte de vida madura, fecunda y espiritual</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/opinion2.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Tanto en común con Daniel Levinas y tantos proyectos por delante. ¡Qué gran pérdida!</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/opinion3.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Ambiente de Feria en el Parc del Fòrum</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/opinion4.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Taurófilos como yo</p>
              </div>
            </div> 

            <button class="carousel-control-prev" type="button" data-bs-target="#carouselOpinion" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselOpinion" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </button>
          </div>
        </div>

        <div class="col-md">
          <h1 class="titol_seccion">SECCIÓN DE POLÍTICA</h1>
          <div id="carouselPolitica" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-inner">
              <div class="carousel-item active">
                <img src="/static/img/politica_1.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Sánchez resta trascendencia a una candidatura de Puigdemont: “Ya se presentó en 2017 y 2021”
                </p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/politica_2.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">Carlos Mazón subraya la "estabilidad" con Vox ante la "debilidad" de Pedro Sánchez
                </p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/politica_3.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">El trumpismo castizo pide calma</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/politica_4.jpeg" class="d-block w-100" alt="Imagen de noticia">
                <p class="texto_img">El Consell avanza que la auditoría al sector público instrumental deja datos "preocupantes"</p>
              </div>
            </div> 

            <button class="carousel-control-prev" type="button" data-bs-target="#carouselPolitica" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselPolitica" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </button>
      
        </div>
      </div>
    
    </div>
    
    <div class="container justify-content-center align-items-center m-3">
      <div class="row">

        <div class="col text-center">
          <h1 class="titol_vida">SECCION DE VIDA</h1>
          <div id="carouselVida" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-inner">
              <div class="carousel-item active">
                <img src="/static/img/vida_1.jpeg" class="img_vida" alt="Imagen de noticia">
                <p class="texto_img">EE.UU. saca una regulación contra las emisiones para que la mayoría de los coches sean eléctricos</p>
                
              </div>
              <div class="carousel-item">
                <img src="/static/img/vida_2.jpeg" class="img_vida" alt="Imagen de noticia">
                <p class="texto_img">La prevención, clave para combatir la insuficiencia cardiaca</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/vida_3.jpeg" class="img_vida" alt="Imagen de noticia">
                <p class="texto_img">Más sequías, más largas y más intensas, resultado de la acción humana</p>
              </div>
              <div class="carousel-item">
                <img src="/static/img/vida_4.jpeg" class="img_vida" alt="Imagen de noticia">
                <p class="texto_img">Iberdrola ha plantado más de tres millones de árboles y llegará a cinco a finales de año</p>
              </div>
            </div>
            
            <button class="carousel-control-prev" type="button" data-bs-target="#carouselVida" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselVida" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </button>
            
        </div>
      </div>
    
    <div>
      <!-- JavaScript del framework bootstrap -->
      <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
      crossorigin="anonymous"></script>
    </div>
    
  </body>

  <footer>

    <navbar>
      <div class="container-fluid"> <!--Para centrar el texto tenemos que ponerlo en el contenedor.-->
        <a class="navbar-brand navbar navbar-expand-sm bg-primary navbar-dark navbar-toggler" href="https://github.com/AlexGonzalvez/Projecte_Flask_LM">Proyecto realizado por Álex Gonzalvez Cuadrado</a> <!--Navbar-brand es para que resalte -->
      </div>
    </navbar>
  </footer>

</html>

```
Ja només ens queda veure com quedarà finalment la nostra pàgina que mostra seccions de notícies. La perfeccionarem amb Bootstrap i li incorporarem l'estil que es troba a la pàgina principal per a que tot tingui sentit i sigui uniforme. 

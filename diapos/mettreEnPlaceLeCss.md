# Mettre en place le CSS

----

## Le CSS
Le CSS sert à gérer la mise en forme de notre site. Il permet de choisir la couleur du texte, la police utilisée, la taille du texte, les bordures, le fond... Il permet aussi de faire la mise en page du site, par exemple de placer un menu à gauche et qu’il occupe telle largeur, l’en-tête du site soit calé en haut et qu’il soit toujours visible, etc...

Il est possible d’aller sur le site https://caniuse.com/ pour voir la compatibilité des fonctionnalités HTML et CSS sur différentes navigateurs.

----

## Où écrit-on le CSS ?
On peut l’écrire dans 3 endroits différents :
- **dans un fichier .css (méthode la plus recommandée)**
- dans l’en-tête <head> du fichier HTML
- directement dans les balises du fichier HTML via un attribut style (méthode la moins recommandé)
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <link rel="stylesheet" href="style.css" />
        <title>Premiers tests du CSS</title>
    </head>

    <body>
        <h1>Mon super site</h1>

        <p>Bonjour et bienvenue sur mon site !</p>
        <p>Pour le moment, mon site est un peu <em>vide</em>. Patientez encore un peu !</p>
    </body>
</html>
```

La ligne 5 de l’exemple indique que ce fichier HTML est associé à un fichier appelé style.css et chargé de la mise en forme.

Créons un fichier style.css pour écrire le texte de tous les paragraphes soit écrit en bleu.
```css
p
{
    color: blue;
}
```

**Dans l’en-tête <head> du fichier HTML**
Il faut insérer le code CSS directement dans une balise `<style>` à l’intérieur de l’en-tête `<head>`.*
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <style>
            p
            {
                color: blue;
            }
        </style>
        <title>Premiers tests du CSS</title>
    </head>

    <body>
        <h1>Mon super site</h1>

        <p>Bonjour et bienvenue sur mon site !</p>
        <p>Pour le moment, mon site est un peu <em>vide</em>. Patientez encore un peu !</p>
    </body>
</html>
```

**Directement dans les balises**
Ajouter un attribut `style` à n’importe quelle balise.
```html
<p style="color: blue;">Bonjour et bienvenue sur mon site !</p>
```

----

## Appliquer un style : sélectionner une balise
Dans un code CSS, on trouve trois éléments différents :
- **des noms de balises :** on écrit les noms des balises dont on veut modifier l’apparence. Pour modifier l’apparence des balises `<p>`, je dois écrire p.
- **des propriétés CSS :** les effets de style de la page sont rangés dans des propriétés. Il y a par exemple la propriété color qui permet d’indiquer la couleur du texte, font-size pour la taille du texte...
- **les valeurs :** pour chaque propriété CSS, on doit indiquer une valeur, par exemple pour la propriété color, il faut indiquer le nom de la couleur.

```css
p
{
    color: blue;
}
```

Une feuille de style CSS ressemble donc à cela :
```css
balise1
{
    propriete1: valeur1;
    propriete2: valeur2;
    propriete3: valeur3;
}

balise2
{
    propriete1: valeur1;
    propriete2: valeur2;
    propriete3: valeur3;
    propriete4: valeur4;
}

balise3
{
    propriete1: valeur1;
}
```

Si l’on souhaite appliquer la même présentation à deux balises, on peut combiner la déclaration comme ceci :
```css
h1, em
{
    color: blue;
}
```

**Des commentaires dans du CSS**
Il suffit de mettre du texte entre /\* et \*/

----

## Appliquer un style : class et id

### Les attributs class et id

Pour éviter que toutes les balises paragraphe aient la même présentation, il faut utiliser des attributs spéciaux qui fonctionnent sur toutes les balises : **class** et **id**. Ces deux attributs sont quasiment identiques à une petite différence près.
```css
<h1 class=""> </h1>
<p class=""> </p>
<img class="" />
```

Par exemple, pour associer à un paragraphe :
 ```html
<p class="introduction">Bonjour et bienvenue sur mon site !</p>
 ```
et en CSS, il faut indiquer que l’on souhaite appliquer un style pour les balises identifié par **l’attribut class** introduction. Il faut marquer le nom de classe en commençant par un point.
```css
.introduction
{
    color: blue;
}
```

**L’attribut id** fonctionne de la même manière sauf qu’il ne peut être utilisé qu’une fois dans le code. Cela pourra être utile en JavaScript pour reconnaître certaines balises.
En pratique, nous ne mettrons des id que sur des éléments qui sont uniques dans la page, comme par exemple le logo.
 ```html
<img src="images/logo.png" alt="Logo du site" id="logo">
 ```
En CSS, pour définir les propriétés d’un attribut id, il faut faire précéder le nom de l’id par un #.
 ```css
#logo
{
    /* Indiquez les propriétés CSS ici */
}
 ```

Pour ne pas mélanger les deux, il faut retenir que deux balises peuvent avoir le même nom avec l’attribut class. Un nom d’id doit en revanche être unique dans la page HTML.

### Les balises universelles
Le problème de class et id est que ce sont des attributs et qu’ils s’appliquent donc à une balise entière comme un paragraphe. Si on souhaite modifier uniquement un mot dans le paragraphe, il faut donc utiliser une des deux balises qui ne servent à rien, c’est à dire qui n’ont aucune signification particulière, qui sont dites universelles. Il y a une différence entre ces deux balises :
- `<span></span>` : c’est une balise de type inline, c’est-à-dire que l’on place au sein d’un paragraphe de texte pour sélectionner certains mots uniquement, comme les balises `<strong>` et `<em>`.
- `<div></div>` : c’est une balise de type block, qui entoure un bloc de texte, comme les balises `<p>` et `<h1>`. Ces balises créent un nouveau bloc dans la page et provoque donc un retour à la ligne. `<div>` est fréquemment utilisée dans la construction d’un design, comme nous le verrons plus tard.

Seul le mot bienvenue va s’écrire en bleu.
HTML :
 ```html
<p>Bonjour et <span class="salutations">bienvenue</span> sur mon site !</p>
 ```
CSS :
 ```css
.salutations
{
    color: blue;
}
 ```

----

## Appliquer un style : les sélecteurs avancés
En CSS, le plus difficile est de savoir cibler le texte dont on veut changer la forme. Pour cibler (ou sélectionner) les éléments de la page à modifier, on utilise ce qu’on appelle des **sélecteurs**.

*Les sélecteurs que l’on connaît déjà :*
- p
- h1
- em
- etc...
- .class
- #id

*Les sélecteurs avancés :*
- \* : sélecteur universelle qui sélectionne toutes les balises sans exception.
 ```css
*
{
}
 ```

- A B : une balise contenu dans une autre
Par exemple, pour sélectionner toutes les balises `<em>` situées à l’intérieur d’une balise `<h3>`.

```css
h3 em
{

}
```

- A + B : une balise qui en suite une autre. Sélectionne la première balise B située après une balise A
- A[attribut] : une balise qui possède un attribut.
Par exemple, a[title] sélectionne tous les liens qui possèdent un attribut title
- A[attribut=”Valeur”] : une balise qui possède un attribut avec une valeur exacte
- A[attribut*=”Valeur”] : idem, l’attribut doit cette fois contenir le mot Valeur.

Il existe beaucoup d’autres sélecteurs. Nous en découvrirons certains dans la suite du cours.

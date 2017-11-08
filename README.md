# Documentation widget visual commerce.

Si vous n'avez pas d'uuid, merci de demander à support@headoo.com

## Intégration

Ajouter un div avec un id "widget-container" dans la page là ou le widget doit apparaître ainsi que le code suivant:

```
<script src="https://dab0b4kce2l36.cloudfront.net/js/widget-visualcommerce.js"></script>
<script>
    jQueryHeadoo(document).ready(function() {
        jQueryHeadoo.fn.visualCommerce({
            container: '#widget-container',
            uuid: ‘VOTRE_IDENTIFIANT’,
            locale: 'fr'
        });
    });
</script>
```

Lorsque vous ne pouvez pas modifier le template, un autres mode d'intégration est possible, en ciblant un élément dans la page et en se positionnant au choix avant ou après comme dans l'éxemple suivant avec le paramètre "placement". Le paramètre "selector" est un selecteur jQuery et "order" accepte les valeurs 'before' et 'after'.

```
<script src="https://dab0b4kce2l36.cloudfront.net/js/widget-visualcommerce.js"></script>
<script>
jQueryHeadoo(document).ready(function() {
    jQueryHeadoo.fn.visualCommerce({
        placement : {selector: '.selector:last', order: 'before|after'}
	uuid: ‘VOTRE_IDENTIFIANT’,
	locale: 'fr'
    });
});
</script>
```

Si des contenus sont enrichis d'au moins un tag et modérés positivement, le widget les affichera. Le cas échéant le widget disparaît de la page. Pour modifier ce comportement, en environnement de recette par exemple, vous pouvez ajouter ce paramètre "filters: {}", le widget affichera alors tous les derniers contenus aspirés directement.

Voici un exemple de ce mode:

`http://headoo.com/static/html/testvc.html`

Pour afficher le widget en mode galerie, il vous suffit d'ajouter le paramètre mode: "gallery". Voici un exemple:

```
<script src="https://dab0b4kce2l36.cloudfront.net/js/widget-visualcommerce.js"></script>
<script>
    jQueryHeadoo(document).ready(function() {
        jQueryHeadoo.fn.visualCommerce({
            container: '#widget-container',
            uuid: ‘VOTRE_IDENTIFIANT’,
            locale: 'fr',
	    mode: 'gallery'
        });
    });
</script>
```


Voici un exemple de ce mode:

`http://headoo.com/static/html/testvc-gallery.html`

## Options avancées

Les options avancées sont les suivantes, avec les valeurs par défaut : 


    settings: {
                container: null,
                placement: null, // Dynamically inject container on DOM exemple value: {selector: '.selector:last', order: 'before|after'}
                visualcommerce_id: null,
                uuid: null,
                tag_shortname: null, // Specific tag shortname to filter UGC
                widget_mode: 'widget', // ['widget'||'gallery']
                locale: 'en',
                width: '100%',
                itemWidth: 200, // Only for 'gallery' mode
                arrow_size: 'normal', // Only for 'widget' mode other value: 'small'
                gutter: 20, // Space between items
                height: 200, // Only for 'widget' mode
                limit: 15, // Pagination limit
                speed: 500, // Widget scroll easing speed
                resize_breakpoint: 546, // The container width until the items are resized to fill the widget space (only for widget mode)
                sort: '{"created_at":"desc"}', // API sort options
                filters: '{"moderated":"1","tagged":"1"}', // API filter
                scheme: 'https', // Scheme for API call
                domain: 'headoo.com', // Domain for API call
                domain_assets: 'headoo.com', // Domain for assets loading
                assets_cache: true, // Cache or not assets
                hideTags: false, // Flag to hide the tags
                debug: false // Call API in app_dev mode
    }



## Filtrer les contenus affichés

Si vous souhaitez filtrer les contenus affichés dans le widget en fonction d'un tag existant, il vous suffit d'ajouter un paramètre "tag_shortname: '123456789a'".

```
<script src="https://dab0b4kce2l36.cloudfront.net/js/widget-visualcommerce.js"></script>
<script>
    jQueryHeadoo(document).ready(function() {
        jQueryHeadoo.fn.visualCommerce({
            container: '#widget-container',
            uuid: ‘VOTRE_IDENTIFIANT’,
            locale: 'fr',
	      tag_shortname: '123456789a'
        });
    });
</script>
```


Précision : Si à la place de '123456789a' vous mettez 'sac 123456789a' , tous les produits dont un tag id contient Sac '123456789a' vont apparaître. C'est pourquoi nous déconseillons les tag id contenant des espaces. En revanche, nous vous invitons à mettre plusieurs tags par produit, reprenant notamment l’id produit et ses catégories.


## Masquer les tags dans la popin

Pour masquer les tags dans la popin, partie droite, il suffit d’ajouter le paramètre hide_tags.

```
<script src="https://dab0b4kce2l36.cloudfront.net/js/widget-visualcommerce.js"></script>
<script>
    jQueryHeadoo(document).ready(function() {
        jQueryHeadoo.fn.visualCommerce({
            container: '#widget-container',
            uuid: ‘VOTRE_IDENTIFIANT’,
            locale: 'fr',
            hide_tags: true
        });
    });
</script>
```


## Autres mode d’intégration

Passer par l’API REST : 
[exemple d’API](https://api.headoo.com/api/v1/photos/get.json?uuid=7332ba4b-6cac-480d-9466-f2acfa91&limit=15&sorts={%22created_at%22:%22desc%22}&filters={%22moderated%22:%221%22,%22tagged%22:%221%22}&limit=15)

Là aussi il faudra remplacer la valeur de uuid avec la valeur que l’on aura fourni

Cette API ne requiert PAS d'authentification

[Référence de l'API](https://admin.headoo.com/doc/api)

Utiliser systématiquement https://api.headoo.com au lieu de https://headoo.com (https://headoo.com sera déprécié courant 2018 pour les appels API)


## Showcase
### ishop.galery
Notre produit ishop.gallery utilise notre API

Par exemple, sur https://ishop.gallery/soniarykiel/, voici l'API utilisée : `https://ishop.gallery/api/v1/photos/get.json?uuid=e70359e0-6ef9-4c1a-81b5-a6bbbcea&sorts={%22sort%22:%22asc%22,%22instagram_created_at%22:%22desc%22}&limit=20&page=1&_=1510157242205`

### Foir'fouille
* [Home](https://www.lafoirfouille.fr/) widget headoo avec personnalisation de la taille des images via configuration itemWidth : . On peut voir dans les sources (onglet network dans Chrome) que le widget utilise l'API, en l'occurence : `https://headoo.com/api/v1/photos/get.json?uuid=1dcd47d8-695c-4134-b5ec-3108ed15066f&limit=15&sorts={%22created_at%22:%22desc%22}&filters=[object%20Object]&limit=15` avec des paramètres de tri, de limit et de filtre.

* [Page gallerie dédiée](https://www.lafoirfouille.fr/galerie-photo-communaute.html) avec un mode d'affichage gallerie et une limite du nombre d'objets retournés

        widget_mode: 'gallery',
        limit: 18,

    Ici aussi, l'API appelée par le widget est visible dans l'onglet network : `https://headoo.com/api/v1/photos/get.json?uuid=1dcd47d8-695c-4134-b5ec-3108ed15066f&limit=18&sorts={%22created_at%22:%22desc%22}&filters=[object%20Object]&limit=18`


### Etam

* [Page produit](http://www.etam.com/nuit/modeles/combinaisons/combinaison-zebre-648612902.html#headoo-widget-vc-slogan) Dans ce cas, le widget a été implémentanté dans un tag [GTM](https://www.google.com/intl/fr/tagmanager/). L'appel API est visible dans la console de debug avec un filtre sur la référence produit (`tag_shortname=648612902`) et les produits modérés (`moderated:"1"`) : `https://headoo.com/api/v1/photos/get.json?uuid=3e87b615-02a1-4915-a41f-0aa7510c&limit=15&sorts={%22created_at%22:%22desc%22}&filters={%22moderated%22:%221%22,%22tagged%22:%221%22}&limit=15&tag_shortname=648612902`

* [Page produit](http://www.etam.com/maillots-de-bain/les-hauts-de-maillot/haut-de-maillot-de-bain-triangle-imprime-palmier-648603190.html#headoo-widget-vc-slogan) autre exemple avec plusieurs produits retournés

### Monnier Frères
* [Page produit](http://www.monnierfreres.fr/hui-sac-seau-m-86926a-lan005039-fr.html#fparent) Dans ce cas, le widget est appelé dans un iframe (source : `http://www.monnierfreres.fr/headoo.php?sku=LAN005039`). L'appel API est visible dans la console de debug avec un filtre sur la référence produit : `https://headoo.com/api/v1/photos/get.json?uuid=db559230-db1b-4ec6-bd7e-7eca8f094608&limit=15&sorts={%22created_at%22:%22desc%22}&filters={%22moderated%22:%221%22,%22tagged%22:%221%22}&limit=15&tag_shortname=LAN005039`

### The Great European Carnival
* [Page gallerie dédiée](http://www.tgec.asia/social/), appel API par le widget : `https://headoo.com/api/v1/photos/get.json?visualcommerce_id=9&limit=15&sorts={%22created_at%22:%22desc%22}&filters={%22moderated%22:%221%22}&limit=15`

## Remarques

dab0b4kce2l36.cloudfront.net est le CDN de headoo.com

Dans le cas, ou il est impossible de modifier le site où le widget va être intégré, il est possible de l'intégrer dans un élément existant de la page. Pour ce faire il suffit de remplacer le paramètre "container"par "placement: {selector: '.cross-sell h2', order: 'before'}". 
"selector" doit pointer vers un élément existant dans la page et la valeur de "order" doit être 'before' ou 'after'. 


Concernant les medias dans la section "meilleurs publications", si ce ne sont pas des publications à l'intérieur de la période d'absorption, elles ne seront pas absorbées.

En fonction de votre contrat, il y a une limite d'absorption par heure, paramétrable, donc certains medias peuvent ne pas être absorbés, notamment si le flux créé sur instagram pour l'ensemble de vos hashtags est supérieur à ce chiffre.

Pour répondre au sujet des "meilleurs publications", nous avons dans notre roadmap une fonctionnalité qui consiste à permettre d'absorber un media instagram donné. On pourrait envisager par exemple un bouton [absorber les "meilleurs publications"] et/ou un bouton : [absorber un post précis].

C'est un développement que nous envisageons de mettre en place fin 2017/début 2018.

BASIS WEBSITE STAPPENPLAN :
------------------------------------------------------------------------------------------------------------

STAP 1 --- DE BASIS :
-  We beginnen met een nieuw project
   File > New > Project --> geef het project een titel --> Create
-  RechterMuisKnop op map basis-website-stappenplan (links in het scherm)
   Kies New > Directory --> noem deze map "assets" Nu heb je je assets map
   In deze directory kun je al je afbeeldingen, ect. zetten die je nodig hebt
-  RechterMuisKnop op map basis-website-stappenplan (links in het scherm)
   Kies New > HTML File --> noem deze "index". Nu heb je je index.html
   WEBSTORM vult automatisch de index.html aan met de <head> en <body>

-  RechterMuisKnop op map basis-website-stappenplan (links in het scherm)
   Kies New > Stylesheet --> noem deze "styles". Nu heb je je styles.css
Eerste stuk HTML:
<head>
 <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
 <link rel="stylesheet" href="styles.css">
 <title>Business Website</title>
</head>
Bij de <HEAD> staat al de META CHARSET en we voegen de "VIEWPORT" toe. Dit zorgt ervoor dat de content op welke device dan ook het hele scherm beslaat op 100% schaal.
We voegen de LINK naar CSS nog toe en de TITLE voor bovenop het TABBLAD.

STAP 2 --- DE DEFAULT STYLES :

2.1 :

-  Bovenaan je styles.css zet je de imports van FONTS:
@import url('https://fonts.googleapis.com/css2?family=Merriweather&family=Roboto:wght@300;400;700&display=swap');

-  Nu maak je in styles.css je de uitgecommentarieerde indeling voor je STYLES aan.
   De standaard indeling ziet er zo uit:

/*////////////////////////
    Table of Contents
    1. Global Styles
    2. Typography
    3. Layout
        3.1 Reusables
        3.2 Other
    4. Areas
        4.1 Header
        4.2 Introduction
        4.3 Work
        4.4 Services
        4.5 Contact
        4.6 Footer
    5. Media Queries
////////////////////////*/
-  We gaan vervolgens de GLOBAL STYLES instellen. De global styles zullen voor de
   hele site gelden tenzij je dit specifiek anders aangeeft door middel van CLASS of ID.

/* ------ 1. Global Styles -------------------------------- */

/* Hier zijn alle kleuren voor de site al bepaald, dit is heel overzichtelijk. Vooral --primary en --secondary zal
   je vaak gebruiken (bijv  color: var(--primary);  )
 */
:root {
    --primary: #5722CD;
    --primary-dark: #4B49E8;
    --secondary: #ED4385;
    --text: #7A7A7A;
    --text-dark: #0c0c0c;
    --text-faded: #f2f0ff;
    --grey: #F3F6F9;
}

* {
    margin: 0;
    padding: 0;
    /*Dit is belangrijk zodat de breedtes en hoogtes van elementen worden berekend INCLUSIEF padding en borders */
    box-sizing: border-box;
}

body {
    font-family: Roboto, Arial, Helvetica, sans-serif;
    font-weight: 300;
    font-size: 20px;
}

/* -----------------------------------------------------------------------------------------------------------------------------*/
Je hebt nu dus alvast je kleuren voor de gehele site ingesteld, ook je standaard lettertype voor je body is alvast bepaald. De Lettertypes Roboto en Merriweather hebben we dus al geimporteerd. Let op dat je bij alledrie de delen van deze stap de waarden altijd nog kan veranderen/weghalen.
2.2 :

We gaan verder met de DEFAULT LETTERTYPES :

/* ------------- 2. Typography ----------------------------------- */

h1, h2, h3, h4, h5, h6 {
    font-family: Merriweather, 'Times New Roman', serif;
}

h1, h2 {
    font-size: 36px;
    padding: 16px 0;
}

h3 {
    font-size: 26px;
}

h4 {
    font-size: 32px;
    padding: 12px 0;
    margin: 24px 0;
}

/* Hier is de SQUIGGLE-Line in de CSS opgelost, dus de squiggle-line komt bij
   h4 nu altijd onder de text te staan met deze afstand. */
h4::after {
    display: block;
    content: '';
    margin: 24px 0 0;
    width: 57px;
    height: 6px;
    background-image: url(./assets/squiggle_line.svg);
}

h5 {
    font-size: 32px;
    padding: 12px 0;
}

h6 {
    font-size: 22px;
    line-height: 1.5;
    padding: 12px 0;
}

p {
    margin: 12px 0;
}

/* -------------------------------------------------------------------- */
Je hebt nu dus FONT STYLES voor de hele site ingesteld. Ook heb je gezorgd dat als er ergens op de site h4 headlines gezet worden, dat er dan direct een SQUIGGLE onder komt te staan. Als we dus bijvoorbeeld een h1 in een h4 zouden veranderen in de HTML dan zou deze headline dus kleiner worden EN er komt dan een squiggle onder.

2.3 :

We gaan aan het eind van deze stap de HERBRUIKBARE styles toevoegen.

/* --------------- 3.1 Reusables ----------------------- */

/* De buitenste container is altijd de volledige schermbreedte. Het is een flexbox container die zijn inhoud altijd netjes horizontaal centreert ZODRA JE DISPLAY: FLEX; erin zet is het (ook) een FLEX-CONTAINER (PARENT)*/
.outer-content-container {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
}

/*
-   De binnenste container is maximaal 1400px breed, zodat het er ook
    goed uitziet op brede schermen.

-   Hij mag krimpen als het scherm minder breed wordt, maar niet
    groeien als er meer ruimte is. We voegen margin toe aan de linker-
    en rechterkant, zodat de content nooit helemaal tegen de rand
    gedrukt kan worden.
-   We zorgen er ook voor dat deze flex-item op haar beurt ook weer een
    flexbox container is, waarin alle children onder elkaar komen te
    staan*/
.inner-content-container {
    flex-basis: 1400px;
    flex-shrink: 1;
    flex-grow: 0;
    margin: 0 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 2;
}

/* Deze text-restrictor is ervoor om te zorgen dat de teksten van verschillende vlakken op dezelfde breedte worden afgesneden.
   We gebruiken hier geen flex-basis property, omdat dit element soms in een parent met column-richting en soms in een parent met row-richting kan staan.
   In een column gaat flex-basis over de hoogte, niet de breedte. Dus om dan alsnog de breedte te veranderen, hebben we max-width (nooit groter dan dit) property nodig */
.default-text-restrictor {
    max-width: 850px;
    text-align: center;
}

/* Default-area-padding zorgt ervoor dat er ruimte aan de boven- en onderkant van de text content komt te staan, als we dit
   weg zouden laten staat de text op de rand van de area van de site Je kunt dit ook oplossen in de area zelf maar dit is netter. */
.default-area-padding {
    padding: 200px 0 100px 0;
}

/* Dit is de driehoek die er optisch voor zorgt dat de delen van de pagina schuin afgesneden worden
   .skewer--bottom is voor als de bodem schuin afgesneden moet worden */
.skewer--bottom {
    border-bottom: 50px solid white;
    border-right: 100vw solid transparent;
    position: absolute;
    bottom: 0;
    left: 0;
    z-index: 1;
}

/* Dit is de driehoek die er optisch voor zorgt dat de delen van de pagina schuin afgesneden worden
   .skewer--top is voor als de bovenkant schuin afgesneden moet worden */
.skewer--top {
    position: absolute;
    top: 0;
    left: 0;
    border-top: 50px solid white;
    border-left: 100vw solid transparent;
    z-index: 1;
}

/* --------------- 3.2 Other --------------------------- */

a,
a:visited,
a:link {
    text-decoration: none;
    color: var(--primary);
}

button {
    font-size: 14px;
    font-weight: 300;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: white;
    background-color: var(--secondary);
    border: none;
    border-radius: 50px;
    box-shadow: 0 5px 8px 4px rgba(0, 0, 0, .2);
    padding: 25px 40px;
    margin: 28px 0;
}

/* Hierdoor veranderd je cursor in een wijzend handje als je HOVER over BUTTON */
button:hover {
    cursor: pointer;
}

/* --------------------------------------------------------------- */
Nu heb je het skelet van de styles opgezet. (Waarschijnlijk weet je niet van te voren wat je allemaal nodig hebt, maar voor dit stappenplan gaan we ervanuit dat je al wist dat je Links/Buttons en de Skewer Driehoeken nodig hebt. Net als je het TYPOGRAPHY pas gaat indelen zodra je hiermee ook in html bezig bent)

Het belangrijkste is alles wat je hebt ingevult bij 2.1 en de outer en inner box omdat je hier meteen mee aan de slag gaat.
STAP 3 --- HTML HEADER + INTRO :
<body>
<header id="header" class="outer-content-container">
    <div class="inner-content-container">
        <nav class="header-content__navigation">
            <ul>
                <li><a href="#work">NavLink1</a></li>
                <li><a href="#services">NavLink2</a></li>
                <li><a href="#contact">NavLink3</a></li>
            </ul>
        </nav>

        <div class="header-content__hero default-text-restrictor">
            <h1>Dit is de H1 HEADLINE voor de HEADER</h1>
            <p>Dit is gewoon P text.</p>
            <button type="button">TEXT OP BUTTON 1</button>
        </div>
    </div>
    <div class="skewer--bottom"></div>
</header>
<main>
    <section id="intro" class="outer-content-container">
        <div class="inner-content-container default-area-padding default-text-restrictor">
            <h6>
                A Hier staat H6 text. Deze text is in HTML 3x gebruikt zodat je ruimte tussen de text krijgt.
            </h6>
            <h6>
                B Hier staat H6 text. Deze text is in HTML 3x gebruikt zodat je ruimte tussen de text krijgt.
            </h6>
            <h6>
                C Hier staat H6 text. Deze text is in HTML 3x gebruikt zodat je ruimte tussen de text krijgt.
            </h6>
            <p class="intro__link">Text met link? <a href="/">DIT IS DE LINK</a> Dit is weer text!</p>
        </div>
    </section>
We sluiten de </BODY> nog niet af omdat dit pas het eerste deel van de <BODY> is.

3.1 (eerste deel van <header>) :
<header id="header" class="outer-content-container">
    <div class="inner-content-container">
        <nav class="header-content__navigation">
            <ul>
                <li><a href="#work">NavLink1</a></li>
                <li><a href="#services">NavLink2</a></li>
                <li><a href="#contact">NavLink3</a></li>
            </ul>
        </nav>
We beginnen bij het eerste stuk van de <HEADER> deze geven we de ID="header" en class="outer-content-container". De ID gebruiken we zo in CSS om de GRADIENT en NOISE erop te zetten. Ook doen we de SQUIGGLE LINE erop in CSS. Dat kan ook in HTML, maar ew doen het nu in CSS.
De OUTER-CONTENT-CONTAINER class en de INNER-CONTENT-CONTAINER class zijn heel belangrijk, want dat zijn de FLEX-BOXEN die we over de gehele site gaan gebruiken.
De <NAV></NAV> heeft de class  header-content__navigation gekregen en is ook een FLEX-CONTAINER met de UL daarin ook een FLEX-CONTAINER met de <li> als FLEX-ITEMS.
DUS je hebt
<header class=OUTER-CONTENT-CONTAINER> (FLEX-CONTAINER)
<div class=INNER-CONTENT-CONTAINER(FLEX-ITEM van hierboven FLEX-CONTAINER voor hieronder)
 <nav class=HEADER-CONTENT__NAVIGATION(FLEX-ITEM van hierboven FLEX-CONTAINER voor hieronder)
 <nav class=HEADER-CONTENT__NAVIGATION> ul (FLEX-ITEM van hierboven FLEX-CONTAINER voor hieronder)
<li> (FLEX-ITEM van hierboven)
Dus de OUTER is de Container van de INNER, de INNER is de Container van de NAV, de NAV UL is de Container van de Li. Zie hieronder de VIER(4) flex-containers.


3.2 (tweede deel van <header>) :

        <div class="header-content__hero default-text-restrictor">
            <h1>Dit is de H1 HEADLINE voor de HEADER</h1>
            <p>Dit is gewoon P text.</p>
            <button type="button">TEXT OP BUTTON 1</button>
        </div>
    </div>
    <div class="skewer--bottom"></div>
</header>
Hier hebben we het 2e deel van de <header>, de <div> "header-content__hero heeft een <h1>, een <p> en een <button> als laatste in de <header> staat nog de SKEWER BUTTON waarmee de schuine rand voor dit stuk van de site wordt gemaakt.
 3.3 HEADER SECTION CSS :

De <header> heeft de volgende styles in CSS:

/* --------------- 4.1 Header ------------------------- */

#header {
    background: var(--primary-dark);
    /*Mocht een verouderde browser geen gradients ondersteunen, dan valt de browser terug op de "effen" achtergrondkleur hierboven*/
    background: linear-gradient(129deg, var(--primary-dark) 0%, var(--primary-dark) 26%, var(--primary)  100%);
    color: white;
    padding: 30px 0;
    position: relative;
}

/* Dit is de Squiggle Line op de HEADER */
#header::before {
    content: '';
    display: block;
    width: 78px;
    height: 100px;
    position: absolute;
    bottom: 20px;
    left: calc(50% - 39px);
    background-image: url(./assets/squiggle_line_stripe.svg);
}

/* Dit zorgt dat er een NOISE-Filet over de achtergrond van de HEADER komt */
#header::after {
    content: '';
    display: block;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    opacity: 0.6;
    background-image: url(assets/noise-texture.png);
    background-position: top center;
    background-size: auto;
}

.header-content__navigation {
    display: flex;
    flex-direction: row;
    /*De <ul> die in de <nav> zit, wordt rechts (einde van de rij) uitgelijnd */
    justify-content: center;
    /*De <nav> moet de beschikbare breedte van de pagina aannemen, anders valt er niks uit te lijnen aan de rechterkant */
    width: 100%;
}

.header-content__navigation ul {
    /*Om ervoor te zorgen dat de menu-items op normale afstand van elkaar staan, zorgen we dat de parent: <ul> minimaal 400px breed is*/
    flex-basis: 400px;
    flex-shrink: 1;
    flex-grow: 0;
    list-style-type: none;
    /*Dit flex-item is op haar beurt ook weer een flex-container, die de <li> die erin zitten netjes evenredig verdeelt*/
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

.header-content__navigation a {
    color: white;
    font-size: 16px;
    font-weight: 600;
}

.header-content__hero {
    padding: 100px 0;
    margin-bottom: 88px;
    font-size: 28px;
}

.header__squiggle {
    display: block;
    width: 78px;
    height: 100px;
    margin: 60px 0 0 0;
    position: absolute;
    bottom: 0;
    /*Hiermee zeggen we: plaats 'm horizontaal gezien op 50% van de breedte,
    MAAR wel min de helft van de breedte van de afbeelding zelf (width: 78px) */
    left: calc(50% - 39px);
    background-image: url(./assets/squiggle_line_stripe.svg);
}

3.4 INTRO Section HTML :
 <main>
    <section id="intro" class="outer-content-container">
        <div class="inner-content-container default-area-padding default-text-restrictor">
            <h6>
                A Hier staat H6 text. Deze text is in HTML 3x gebruikt zodat je ruimte tussen de text krijgt.
            </h6>
            <h6>
                B Hier staat H6 text. Deze text is in HTML 3x gebruikt zodat je ruimte tussen de text krijgt.
            </h6>
            <h6>
                C Hier staat H6 text. Deze text is in HTML 3x gebruikt zodat je ruimte tussen de text krijgt.
            </h6>
            <p class="intro__link">Text met link? <a href="/">DIT IS DE LINK</a> Dit is weer text!</p>
        </div>
    </section>
Hier wordt ook de <main> gemaakt, de html heeft <header><main><footer>
Zoals je hierboven kan zien wordt hier ook weer de OUTER en INNER boxen gebruikt.
3.5 INTRO Section CSS :
/* --------------- 4.2 Introduction ------------------- */

#intro {
    background-color: white;
    color: var(--primary);
    position: relative;
}

#intro > div {
    padding: 100px 0;
}

/*Dit zijn de zwevende letters achter de content*/
#intro::before {
    display: block;
    content: 'BACK';
    color: var(--text-faded);
    font-size: 150px;
    opacity: 6;
    font-weight: 600;
    left: 0;
    top: 40px;
    position: absolute;
    text-align: center;
    width: 100%;
    letter-spacing: -10px;
}

.intro__link {
    color: var(--text-dark);
    font-weight: 500;
    margin: 50px 0 0 0;
}

STAP 4 --- WORK SECTION :
4.1 HTML <section id="work"> :
<section id="work" class="outer-content-container">
    <div class="skewer--top"></div>
    <div class="inner-content-container default-area-padding">

        <article class="work-article">
            <span class="work-article__image-wrapper">
                 <img src="./assets/work-image-01.jpeg" alt="Portfolio work"/>
            </span>

            <div class="work-article__info-container">
                <h4>Eerste Titel van Article</h4>
                <p>Dit is de text van de eerste article. De text heeft aparte CSS opmaak omdat de weight wat zwaarder is.</p>
                <a class="work-article__project-link" href="dead-end.html">Article Link 1</a>
            </div>
        </article>
        <article class="work-article">
            <span class="work-article__image-wrapper">
                <img src="./assets/work-image-02.jpeg" alt="Portfolio work"/>
            </span>

            <div class="work-article__info-container">
                <h4>Tweede Titel van Article</h4>
                <p>Dit is de text van de tweede article. De text heeft aparte CSS opmaak omdat de weight wat zwaarder is.</p>
                <a class="work-article__project-link" href="dead-end.html">Article Link 2</a>
            </div>
        </article>
        <article class="work-article">
            <span class="work-article__image-wrapper">
                <img src="./assets/work-image-03.jpeg" alt="Portfolio work"/>
            </span>

            <div class="work-article__info-container">
                <h4>Derde Titel van Article</h4>
                <p>Dit is de text van de derde article. De text heeft aparte CSS opmaak omdat de weight wat zwaarder is.</p>
                <a class="work-article__project-link" href="dead-end.html">Article Link 3</a>
            </div>
        </article>
    </div>

    <div class="skewer--bottom"></div>

</section>
4.2 CSS <section id="work"> :

/* --------------- 4.3 Work --------------------------- */

#work {
    background-color: var(--grey);
    position: relative;
    padding: 0;
}

/*Dit zijn de zwevende letters achter de content*/
#work::before {
    display: block;
    content: 'work';
    color: white;
    font-size: 150px;
    font-weight: 600;
    left: 0;
    top: 80px;
    position: absolute;
    text-align: center;
    width: 100%;
    letter-spacing: -5px;
}

.work-article {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    margin: 0;
}

.work-article__image-wrapper {
    /*De afbeelding-wrapper moet in de basis 800px breed zijn...*/
    flex-basis: auto;
    /*Als er meer ruimte is, mag hij NIET groter worden*/
    flex-grow: 0;
    /*Als er minder ruimte is, krimpt hij 1 fractie (dus alles) van de ingeleverde ruimte*/
    flex-shrink: 1;
}

.work-article__image-wrapper img {
    /*Om afbeeldingen goed mee te laten schalen met de wrapper, zet je de afbeelding zelf altijd op 100% breedte.
    Zo past de afbeelding zich telkens aan, aan zijn omgeving*/
    width: 100%;
    box-shadow: 0 32px 28px -10px rgba(0, 0, 0, 0.22);
}

.work-article__info-container {
    /*De content moet in de basis 480 breed zijn*/
    flex-basis: auto;
    /*Als er meer ruimte is, mag hij NIET groter worden*/
    flex-grow: 0;
    /*Als er minder ruimte is, mag hij NIET kleiner worden*/
    flex-shrink: 0;
    padding: 0 0 50px 0;
}

.work-article__info-container p {
    font-weight: 400;
    margin: 30px 0;
}

.work-article__project-link {
    font-size: 14px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 2px;
}

/*.work-article__title-squiggle {*/
/*    margin-top: 24px;*/
/*    width: 57px;*/
/*    height: 6px;*/
/*    background-image: url(./assets/squiggle_line.svg);*/
/*}
Deze CSS is uiteindelijk niet gebruikt, kijk naar de <h4> styles */

.work-article__project-link::after {
    display: inline-block;
    content: '';
    /*In de basis is het streepje 15 breed, maar dit veranderd bij hover*/
    width: 15px;
    height: 1px;
    background-color: var(--primary);
    margin: 0 0 4px 12px;
    /*Zorg dat de overgang van kort naar lang streepje vloeiend verloopt*/
    transition: all 0.2s ease-in-out;
}

.work-article__project-link:hover::after {
    width: 55px;
}
STAP 5 --- SERVICES SECTION :

5.1 HTML <section id="services"> :

<section id="services" class="outer-content-container">
    <div class="inner-content-container default-area-padding">
        <article class="service-tile">
            <img src="./assets/icon_web-design.svg" alt="icon" class="service-tile__icon"/>
            <h5 class="service-tile__title">Tile 01</h5>
            <p>AAAAA ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                AAAAA ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                 AAAAA ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.</p>
        </article>
        <article class="service-tile">
            <img src="./assets/icon_web-development.svg" alt="icon" class="service-tile__icon"/>
            <h5 class="service-tile__title">Tile 02</h5>
            <p>BBBBB ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                BBBBB ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                 BBBBB ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.</p>
        </article>
        <article class="service-tile">
            <img src="./assets/icon_ux.svg" alt="icon" class="service-tile__icon"/>
            <h5 class="service-tile__title">Tile 03</h5>
            <p>CCCCC ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                CCCCC ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                 CCCCC ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.</p>
        </article>
        <article class="service-tile">
            <img src="./assets/icon_graphic-design.svg" alt="icon" class="service-tile__icon"/>
            <h5 class="service-tile__title">Tile 04</h5>
            <p>DDDDD ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                DDDDD ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                 DDDDD ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.</p>
        </article>
        <article class="service-tile">
            <img src="./assets/icon_seo.svg" alt="icon" class="service-tile__icon"/>
            <h5 class="service-tile__title">Tile 05</h5>
            <p>EEEEE ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                EEEEE ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                 EEEEE ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.</p>
        </article>
        <article class="service-tile">
            <img src="./assets/icon_copywriting.svg" alt="icon" class="service-tile__icon"/>
            <h5 class="service-tile__title">Tile 06</h5>
            <p>FFFFF ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                FFFFF ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.
                 FFFFF ipsum dolor sit amet, consectetur adipisicing elit. Numquam, voluptate.</p>
        </article>
    </div>
</section>

5.1 CSS <section id="services"> :

/* --------------- 4.4 Services------------------------ */

#services {
    background-color: white;
    padding: 50px 0;
    position: relative;
}

/*Dit zijn de zwevende letters achter de content*/
#services::before {
    display: block;
    content: 'services';
    color: var(--text-faded);
    font-size: 100px;
    opacity: 0.6;
    font-weight: 600;
    left: 0;
    top: 70px;
    position: absolute;
    text-align: center;
    width: 100%;
    letter-spacing: -5px;
}

#services > div {
    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
    gap: 40px;
    padding: 100px 0 50px 0;
}
/* Hierboven zijn dus de volledige inhoud van de services op flex-box container gezet op ROW zodat deze door WRAP
   netjes naast elkaar geplaatst worden.
   De TILE in de container is ook weer een flex-box container en deze staat op COLUMN omdat de img--icon title
   en de tekst onder elkaar komen te staan.
 */
.service-tile {
    /*De tegel moet in de basis 480 breed zijn*/
    flex-basis: 384px;
    /*Als er meer ruimte is, mag hij NIET groter worden*/
    flex-grow: 0;
    /*Als er minder ruimte is, krimpt hij 1 fractie (dus alle tegels evenveel) van de ingeleverde ruimte*/
    flex-shrink: 1;
    /*Deze tegel is op haar beurt weer een flexbox-container */
    display: flex;
    flex-direction: column;
    padding: 40px;
    background-color: white;
    border: 1px solid var(--primary);
    box-shadow: 0 11px 16px 0 rgba(0, 0, 0, 0.1);
    color: var(--text);
    font-size: 16px;
}

.service-tile__title {
    color: var(--primary);
    font-size: 24px;
}

.service-tile__icon {
    width: 80px;
}

6.1 HTML <section id="contact"> :
    <section id="contact" class="outer-content-container">
        <div class="skewer--top"></div>

        <div class="inner-content-container default-text-restrictor default-area-padding">
            <h2>Dit is de H2 HEADLINE voor de CONTACT SECTION</h2>
            <p>Nog wat text? Nog Wat Text? NOG WAT TEXT!</p>
            <form class="contact-content__form">
                <label for="name-field">
                    "NAME" Name for="name-field"
                    <input type="text" id="name-field" name="name" placeholder="placeholder Name">
                </label>
                <label for="email-field">
                    "EMAIL" Name for="email-field"
                    <input type="email" id="email-field" name="email" placeholder="placeholder Email">
                </label>
                <label for="message-field">
                    "MESSAGE" Name for="message-field"
                    <textarea name="message" id="message-field" cols="30" rows="10"
                              placeholder="placeholder Message"></textarea>
                </label>
                <button type="submit">TEXT OP BUTTON 2</button>
            </form>
        </div>
    </section>
</main>
Vergeet niet de </main> af te sluiten.

6.2 CSS <section id="contact"> :

/* --------------- 4.5 Contact ------------------------ */

#contact {
    background: var(--primary-dark);
    /*Mocht een verouderde browser geen gradients ondersteunen, dan valt de browser terug op de "effen" achtergrondkleur hierboven*/
    background: linear-gradient(129deg, var(--primary-dark) 0%, var(--primary-dark) 26%, var(--primary)  100%);
    color: white;
    position: relative;
}

#contact > div {
    padding: 100px 0 0 0;
}

#contact::after {
    content: '';
    display: block;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    opacity: 0.6;
    background-image: url(assets/noise-texture.png);
    background-position: top center;
    background-size: auto;
}

.contact-content__form {
    display: flex;
    flex-direction: column;
    text-align: left;
    width: 100%;
}

.contact-content__form input,
.contact-content__form textarea {
    background-color: #ffffff;
    border: 1px solid var(--text);
    border-radius: 4px;
    font-family: 'Roboto', sans-serif;
    padding: 20px;
    display: block;
    font-size: 16px;
    color: var(--text);
    width: 100%;
}

.contact-content__form input::placeholder,
.contact-content__form textarea::placeholder {
    color: var(--text);
}

.contact-content__form label {
    font-size: 16px;
    font-weight: 600;
    padding: 20px 0;
}

.contact-content__form button {
    width: 200px;
    align-self: center;
}

7.1 HTML <section id="footer"> :

<footer id="footer" class="outer-content-container">
    <div class="inner-content-container">
        FOOTER TEXT &copy; footer vak 2022
    </div>
</footer>
</body>
</html>
Je sluit hier dus ook de </body> en de </html> af.

7.2 CSS <section id="footer"> :

/* --------------- 4.6 Footer ------------------------- */

#footer {
    background-color: black;
    color: white;
    text-align: center;
    padding: 20px 0;
    font-size: 14px;
}
8 CSS MEDIA QUERIES :

/* ------------- 5. Media Queries -------------------------------- */


/*Omdat hier maar zo weinig media-queries nodig zijn is er gebruik gemaakt van een max-width query.*/
/*Normaliter maak je altijd gebruik van min-width queries, waarbij de versie voor mobiel buiten de query staat, */
/*en de versie voor desktop juist BUITEN de query*/
@media screen and (min-width: 900px) {
    h1, h2 {
        font-size: 46px;
        padding: 16px 0;
    }

    h3 {
        font-size: 36px;
    }


    h6 {
        font-size: 32px;
        line-height: 1.5;
        padding: 12px 0;
    }

    .header-content__navigation {
        justify-content: flex-end;
    }

    .header-content__navigation a {
        font-size: 16px;
        font-weight: 100;
    }

    #intro::before {
        font-size: 350px;
        letter-spacing: -18px;
        top: 0;
    }

    .intro__link {
        margin-top: 100px;
    }

    #work::before {
        font-size: 350px;
        top: 40px;
        letter-spacing: -18px;
    }

    #work {
        padding: 100px 0 0 0;
    }

    .work-article {
        flex-direction: row;
        margin: 0 0 100px 0;
    }

    .work-article:nth-of-type(odd) {
        flex-direction: row-reverse;
    }

    .work-article__image-wrapper {
        /*om de breedte, die nu geldt als lengte, te overschrijven*/
        flex-basis: 800px;
    }


    .work-article__info-container {
        padding: 0 50px 50px 50px;
        flex-basis: 400px;
    }

        #services {
            padding: 100px 0 0 0;
        }

    #services::before {
        font-size: 230px;
        top: 50px;
    }
}

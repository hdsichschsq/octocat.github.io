# octocat.github.io
title: calculette css 
description: style css
/* 
Balise : 
    Dans ton index.html
        <body>

    Dans ton css 
        body{}

Classe :
    Dans ton index.html
        class="calculator"

    Dans ton css 
        .calculator{}
*/

body {
    font-family: Arial, sans-serif; /* Police de caractères */
    display: flex; /* Modèle de boîte flexible */
    justify-content: center; /* Centrer horizontalement */
    align-items: center; /* Centrer verticalement */
    height: 100vh; /* Hauteur de la page égale à la fenêtre */
    margin: 0; /* Supprimer les marges par défaut */
    background-color: #000; /* Couleur de fond de la page (noir) */
    color: #fff; /* Couleur du texte (blanc) */
}

.calculator {
    width: 400px; /* Largeur de la calculatrice */
    background-color: #444; /* Couleur de fond de la calculatrice */
    border-radius: 5px; /* Coins arrondis */
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); /* Ombre portée */
    padding: 10px; /* Espacement intérieur */
}

.display {
    background-color: #555; /* Couleur de fond de l'affichage */
    color: #fff; /* Couleur du texte de l'affichage */
    padding: 10px; /* Espacement intérieur */
    text-align: right; /* Alignement du texte à droite */
    border-top-left-radius: 5px; /* Coin supérieur gauche arrondi */
    border-top-right-radius: 5px; /* Coin supérieur droit arrondi */
    border-bottom: 1px solid #777; /* Bordure inférieure */
}

.buttons {
    display: grid; /* Modèle de grille pour les boutons */
    grid-template-columns: repeat(5, 1fr); /* 5 colonnes égales */
    grid-gap: 5px; /* Espacement entre les boutons */
}

button {
    border: none; /* Pas de bordure */
    background-color: #777; /* Couleur de fond des boutons */
    color: #fff; /* Couleur du texte des boutons */
    padding: 20px; /* Espacement intérieur */
    cursor: pointer; /* Curseur pointeur */
    font-size: 20px; /* Taille de police */
}

button:hover { /* :hover = au survol */
    background-color: #999; /* Couleur de fond des boutons au survol */
}
title: calculette html 
description: html 
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8"> <!-- correction de la balise charset -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>calculatrice</title>
    <link rel="stylesheet" href="style.css"> <!-- Lien vers la feuille de style CSS -->
</head>
<body><!--code-->
    <div class="calculator">
        <div class="display" id="display">0</div> <!-- Affichage de la calculatrice -->
        <div class="buttons">
            
            <!-- Ligne 1 des boutons -->
            <button onclick="appendToDisplay('1')">1</button>
            <button onclick="appendToDisplay('2')">2</button>
            <button onclick="appendToDisplay('3')">3</button>
            <button onclick="clearDisplay()">C</button> <!-- Bouton pour effacer l'affichage -->
            <button onclick="backspace()">Delete</button> <!-- Bouton pour effacer un chiffre -->

            <!-- Ligne 2 des boutons -->
            <button onclick="appendToDisplay('4')">4</button>
            <button onclick="appendToDisplay('5')">5</button>
            <button onclick="appendToDisplay('6')">6</button>
            <button onclick="appendToDisplay('-')">-</button>
            <button onclick="appendToDisplay('+')">+</button>

            <!-- Ligne 3 des boutons -->
            <button onclick="appendToDisplay('7')">7</button>
            <button onclick="appendToDisplay('8')">8</button>
            <button onclick="appendToDisplay('9')">9</button>
            <button onclick="appendToDisplay('/')">/</button>
            <button onclick="appendToDisplay('*')">*</button>

            <!-- Ligne 4 des boutons -->
            <button onclick="appendToDisplay('.')">.</button>
            <button onclick="appendToDisplay('0')">0</button>
            <button onclick="appendToDisplay('(')">(</button>
            <button onclick="appendToDisplay(')')">)</button>
            <button onclick="calculate()">=</button> <!-- Bouton pour effectuer le calcul -->
        </div>
    </div>
    <script src="script.js"></script> <!-- Lien vers le fichier JavaScript -->
</body>
</html>
title: calculette java script 
description: java 
et display = document.getElementById('display'); // Selectionne l'element d'affichage
let resultDisplayed = false; // Variable pour suivre l'affichage du resultat

// Fonction pour ajouter du texte a l'affichage
function appendToDisplay(value) {
    // Si le resultat est affiche et l'utilisateur commence a entrer de nouveaux chiffres,
    // efface le resultat et met a jour la variable resultDisplayed
    if (resultDisplayed) {
        clearDisplay();
        resultDisplayed = false; // Variable pour suivre l'affichage du résultat
    }

    // Si le texte actuel est "0" et la valeur ajoutée est un chiffre,
    // remplace "0" par la nouvelle valeur
    if (display.innerText === '0' && !isNaN(parseInt(value))) {
        display.innerText = value;
    } else {
        display.innerText += value; // ajoute la valeur au texte existant
    }
}

// Fonction pour effacer un chiffre de l'affichage
function backspace() {
    let currentValue = display.innerText;
    // vérifie si la valeur actuelle n' est pas vide avant de couper
    if (currentValue.length > 0) {
    display.innerText = currentValue.slice(0, -1); // supprime le dernier caractère du texte
    }
}    

// Fonction pour effacer l'affichage
function clearDisplay() {
    display.innerText = '0'; // efface le texte de l'affichage
}

// Fonction pour effectuer le calcul
function calculate() {
    try {
        let result = eval(display.innerText); // Évalue le texte de l'affichage 
        display.innerText = result; // Affiche le résultat
        resultDisplayed = true; // Met à jour la variable pour indiquer que le résultat est affiché
    } catch (error) {
        display.innerText = 'Error'; // Affiche "Error" en cas d'erreur de calcul
        resultDisplayed = true; // Met à jour la variable pour indiquer que le résultat est affiché 
    }
}

// Ajoute un écouteur d'événements pour la saisie au clavier
document.addEventListener('keypress', handleKeyPress);

// fonction pour gérer la saisie au clavier
function handlekeyPress(event) {
    const key = event.key;
    if (!isNaN(event.key) || ['+','-','*','/','(',')','.'].includes(key)) {
        apprendToDisplay(key);
    } else if (key === 'enter') {
        calculate();
    } else if (key === 'Backspace'){
        backspace ();
    }
}                   

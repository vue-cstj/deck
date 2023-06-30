# Deck-vue

## Procédure d'installation

1. Créer le dossier de travail
2. Ouvrir le dossier dans VSCode
3. Ouvrir le terminal
4. Exécuter la commande 
	```bash
	npm init vite@next .
	```
   > Ne pas oublier le point à la fin de la commande. Il indique que le projet sera créé dans le dossier courant. S'il est omis, un nouveau dossier sera créé avec le nom du projet.
5. Répondre aux questions posées par la commande
   1. Ne répondre **yes** qu'à la question demandant l'utilisation du `router`.
   2. Pour les autres questions, répondre **no**.
6. Exécuter la commande
	```bash
	npm install
	```	
1. Installer le module `sass` qui permet de compiler les fichiers scss directement. Exécuter la commande :
	```bash
	npm install -D sass
	```
2. Installer le module `axios` qui permet de faire des requêtes HTTP. Exécuter la commande :
	```bash
	npm install axios
	```
3. Voilà, le projet est prêt à être utilisé. Pour le tester, exécuter la commande
	```bash
	npm run dev
	```
4. Ouvrir un navigateur et aller à l'adresse indiquée. Ex.: [http://localhost:5173](http://localhost:5173)

## Remise à zéro du projet

L'installateur de Vite crée un projet avec des fichiers de démonstration. Nous devons les adapter ou les supprimer.

| Fichier | Explication | Action |
|---------|-------------|--------|
| `index.html` | Page d'accueil du projet | Adapter le titre et le contenu de la balise `<title>`; Ajouter un favicon; Lier une feuille de styles |
| `src/main.js` | Point d'entrée de l'application | Supprimer (ou adapter) le `import` de la feuille de styles |
| `src/App.vue` | Composant principal de l'application | Supprimer le `import` de `HelloWorld`; Adapter selon le design voulu. Le seul élément qui **doit** rester est le `<RouterView />` où le contenu sera généré; Supprimer la balise `<style>`, car nous allons utiliser une feuille de styles externe |
| `src/router/index.js` | Fichier de configuration du `router` | Supprimer le `import` de `Home`; Importer la vue 'Index' : `import IndexView from '../views/Index.vue';`; Ajouter une route vers la page d'accueil : `{ path: '/', name: 'accueil', component: IndexView },`; Supprimer les routes `Home` et `About`. |
| `src/views` | Dossier contenant les "_pages_" de notre application | Supprimer tout le contenu; Créer une fichier `Index.vue`. |
| `src/components` | Dossier contenant les "_composants_" de notre application | Supprimer tout le contenu; Créer un fichier `Nav.vue` |
| `src/assets` | Dossier contenant les "_assets_" de notre application | Supprimer tout le contenu; Créer un dossier `scss` et un fichier `style.scss`; Créer un dossier `img` |

## Les fichiers `.vue`
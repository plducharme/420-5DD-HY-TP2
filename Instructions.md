# Instructions pour démarer le projet du TP

## Création d'un projet Phoenix

Super important : **le projet ne doit pas s'appeler `chat`, mais doit porter votre nom d'équipe.**

Commencez par générer une base de projet nommé avec votre nom d'équipe avec la commande [Phoenix new](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.New.html) sans base de données.

	mix phx.new votrenomdequipe --live --no-ecto


suivre les instructions à l'écran pour changer de répertoire et compiler/exécuter le serveur.

Vous devriez maintenant être en mesure d'ouvrir la page web de votre application sur http://localhost:4000/

La page d'accueil de Phoenix devrait apparaitre

Vous pouvez arrêter ce serveur (CTRL-C), on est rendu à configurer l'environnement de développement.

## Configuration de VS Code pour pouvoir lancer l'application en mode débogage

Ouvrir le **dossier de projet** avec VSCode (attention, c'est vraiment juste le dossier qu'il faut ouvrir!)

Créez un espace de travail via le menu `Fichier` > `Enregistrer l'espace de travail sous...`

Dans Windows, vous devriez voir le fichier *votrenomdequipe*.code-workspace dans le même dossier que mix.exs

Vous pouvez dorénavant **ouvrir le projet avec ce nouveau fichier .workspace**.

Si ce n'est déjà fait, installez l'extension pour Elixir "JakeBecker.elixir-ls"

Dans le panneau **Exécuter et déboguer** (icone en triangle avec une bestiole), cliquez sur `Créer un ficher launch.json` sélectionnez ensuite le nom du projet, puis choisissez **Projet Mix**.

Modifiez le fichier généré pour y inclure le bloc suivant dans la section Configurations :

	{
		"type": "mix_task",
		"name": "mix (Phoenix)",
		"request": "launch",
		"task": "phx.server",
		"projectDir": "${workspaceRoot}"
	},
	
Dans le panneau **Exécuter et déboguer**, sélectionnez `mix (Phoenix)` dans le menu, puis cliquez sur le triangle

Vous pouvez ensuite lancer un browser (Edge ou autre) avec l'adresse http://localhost:4000/

La page d'accueil de Phoenix devrait apparaitre

## Video de référence pour les instruction détaillées


[Let’s Build a Real Time Chat Application with Elixir and Phoenix](https://youtu.be/fyg0FuSL5DY?t=243)


Livre de l'auteur (accès gratuit vua BAnQ) 

[![Elixir in action](https://cap.banq.qc.ca/in/rest/Thumb/image?id=p%3A%3Ausmarcdef_0006309492&isbn=9781617295041&author=Lessel%2C+Geoffrey.+auteur&title=Phoenix+in+action&year=2019&TypeOfDocument=Physical&mat=EBOOK&ct=true&size=256&isPhysical=1)](https://cap.banq.qc.ca/notice?id=p%3A%3Ausmarcdef_0006309492&locale=fr)

## Fichiers à modifier


- root.html.heex : cadre de page pour l'application
- index.html.heex : le code html qui sera utilisé pour l'application
- mix.exs : La configuration de build et exécution du projet
- router.ex : Aiguillage des requêtes web

## Fichiers sont à créer

Attention, la nouvelle version de Phoenix impacte les contrôleurs : les fichiers .leex sont maintenant des fichiers .heex qui doivent être à côté des fichiers .ex correspondants.

	├───controllers
	│       page_controller.ex
	│       page_live.ex
	│       page_live.html.heex
	│       room_live.ex
	│       room_live.html.heex


De plus, les feuilles de styles sont dans un .css au lieu d'un .scss

## À surveiller

* Les formulaires ont évolué dans la nouvelle version de Phoenix : 
	- voir https://hexdocs.pm/phoenix_html/Phoenix.HTML.Form.html
	- et https://hexdocs.pm/phoenix_live_view/form-bindings.html

Utilisez la forme suivante au lieu de celle dans le vidéo :

	<%= form_for :chat, "#", [phx_submit: :submit_message],fn f -> %>
	
	
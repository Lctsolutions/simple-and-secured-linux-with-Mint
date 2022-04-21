English version [below](#a-pretty-secure-and-usuable-Linux-distribution) !

<br />

# Une distribution Linux sécurisée et simple
Au travers de ce dépôt je documente comment j'ai installé, personnalisé et sécurisé mon installation de Linux Mint XFCE. J'ai essayé d'obtenir un résultat avec des interfaces utilisateurs au maximum cohérentes, un système pratique et facile à maintenir tout en ayant une bonne sécurité.

Au cours de mes recherches j'ai dû faire certains compromis après divers tests ; je partage donc ici ma configuration personnalisée qui ne vous conviendra peut-être pas. En fonction des pistes que j'ai creusé j'essaye de fournir des alternatives à mes décisions finales afin que vous puissiez faire vos propres choix.

# Installation de Linux Mint 21 édition XFCE
## Choisir la version
:warning: Ici je détaille à date la version que j'ai installée ; depuis d'autres versions sont sans doute sorties ! Je vous conseille de toujours vous référer à la [documentation officielle](https://linuxmint-installation-guide.readthedocs.io/fr/latest/) de la version que vous installez afin de bénificier de l'aide la plus à jour.

:warning: Dès cette phase un choix "important" est effectué : celui de l'environnement graphique. En effet [XFCE](https://xfce.org/?lang=fr) n'est pas [Mate](https://mate-desktop.org/fr/), ni Cinnamon créé par les développeurs de Mint.

La documentation officielle propose un [comparatif rapide](https://linuxmint-installation-guide.readthedocs.io/fr/latest/choose.html) de ces environnements. Si ces environnements ne vous conviennent pas, sachez qu'il en existe d'autres comme :
- [Gnome](https://www.gnome.org/)
- [KDE](https://kde.org/fr/)
- [Enlightment](https://www.enlightenment.org/)
- ...

Il vous faudra alors vous diriger vers d'autres systèmes d'exploitation si c'est le cas, sauf si vous vous sentez suffisament confiant pour installer un environnement non supporté (ce qui est possible comme indiqué [ici](https://linoxide.com/install-gnome-on-linux-mint/) ; attention je pense que cela peut poser problème en fonction des mises à jour !)

## Installation du système
L'installation de Linux Mint est assez facile ; la création du support USB d'installation est détaillé [ici](https://linuxmint-installation-guide.readthedocs.io/fr/latest/burn.html) si nécessaire. Pour ma part j'ai suivi l'installateur graphique sans personnalisation exceptionnelle.
J'ai choisi de chiffrer l'ensemble du disque système (ayant un disque pleinement disponible), attention aux manipulations lors de la phase de partitionnement si vous souhaitez effectuer un dual-boot Windows par exemple. La documentation [officielle](https://linuxmint-installation-guide.readthedocs.io/fr/latest/install.html) contient de bonnes bases mais si vous n'êtes pas sûr n'hésitez pas à faire des recherches complémentaires sur le sujet.

Le chiffrement complet du système protège votre machine d'un accès à vos fichiers dans le cas d'un vol de portable par exemple ; en effet lors du démarrage un mot de passe est requis et sans celui-ci il est impossible de consulter le contenu du disque même via un live boot. :warning: Cette mécanique n'est en aucun cas une protection contre les malwares ! Une fois le déchiffrement effectué et la phase de boot passée, les fichiers sont accessibles de manière classique donc si la machine est compromise cela ne change rien.

D'après mon expérience l'indication concernant l'agencement du clavier lors de la saisie du mot de passe de chiffrement n'est plus d'actualité (au moins sur Linux Mint 20.1 "Ulyssa"). En effet ce choix d'agencement est désormais en amont dans la phase de partionnement et lors de la saisie au démarrage du système l'agencement du clavier est bien celui choisi (Français (azerty) pour ma part).

## Configuration post-installation
A la première ouverture de session, une fenêtre s'ouvre pour suggérer plusieurs personnalisations à effectuer. Voici ce qui m'a paru prioritaire :
1. Activer le pare-feu
2. Paramétrer les mises à jour et sources de logiciels
3. Choisir le bon pilote de carte graphique
4. Et enfin régler la mise en veille et extinction de l'écran

<br />
TODO: reporter et reformuler le dépôt privé pour ajouter les différentes sections ici au fur et à mesure


<br />
<br />

# A pretty secure and usuable Linux distribution
Through this repository I detail how I installed, personalized and secured my installation of Linux Mint XFCE. I looked for user interface consistency, a system easily maintainable and convenient with security in mind.

During my research I had to make some choices after testing an option or software ; here I share my own configuration which probably won't be a perfect match for you. That is why I propose multiple alternative so that you can choose the best option according to your usage.

<br />
TODO: complete english version when documentation is stable
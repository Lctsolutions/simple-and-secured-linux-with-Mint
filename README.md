English version [below](#a-pretty-secure-and-usable-linux-distribution) !

*My english is not perfect at all.. If you see errors please be kind and report it to me* :wink:

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
1. Activer le [pare-feu](#pare-feu-par-défaut)
2. Paramétrer les [mises à jour et sources de logiciels](#mises-à-jour-et-sources-de-logiciels)
3. Choisir le bon [pilote de carte graphique](#pilote-de-la-carte-graphique)
4. Et enfin [régler la mise en veille et extinction](#gestion-de-la-mise-en-veille) de l'écran

Pour les autres sujets (personnalisation, sécurisation, ...), je m'y suis attaqué en fonction de mon temps libre et de mes envies. Vous pouvez retrouver ces catégories via la table des matières générée par GitHub.

### Pare-feu par défaut
Le pare-feu fourni par défaut avec Linux Mint est [ufw](https://help.ubuntu.com/community/UFW) avec son interface graphique [Gufw](https://help.ubuntu.com/community/Gufw). Comme son nom l'indique, ufw (Uncomplicated Firewall) est fait pour être simple d'usage. La simple activation de ce pare-feu répond aux besoins de l'utilisateur moyen hors entreprise. Pour l'activer il faut se rendre dans le menu `Paramètres` > `Configuration du pare-feu` ; ce réglage étant réservé aux utilisateurs habilités, il faut donc saisir son mot de passe.

Personnellement je choisi la configuration la plus basique possible comme je compte compléter le pare-feu avec d'autres solutions pour protéger mon poste. N'utilisant pas de service particulier (avec écoute sur port externe notamment), le refus des connexions entrantes et l'autorisation des connexions sortantes me convient tout à fait (:warning: cela peut représenter un risque de sécurité comme une application compromise pourrait dialoguer vers l'extérieur sans limitation). Il ne faut pas oublier de faire glisser la coche pour activer ufw.

![Copie d'écran de Gufw](./assets/images/copie_ecran_gufw_01.png)

En alternative pour ceux souhaitant un filtrage plus fin que par protocole/port, il existe des pare-feu applicatifs comme [Douane](https://gitlab.com/douaneapp/Douane). Cette solution permet de gérer les autorisations de chaque application ayant besoin de communiquer sur le réseau ; ainsi une popup est générée à chaque nouvelle application non connue et l'utilisateur peut choisir de poursuivre le blocage ou autoriser l'application, et ce temporairement ou non. L'installation sur Linux Mint se fait via [Douane installer](https://gitlab.com/douaneapp/douane-installer).

### Mises à jour et sources de logiciels
Concernant la gestion des mises à jour, j'ai validé la recherche automatique lors de l'invitation à la première connexion. On peut vérifier que l'actualisation automatique est bien activée et avec quelle périodicité en passant par le menu `Système` > `Gestionnaire de mises à jour` puis dans la fenêtre `Édition` > `Préférences` et enfin onglet `Options`.

![Copie d'écran des mises à jour automatique](./assets/images/copie_ecran_maj_01.png)

Au niveau des sources de logiciels j'ai également configuré les miroirs afin d'utiliser ceux les plus performants selon ma localisation. On accède à ces réglages par le menu `Système` > `Sources de logiciels` (ce qui nécessite les droits administrateur). En cliquant dans la liste déroulante pour le miroir `Principal (ulyssa)` ou `Base (focal)`, la vitesse de téléchargement depuis chaque miroir s'affiche ce qui permet de sélectionner les plus appropriés.

![Copie d'écran des sources de logiciels](./assets/images/copie_ecran_sources_log_01.png)

### Pilote de la carte graphique
J'ai une carte graphique Nvidia dont la gestion peut-être compliquée selon les drivers disponibles sur les différentes distributions GNU/Linux. Le driver Nouveau m'a notamment posé plusieurs soucis précédemment, et malgré que je préfère utiliser des logiciels open-source et/ou libres, dans ce cas j'installe désormais le pilote propriétaire.

Pour ce faire il faut se rendre dans le menu `Système` > `Gestionnaire de pilotes` et il n'y a plus qu'à cocher le pilote propriétaire recommandé. L'application de ce choix prend quelques minutes le temps de faire le téléchargement et l'installation.

![Copie d'écran des pilotes](./assets/images/copie_ecran_pilotes_01.png)

### Gestion de la mise en veille
L'un des paramétrages que j'effectue en premier sur un nouveau système est la gestion de l'extinction de l'écran et de la mise en veille. Je déteste retrouver mon PC éteint alors que j'avais lancé un téléchargement, script, etc. Personnellement je n’aime pas avoir de mise en veille automatique, cependant je veux éteindre l’écran au bout de 5 minutes d’absence (avec verrouillage de la session). Sur Linux Mint c'est assez facile, il faut cliquer sur l’icône d'un éclair dans la barre de menu puis choisir `Paramètre du gestionnaire d'alimentation`. Au niveau de l'onglet `Général` de la fenêtre qui s'ouvre, je sélectionne `Ne rien faire` pour chaque option afin qu'aucun bouton ne déclenche la mise en veille. Dans l'onglet `Écran` j'active la gestion de l'alimentation de celui-ci, et je choisi d'éteindre l'écran après 5 minutes d'inactivité (ce qui correspond à l'option `Écran vide après`) ; je règle à `Jamais` pour le reste. Enfin dans l'onglet `Sécurité` j'active le verrouillage automatique de l'écran quand l'économiseur d'écran se déclenche, avec 1 seconde de différé.

## Sécurisation du système
### Bac à sable d'application
#### Introduction à la notion de bac à sable
Un bac à sable permet de ne fournir à une application que ce dont elle a besoin pour fonctionner, sans pouvoir accéder à toutes les fonctions du système d'exploitation ce qui limite le risque de failles de sécurité. A titre d'illustration il est ainsi possible de :
- cloisonner l'accès aux documents de l'utilisateur (`/home/[utilisateur]/Documents`)
- masquer le contenu réel de certains dossier comme `/dev`, `/proc`, ... (CF cette [documentation](https://linuxhandbook.com/linux-directory-structure/) pour le détail de l'arborescence Linux)
- empêcher l'accès au réseau à une application qui n'en a pas besoin
- si l'application doit accéder au réseau, lui créer une nouvelle pile réseau propre afin de l'empêcher de voir les autres communications
- donner une vue virtuelle du kernel partagé
- ...

Voici deux solutions de type bac à sable très connues et recommandées notamment par l'ANSSI dans le guide de [configuration GNU/Linux](https://www.ssi.gouv.fr/uploads/2016/01/linux_configuration-fr-v1.2.pdf) :
- [AppArmor](https://gitlab.com/apparmor/apparmor/-/wikis/GettingStarted)
- [SELinux](https://selinuxproject.org/page/Main_Page)

Cependant bien que je sois relativement attentif à la sécurité, ces solutions me paraissent "overkill" (dans le sens trop complexe à mettre en place et trop limitant au regard de mon [modèle de menace](https://fr.wikipedia.org/wiki/Mod%C3%A8le_de_menace)) pour un usage domestique.

#### Firejail
Lors d'un essai de Manjaro, j'ai découvert [Firejail](https://firejail.wordpress.com/) qui est recommandé dans le [wiki sécurité](https://wiki.manjaro.org/index.php/Linux_Security#Sandboxing) de la distribution. Il s'agit depuis de la solution de bac à sable que j'utilise au quotidien. Son utilisation est très simple puisque de nombreux profils d'application existent, et hormis une application en particulier (VSCodium) je n'ai jamais rencontré de soucis avec. Il existe d'ailleurs un petit [guide pour Linux Mint](https://firejail.wordpress.com/2017/05/15/linux-mint-sandboxing-guide/) permettant de mieux appréhender son fonctionnement et sa simplicité pour l'utilisateur.

Pour le mettre en oeuvre il suffit d'installer les paquets suivants (via la logithèque en mode graphique ou le terminal avec `sudo apt install [nom du paquet]`) :

| Paquet | Objet |
| --- | --- |
| Firejail | Le bac à sable en lui-même |
| firejail-profiles | Des profils supplémentaires à ceux de base pour une prise en charge de plus d'application par défaut |
| Firetools | L'interface graphique de Firejail pour voir les bacs à sable, lancer une application, ... |

Point d'attention lors de l'installation d'une nouvelle application, afin que celle-ci soit prise en compte par Firejail (si un profil correspondant existe), il faut exécuter la commande `sudo firecfg`. Si aucun profil n'existe, on peut lancer l'application depuis l'interface Firetools après avoir défini les contraintes :

![Copie d'écran configuration Firejail](./assets/images/copie_ecran_firetools_01.png)

Ou bien rédiger un profil spécifique dans `~/.config/firejail/` à l'aide de la [documentation dédiée](https://firejail.wordpress.com/documentation-2/building-custom-profiles/).

Comme indiqué précédemment la prise en compte d'une nouvelle application est manuelle ; il est possible d'automatiser cela grâce à un crochet post-installation dont le but sera d'exécuter la commande `sudo firecfg` après chaque nouvelle installation. Voici comment procéder ([source](https://www.cyberciti.biz/faq/debian-ubuntu-linux-hook-a-script-command-to-apt-get-upgrade-command/)) :
1. Créer un fichier dans `/etc/apt/apt.conf.d/` (intitulé "100install" pour ma part)
2. Dans ce fichier mettre le contenu suivant :
```bash
# Script personnalisé pour exécuter des commandes après l'invocation de dpkg ou apt
DPkg::Post-Invoke {"/usr/bin/firecfg";};
```

Après une installation on constate bien que le fichier créé est pris en compte par `apt` :

![Copie d'écran d'une installation avec crochet personnalisé](./assets/images/copie_ecran_firejail_post_invoke_01.png)

:warning: Avec la mise en place de ce crochet, l'installation au travers du Gestionnaire de mises à jour (en mode graphique donc) semble ne plus fonctionner. Cependant comme j'utilise plutôt la ligne de commande je n'ai pas cherché de solution à ce problème.

### Chargeur d'amorçage
#### Introduction à la notion de chargeur d'amorçage
Le chargeur d'amorçage (bootloader) est le deuxième programme lancé au démarrage d'une machine après le BIOS/UEFI. Son rôle est de charger la mémoire (RAM) avec le nécessaire pour que le système d'exploitation s'exécute. Pour en savoir plus sur le démarrage d'un ordinateur, rendez-vous [ici](https://www.ionos.com/digitalguide/server/configuration/what-is-a-bootloader/) et [là](https://fr.wikipedia.org/wiki/Chargeur_d%27amor%C3%A7age).

Ce chargeur est donc un composant critique puisqu'il contient de quoi lancer le système. Par défaut sur la plupart des distributions GNU/Linux il s'agit de [Grub 2](https://www.gnu.org/software/grub/) qui ne contient aucune protection particulière sans configuration. Ainsi l'accès aux options du démarrage système est possible sans aucune identification, ce qui peut représenter un risque. En effet il y a une [technique bien connue](https://itigic.com/change-or-remove-root-password-in-linux-using-grub/) permettant de changer le mot de passe du super utilisateur (root) via Grub en modifiant le démarrage du système pour obtenir un terminal avec tous les droits. Un autre exemple de risque possible est le chargement du système sur une version précédente du [noyau](https://fr.wikipedia.org/wiki/Noyau_de_syst%C3%A8me_d%27exploitation) (kernel), dont l'attaquant sait qu'elle contient une vulnérabilité intéressante dans le cas où le disque système est chiffré (ce qui empêche l'utilisation de la technique précédente).

#### Protéger l'accès à Grub par un mot de passe
Voici comment sécuriser Grub 2 avec une [empreinte](https://fr.wikipedia.org/wiki/Fonction_de_hachage) de mot de passe dans le fichier de configuration ([source](https://help.ubuntu.com/community/Grub2/Passwords)) :

1. Définir un mot de passe et générer son empreinte grâce à la commande `grub-mkpasswd-pbkdf2` :
```console
~$ grub-mkpasswd-pbkdf2
Entrez le mot de passe : 
Entrez de nouveau le mot de passe : 
Le hachage PBKDF2 du mot de passe est grub.pbkdf2.sha512.10000.83F3E4D0822F10E1FB2BE3532F77235EE833524D681BA4FF7ABBBD2A13F9789FFC99F0229A54083D4ECCE934BEDFEC1CEA1113F1AA166686AFB5281C58577A7B.EBE7A53F7C1D244199E3457968C1ED27E976D5818CE07CFC7FDC7EFA75814115AE194D44E53C5B4BB61624A2FCCBC7C7803582CFDD7537AA28C823A5066A1101
```
2. Éditer le fichier `40_custom` dans `/etc/grub.d/` afin d'ajouter le contenu suivant à la fin :
```bash
# Définit un utilisateur. Le nom n'a aucune importance et n'a pas besoin de correspondre à un utilisateur du système d'exploitation.
set superusers="utilisateur"
# Définit le mot de passe associé. Il s'agit de l'empreinte PBKDF2 du mot de passe plutôt que de l'inscrire en clair, ce qui est une bonne pratique surtout si le disque système n'est pas chiffré.
password_pbkdf2 utilisateur grub.pbkdf2.sha512.10000.83F3E4D0822F10E1FB2BE3532F77235EE833524D681BA4FF7ABBBD2A13F9789FFC99F0229A54083D4ECCE934BEDFEC1CEA1113F1AA166686AFB5281C58577A7B.EBE7A53F7C1D244199E3457968C1ED27E976D5818CE07CFC7FDC7EFA75814115AE194D44E53C5B4BB61624A2FCCBC7C7803582CFDD7537AA28C823A5066A1101
```
3. Exécuter la commande `sudo update-grub` afin de regénérer le chargeur d'amorçage avec la nouvelle configuration.

Au prochain démarrage du système, l'accès à chaque entrée du menu Grub nécessitera de saisir l'utilisateur et le mot de passe définit plus haut.
:warning: Le clavier peut-être configuré en QWERTY à cette étape ! Profitez de la saisie de l'utilisateur qui se fait en clair pour vérifier ce point.

#### Complément : rendre libre une entrée Grub 2
Comme indiqué précédemment avec la définition d'un mot de passe sans ajustement particulier, la moindre entrée nécessite de s'authentifier. Ayant chiffré mon disque système cela veut dire que je dois saisir deux mots de passe avant que celui-ci ne démarre, ce qui n'est pas très pratique.

Voici comment rendre l'entrée correspondant à Linux Mint libre (unrestricted) afin que celle-ci ne requiert aucune authentification :

1. Éditer le fichier `10_linux` dans `/etc/grub.d/` afin de modifier la ligne suivante :
```bash
# Ajouter l'option unrestricted devant la classe
echo "menuentry '$(echo "$os" | grub_quote)' --unrestricted ${CLASS} \$menuentry_id_option 'gnulinux-simple-$boot_device_id' {" | sed "s/^/$submenu_indentation/"
```
2. Exécuter la commande `sudo update-grub` afin de régénérer le chargeur d'amorçage avec la nouvelle configuration.

Au prochain démarrage du système, toutes les entrées sauf celle du système courant nécessiteront une authentification. Cette méthode permet de ne pas éditer le fichier `grub.cfg` après chaque mise à jour du noyau :thumbsup: ([source](https://askubuntu.com/questions/1088215/grub-2-avoid-unrestricted-boot-options-are-overwritten-with-kernel-updates)).

<br />
<br />
TODO: reporter et reformuler le dépôt privé pour ajouter les différentes sections ici au fur et à mesure


<br />
<br />

# A pretty secure and usable Linux distribution
Through this repository I detail how I installed, personalized and secured my installation of Linux Mint XFCE. I looked for user interface consistency, a system easily maintainable and convenient with security in mind.

During my research I had to make some choices after testing an option or software ; here I share my own configuration which probably won't be a perfect match for you. That is why I propose multiple alternatives so that you can choose the best option according to your usage.

# Linux Mint 21 XFCE installation detailed
## Choosing the edition
:warning: Here I explain which version I installed at the time ; some newer versions are surely available now ! Always check the [official documentation](https://linuxmint-installation-guide.readthedocs.io/en/latest/) of the version you are installing to be sure to not get into errors.

:warning: From this step an important choice is made : the desktop environment. [XFCE](https://xfce.org/?lang=en) is not like [MATE](https://mate-desktop.org/) nor Cinnamon created by Mint developers.
The official documentation [compares](https://linuxmint-installation-guide.readthedocs.io/en/latest/choose.html) these environments. If none is suitable for you, you should know it exists plenty of others as :
- [Gnome](https://www.gnome.org/)
- [KDE](https://kde.org/)
- [Enlightment](https://www.enlightenment.org/)
- ...

If one of these environments fits you more, it would be better choosing an other operating system. It is technically possible the install a desktop environnement like Gnome in Mint as detailed [here](https://linoxide.com/install-gnome-on-linux-mint/) ; but I think it is not recommended for new users of Linux.

## Installing the OS
The installation process is quite simple in Linux Mint ; if you need to create a bootable USB first, see [here](https://linuxmint-installation-guide.readthedocs.io/en/latest/burn.html). I followed the steps in the graphical installer without taking exotic options. I choose to encrypt the whole disk (having one entirely free aka without an other OS), take care during the partioning steps as you could messed up with Windows if you are dual-booting. The [official documentation](https://linuxmint-installation-guide.readthedocs.io/fr/latest/install.html) presents some cases but if you are unsure do not hesitate to seek more information.

Disk encryption protects the computer against physical access like a theft of laptop for exemple. Actually during the boot it is needed to provide the password, without it it is impossible to read anything on the disk even with a live boot. :warning: Disk encryption is not a protection from malware ! In fact when the decryption process and boot are done, all files are free to use for the system ; if it is compromised then the data can be read/used by a malicious program.

From my experience, the hint about the keyboard layout for encryption password is not true anymore (as of Linux Mint 20.1 "Ulyssa"). Indeed the layout is choosen in the upstream part of installation.

## Post-installation
When the installation is completed a window opens shortly after login and suggests a few things to do. This is what I have done in priority :
1. Set the firewall
2. Choose sources of updates
3. Get the right graphic card driver
4. Finally configure hibernation and screen saver

For the rest (personalisation, security, ...) I take care of it according to the time I got at the moment and my desires. See the table of contents generated by Github.

### Default firewall
The default firewall pre-installed in Linux Mint is [ufw](https://help.ubuntu.com/community/UFW) along with its GUI [Gufw](https://help.ubuntu.com/community/Gufw). ufw (Uncomplicated Firewall) as its name indicate is easy to use ; the basic configuration will be convenient enough for most home users. To configure it you will need to authenticate to get administration rights.

In my case I don't use specific rules as I will use other solutions in combination to harden my PC. As I don't need to SSH into this PC I select to block incoming connections and allow everything outgoing (:warning: this might be a security risk as a compromised application could use networking without limitation). Don't forget to activate ufw with the toggle switch.

![Gufw screenshot in french sorry](./assets/images/copie_ecran_gufw_01.png)

Alternatively for power users wanting to not only allow/deny based on protocols/ports, some firewalls can filter application connections like [Douane](https://gitlab.com/douaneapp/Douane). This firewall generates popup when a new app uses the network, then the user must choose to allow/deny it, temporarily or not. To install it on Linux Mint, see [Douane installer](https://gitlab.com/douaneapp/douane-installer).

<br />
<br />
TODO: complete english version when documentation is stable (with screenshots in english :smile:)
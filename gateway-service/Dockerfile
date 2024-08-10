# Utilise l'image officielle d'OpenJDK 17 basé sur Debian.
# Oracle JDK n'a pas une version alpine disponible.
FROM openjdk:17-oracle

# Déclare un point de montage de volume pour le répertoire /tmp.
# Cela permet de partager ce répertoire entre le conteneur et l'hôte.
VOLUME /tmp

# Copie tous les fichiers JAR de target (qui est le dossier de sortie par défaut pour Maven)
# dans l'image Docker sous le nom app.jar.
# Assurez-vous que votre application Java est compilée avant cette étape.
COPY target/*.jar app.jar

# Spécifie la commande à exécuter lorsque le conteneur démarre.
# Ici, il s'agit d'exécuter l'application Java en utilisant la commande 'java -jar'.
ENTRYPOINT ["java", "-jar", "app.jar"]

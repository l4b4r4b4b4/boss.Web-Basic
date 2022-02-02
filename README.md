# boss.Web-Wordpress
## Quickstart

1. Wirdpress Anwendungsmuster von Git-Repository auf Server kopieren

```
git clone https://github.com/l4b4r4b4b4/boss.Web-Basic.git
```

2. (Optional) Ordner umbennennen

```
mv boss.Web-Basic www.websitedomain.de
```

3. Umgebungsvariablen anpassen

```
cp .sample.env .env
```

3. Umgebungsvariablen setzten

```
nano .env
```

```
CONTAINER_PREFIX=AwesomeProjekt
SUB=test
DOMAIN=domain.de
MYSQL_ROOT_PASSWORD=I1nqSsxGMNgbW9bDBRrUTHG3v8hA7Zaf
MYSQL_USER=website
MYSQL_PASSWORD=rtHziRRJLTJurMDqkJQ3kWKu6ZUK6ErT
MYSQL_DATABASE=website
REDIS_PASS=QbsZTgQRBuftaaAtskAKPd8Z21W6Zy2V
```

Passwörter als mindestens 32 Zeichen lange alphanumerische Zeichenketten. Diese können z.B. mithilfe eines **lokalen** Passwortmanager wie KeepassXC erzeugt werden.

4. Anwendung hochfahren

```
docker-compose up -d && docker-compose logs -f
```

5. Wordpress installieren

![WordpressInstallation.gif](WordpressInstallation.gif?fileId=232495#mimetype=image%2Fgif&hasPreview=true)

## Produktion

Währen der Entwicklung kann es sinnvoll sein, die Wordpress Anwendung lokal auszuführen.

Führe hierfür zunächst die Schritte 1-3 des Quickstart Kochrezepts durch.

1. NGINX Webserver konfigurieren

```
cp nginx-conf/nginx.template.conf nginx-conf/nginx.conf
nano nginx-conf/nginx.conf
```

```
...
       server_name domain.de test.domain.de;
...
                fastcgi_pass AwesomeProjekt-wordpress:9000;
...
```

1. Docker Stack hochfahren und Container Logs ausgeben.

```
docker-compose -f docker-compose.dev.yml up -d && docker-compose -f docker-compose.dev.yml logs -f
```

2. Wordpress installieren

# Konfiguration

## Maximale Upload Größe anpassen

Um die maximale Größe 

## Redis Cache 
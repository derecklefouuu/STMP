# Pterodactyl — installer StarTruckMP 1.8.0 **no-SSL**

## Fichiers
- `egg-startruckmp-NOSSL.json` : **utilisez celui-ci** (HTTP uniquement, aucun certificat).
- `linux-nossl.zip` : binaires serveur Linux 1.8.0 no-SSL (autonome, 44 Mo).

## Pourquoi no-SSL ?
Zéro certificat : pas d'auto-signé, pas d'avertissement navigateur, pas de
`IgnoreSslValidation`. L'API et la page `/admin` sont en **HTTP** sur le même
port que le jeu (7777 TCP+UDP). Les appels externes (validation Steam/Xbox)
restent en HTTPS, c'est obligatoire et invisible.

## Procédure
1. Uploade `linux-nossl.zip` sur ton GitHub (voir `github-upload/README-GITHUB.md`),
   puis remplace `GITHUB_USER` par ton pseudo dans l'egg (variable `URL de téléchargement`).
2. Panel admin → Nests → **Import Egg** → `egg-startruckmp-NOSSL.json`.
3. Crée le serveur avec **1 allocation** ; le port sert en **TCP+UDP**
   (vérifie que le nœud autorise l'UDP sur cette allocation).
4. Démarre : soit le script télécharge le zip GitHub tout seul, soit envoie le
   **contenu de `linux-nossl.zip`** à la racine via SFTP. Le panel détecte
   `Server started on port`.
5. Réglages via l'onglet **Variables** (priment sur `server.json` sans l'écraser).
6. Vérifie : `http://<ip>:<port>/api/status` → `{"version":"1.8.0",...}`.
   Change `STARTRUCK_ADMIN_PASSWORD` pour activer `http://<ip>:<port>/admin`.

## Variables d'environnement reconnues
`STARTRUCK_SERVER_NAME`, `STARTRUCK_MOTD`, `STARTRUCK_MAX_PLAYERS`,
`STARTRUCK_PORT` (+ `SERVER_PORT` = allocation panel), `STARTRUCK_IP`
(+ `SERVER_IP`), `STARTRUCK_PUBLIC_HOST` (informatif), `STARTRUCK_ADMIN_USER`,
`STARTRUCK_ADMIN_PASSWORD`, `STARTRUCK_STEAM_API_KEY`, `STARTRUCK_DATA_DIR`.

## Anciens fichiers (rappel, déjà nettoyés du package)
Les eggs `egg-startruckmp.json` / `-Copie` / `_v2` du dossier de test étaient
buggés (détection `Application started` inexistante, install cassé
`\(DOWNLOAD_URL`, `between:1|1000`, runtime .NET manquant). Ne plus les utiliser.

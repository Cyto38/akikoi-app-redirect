# akikoi-app-redirect

Seul rôle : rediriger **akikoi.app** vers **akikoi.fr**, en conservant le chemin, la
query et le fragment (`akikoi.app/e?lang=en#…` → `akikoi.fr/e?lang=en#…`).

Hébergé sur GitHub Pages (branche `main`, racine), HTML statique, zéro dépendance.

## Fonctionnement
- `index.html` et `404.html` sont **identiques**. GitHub Pages sert `404.html` pour tout
  chemin inconnu : c'est lui qui redirige `/e`, `/app`, `/o`, `/objets`, `/p`, etc.
- Un script en tête fait
  `location.replace('https://akikoi.fr' + location.pathname + location.search + location.hash)`.
  Le fragment (`#…`) ne quitte jamais le navigateur : seul le script peut le transmettre.
- Sans JavaScript, un `<meta http-equiv="refresh">` renvoie vers `https://akikoi.fr/`
  (le chemin est alors perdu).
- `noindex`, et aucune balise Open Graph : l'aperçu doit venir d'akikoi.fr.

## DNS attendu (zone akikoi.app)
| Type  | Nom   | Valeur              |
|-------|-------|---------------------|
| A     | @     | 185.199.108.153     |
| A     | @     | 185.199.109.153     |
| A     | @     | 185.199.110.153     |
| A     | @     | 185.199.111.153     |
| CNAME | www   | cyto38.github.io.   |

`CNAME` contient `akikoi.app`. « Enforce HTTPS » s'active dans les réglages Pages une
fois le certificat émis par GitHub (quelques minutes après que le DNS pointe ici).

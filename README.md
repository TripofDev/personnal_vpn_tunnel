# Accéder à un Raspberry Pi ( ou tout autre appareil)à  à distance via Tailscale (VPN privé) et SSH

## Objectif
Permettre à un d'accéder à son appareil à distance (peu importe l'IP publique ou le réseau) grâce à **Tailscale** et **SSH**, de manière sûre, rapide et sans configuration de box.

---

## Prérequis

- Un compte Google (pour se connecter à Tailscale)
- Une connexion de base à votre appareil où vous souhaitez avoir le vpn
- Un PC / Mac avec un terminal ou un logiciel SSH comme **Termius** 

---

## Ὄ2 1. Installation de Tailscale avec en exemple le Raspberry Pi

### Connexion SSH locale ou via écran/clavier

Ouvre un terminal sur ton Raspberry Pi puis exécute :

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

### Connexion du Raspberry à ton compte Tailscale

```bash
sudo tailscale up
```

Une URL apparaîtra. Ouvre-la dans un navigateur (depuis ton PC ou smartphone), et connecte-toi avec ton compte Google.

Une fois connecté, ton Raspberry apparaît dans [https://tailscale.com/admin/machines](https://tailscale.com/admin/machines).

### Récupérer son IP Tailscale (fixe)

```bash
tailscale ip -4
```

Exemple de résultat : `100.107.22.56`  → C'est l'IP que tu utiliseras pour te connecter en SSH l'ip privée

---

## 2. Connexion depuis un PC / Mac avec Tailscale

### Installer Tailscale sur ton poste de travail

- Va sur : [https://tailscale.com/download](https://tailscale.com/download)
- Télécharge et installe Tailscale pour ton OS
- Connecte-toi avec le **même compte Google** que sur le Raspberry Pi

Une fois installé et connecté : tu fais partie du même réseau privé chiffré.

---

## 3. Se connecter en SSH

### Via le terminal :
```bash
ssh pi@100.107.22.56
```
(Si ton utilisateur sur le Pi est `iot_project`, remplace `pi@` par `iot_project@`)

### Via Termius :
1. Crée un nouveau "Host"
2. Adresse : `100.107.22.56`
3. Port : `22`
4. Utilisateur : `iot_project`
5. Authentification : Password ou Clé SSH si configuré

---

## 4. Configuration facultative : connexion sans mot de passe

Gère une clé SSH avec :
```bash
ssh-keygen
```
Puis copie ta clé publique dans le fichier :
```bash
~/.ssh/authorized_keys
```
du Raspberry Pi (ou en utilisant `ssh-copy-id`).

---

## 5. Avantages de cette méthode

- Pas besoin d'ouvrir de port sur ta box
- IP fixe privée assurée
- Connexion chiffrée de bout en bout
- Accès distant de n'importe où dans le monde
- Possibilité de surveiller et contrôler tes bots, scripts, projets

---

## FAQ rapide

**Est-ce que l'IP Tailscale change ?**  
Non, elle reste stable tant que tu n'unlink pas l'appareil

**Est-ce que je peux accéder à d'autres appreils ?**  
Oui, tous les appareils connectés au même compte Tailscale sont interconnectés

**Est-ce que Tailscale est gratuit ?**  
Oui, jusqu'à 100 appareils pour un usage personnel


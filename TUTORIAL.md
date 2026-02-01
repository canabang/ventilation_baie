# 📚 Tutoriel d'Installation : Ventilation Baie de Brassage (V2 - Dual Zone)

Ce guide détaille l'installation de la version **V2 (Dual Zone)** du système de ventilation. Cette version permet de piloter **deux lignes de ventilateurs indépendantes** (Haut et Bas) pour refroidir efficacement votre équipement (Mini PCs, Switchs, etc.).

---

## � Aperçu du Projet

**L'objectif** : Refroidir la zone des équipements (Mini PCs ci-dessous) grâce à un montage piloté.

![Zone à refroidir (Baie / Mini PCs)](docs/IMG_20260201_121634.jpg)

---

## �🛠️ Matériel Requis

*   **ESP32** (Modèle S3 ou standard)
*   **Ventilateurs PWM** : ARCTIC P14 Pro PST(4 fils standard)
*   **Alimentation 12V** Dédiée ventilateurs
*   **Capteurs de Température DHT22** (x2)

---

## ⚡ Schéma de Câblage (V2)

Voici le schéma global de principe pour le raccordement de l'ESP32 avec les deux lignes de ventilateurs.

![Schéma de câblage global](docs/wiring_diagram.png)

### 1. Alimentation
*   **ESP32** : Via USB ou Vin (5V)
*   **Ventilateurs** : Raccordez le **GND** et le **12V** directement à l'alimentation externe.
    *   ⚠️ **IMPORTANT** : Reliez le GND de l'alim 12V au GND de l'ESP32 (masse commune).

### 2. Ventilateurs (Pinout)

Référez-vous à l'image ci-dessous pour identifier les câbles de vos connecteurs ventilateurs standards (PWM).

![Pinout Ventilateur PWM](docs/fan_pinout.png)

**Raccordement sur l'ESP32 :**

| Composant | Fil Ventilateur | Pin ESP32 | Fonction |
| :--- | :--- | :--- | :--- |
| **Ligne 1 (Haut)** | PWM (Bleu) | **GPIO 6** | Contrôle Vitesse |
| | Tach (Vert/Jaune) | **GPIO 4** | Retour Vitesse (RPM) |
| **Ligne 2 (Bas)** | PWM (Bleu) | **GPIO 35** | Contrôle Vitesse |
| | Tach (Vert/Jaune) | **GPIO 36** | Retour Vitesse (RPM) |

### 3. Capteurs de Température (DHT22)

| Composant | Pin DHT22 | Pin ESP32 |
| :--- | :--- | :--- |
| **DHT Ligne 1** | DATA | **GPIO 7** |
| **DHT Ligne 2** | DATA | **GPIO 37** |

---

## 🧪 Validation & Tests (Banc d'essai)

Avant l'installation finale dans la baie, il est recommandé de valider le montage "sur table" comme ci-dessous. Cela permet de vérifier que les RPM remontent bien et que les sondes réagissent.

![Montage sur table (Test)](docs/IMG_20260201_121203.jpg)

### Check-list de vérification :
1.  **RPM** : Faites tourner les ventilateurs à la main, la valeur doit s'afficher dans HA.
2.  **Température** : Soufflez sur les capteurs, la courbe doit monter.
3.  **Commandes** : Testez le Slider Manuel et le Boost.
4.  **perte de sonde** : Débranchez une sonde et vérifiez que la ligne se met bien à 50%.
5.  **surchauffe** : Chauffez une sonde au dessus de 30°C et vérifiez que la ligne se met bien à 100%.

---

## 💻 Installation Logicielle

### 1. Préparation dans Home Assistant
1.  Ouvrez l'interface **ESPHome** dans Home Assistant.
2.  Cliquez sur **"+ NEW DEVICE"**.
3.  Donnez-lui le nom `esp-fan`.
4.  **Clé API** : ESPHome va vous fournir une clé de chiffrement. **Copiez-la et conservez-la précieusement**, vous en aurez besoin à l'étape suivante.
5.  **Installation** : Une fois le device créé, ESPHome propose de l'installer. **ARRÊTEZ le processus** (cliquez sur "SKIP" ou fermez la fenêtre).
6.  Cliquez sur le bouton **"EDIT"** sur la nouvelle carte `esp-fan`.

### 2. Configuration du YAML
1.  **Nettoyage** : Effacez tout le contenu par défaut proposé dans l'éditeur.
2.  **Copie** : Copiez-collez l'intégralité du contenu du fichier [ventilation_v2.yaml](./ventilation_v2.yaml).
3.  **Clé API** : Recherchez la section `api:` et remplacez la valeur `key:` par celle que vous avez copiée à l'étape 1.
4.  **Dépendances** :
    *   Assurez-vous que le fichier [.base.yaml](./.base.yaml) est présent dans votre dossier `/config/esphome/`.
    *   Créez ou modifiez votre fichier `secrets.yaml` (utilisez [secrets.yaml.example](./secrets.yaml.example) comme modèle).
5.  **Flashage** : Cliquez sur **"SAVE"** puis sur **"INSTALL"**.

### 3. Dashboard Home Assistant
1.  Installez les pré-requis via **HACS** : `Mushroom`, `Streamline Card`, `Card Mod`.
2.  Utilisez le fichier [ventilation_card.yaml](./ventilation_card.yaml) pour créer votre interface (suivez les instructions à l'intérieur du fichier).

---

## 🛠️ Dépannage
*   **Les ventilateurs ne tournent pas ?** Vérifiez si le GND de l'alim 12V est bien relié à celui de l'ESP32.
*   **Température à NaN ?** Vérifiez le câblage du DHT22 et assurez-vous que la résistance de pull-up est présente (intégrée ou externe).
*   **RPM à 0 ?** Vérifiez que le fil Tach est sur le bon GPIO et que le ventilateur tourne réellement.

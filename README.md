# 🌬️ Projet Ventilation Baie Automatisée

Ce projet vise à créer un système de refroidissement intelligent pour une baie informatique (ou tout autre boîtier nécessitant une extraction d'air). Il utilise un ESP32-S3 pour réguler la vitesse de ventilateurs industriels (PWM) en fonction de la température ambiante mesurée par des capteurs DHT22.

## 🚀 Fonctionnalités Clés

- **Courbe Linéaire Intelligente** : La vitesse s'adapte progressivement entre deux seuils de température pour un silence optimal.
- **Réglage Dynamique** : Modifiez les seuils de température (Min/Max) directement depuis Home Assistant sans reflasher.
- **Mode Boost** : Un bouton pour forcer les ventilateurs à 100% pendant une durée réglable (1-60 min).
- **Priorité Manuelle** : Le mode automatique se désactive instantanément dès que vous réglez la vitesse manuellement.
- **Tableau de Bord Complet** : Suivi des RPM, de la température CPU de l'ESP32, de la température ambiante et de la puissance (%) envoyée.

## 🛠️ Matériel Requis

| Composant | Détails |
| :--- | :--- |
| **Microcontrôleur** | ESP32-S3 (ex: DevKitC-1) |
| **Ventilateurs** | Arctic P12 Pro PWM (Signal PWM 25kHz) |
| **Capteurs** | DHT22 (Température) |
| **Alimentation** | 12V (Ventilateurs) + 5V (ESP32) |

## 📂 Structure du Dépôt

- `ventilation_v1.yaml` : Version actuelle avec courbe linéaire et seuils dynamiques.
- `ventilation_v2.yaml` : Préparation pour la gestion bi-zone (2 lignes indépendantes).
- `TUTORIAL.md` : Guide complet d'installation et de configuration.
- `secrets.yaml.example` : Modèle pour vos identifiants WiFi.

## ⚙️ Installation Rapide

1. Installez [ESPHome](https://esphome.io/).
2. Créez votre fichier `secrets.yaml` (voir `TUTORIAL.md`).
3. Flashez : `esphome run ventilation_v1.yaml`.

## 📈 Roadmap

- [x] Phase 1 : Pilotage PWM et tachymètre.
- [x] Phase 2 : Automatisation par paliers.
- [x] Phase 3 : Courbe linéaire et seuils dynamiques via HA.
- [ ] Phase 4 : Extension bi-zone (V2).
- [ ] Phase 5 : Boîtier de contrôle sur mesure.

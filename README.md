# 🌬️ Projet Ventilation Baie Automatisée

Ce projet vise à créer un système de refroidissement intelligent pour une baie informatique (ou tout autre boîtier nécessitant une extraction d'air). Il utilise un ESP32-S3 pour réguler la vitesse de ventilateurs industriels (PWM) en fonction de la température ambiante mesurée par des capteurs DHT22.

## 🚀 Objectifs du Projet

- **Contrôle précis** : Utilisation du signal PWM pour une gestion fine de la vitesse.
- **Silence & Économie** : Arrêt total des ventilateurs sous un seuil de température défini.
- **Multi-zone** : À terme, gestion de deux lignes de ventilateurs indépendantes (2x2 ou 2x3 ventilateurs) avec chacune son propre capteur de température.
- **Connectivité** : Intégration complète à Home Assistant via ESPHome et interface web locale.

## 🛠️ Matériel Requis

| Composant | Détails |
| :--- | :--- |
| **Microcontrôleur** | ESP32-S3 (ex: DevKitC-1) |
| **Ventilateurs** | Arctic P12 Pro PWM (ou équivalent 4 fils) |
| **Capteurs** | DHT22 (Température & Humidité) |
| **Alimentation** | 12V pour les ventilateurs, 5V/USB pour l'ESP32 |

## 📂 Structure du Dépôt

- `ventilation_v1.yaml` : Version initiale (1 ligne, 1 capteur).
- *`ventilation_v2.yaml`* : (Prévu) Gestion multi-ligne.
- `secrets.yaml` : Contient vos identifiants WiFi (non inclus dans Git).

## ⚙️ Installation

1. Installez [ESPHome](https://esphome.io/) sur votre machine.
2. Utilisez le fichier `ventilation_v1.yaml`.
3. Créez un fichier `secrets.yaml` à la racine avec vos identifiants WiFi :
   ```yaml
   wifi_ssid: "VOTRE_SSID"
   wifi_password: "VOTRE_PASSWORD"
   ```
4. Compilez et flashez :
   ```bash
   esphome run ventilation_v1.yaml
   ```

## 📈 Roadmap

- [x] Phase 1 : Pilotage d'une ligne de ventilateur simple.
- [ ] Phase 2 : Extension à 2 lignes indépendantes.
- [ ] Phase 3 : Optimisation logicielle (hystérésis, courbes de ventilation personnalisées).
- [ ] Phase 4 : Conception d'un boîtier imprimé en 3D pour l'ESP32 et le câblage.

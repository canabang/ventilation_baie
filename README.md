# 🌬️ Ventilation Baie de Brassage (V2 - Dual Zone)

Projet de gestion intelligente de ventilation pour baie de brassage, basé sur **ESPHome** et **Home Assistant**.
Cette version V2 introduit une gestion bi-zone (Haut/Bas) indépendante pour optimiser le flux d'air et le refroidissement.

---

## ✨ Fonctionnalités Principales

*   **⚡ Dual Zone (Haut / Bas)** : Pilotage indépendant de deux rangées de ventilateurs.
*   **🌡️ Mode Automatique Intelligent** :
    *   Régulation PID simplifiée (courbe linéaire) basée sur la température de chaque zone.
    *   **Kickstart** : Impulsion de démarrage pour assurer la rotation des ventilateurs à basse vitesse.
*   **🚀 Mode Boost Global** : "Tout à fond" pendant une durée configurable (ex: 10 min) en un clic.
*   **🛡️ Sécurités Actives (Fail-Safe)** :
    *   **Perte de Sonde** : Si un capteur ne répond plus, la ligne concernée passe à 50% par sécurité.
    *   **Interlock Surchauffe** : Si la T° dépasse le seuil critique (`Max + 5°C`), toutes les lignes passent à 100%.
    *   **Indicateur RPM** : Surveillance de la vitesse réelle des ventilateurs.

---

## 📂 Structure du Projet

*   **`ventilation_v2.yaml`** : Configuration principale ESPHome (Code source à flasher).
*   **`.base.yaml`** : Configuration commune (WiFi, API, OTA).
*   **`ventilation_card.yaml`** : Code YAML complet pour le dashboard Home Assistant (Templates + Vue).
*   **`TUTORIAL.md`** : Guide pas à pas pour le câblage et l'installation.

---

## 🚀 Installation Rapide

1.  **Câblage** : Suivez le guide [TUTORIAL.md](./TUTORIAL.md).
2.  **Flashage** : Copiez les fichiers YAML dans votre dossier ESPHome et flashez votre ESP32.
3.  **Dashboard** : Copiez le contenu de `ventilation_card.yaml` dans une vue "Sections" de votre Home Assistant.

---

## 🔧 Configuration par défaut

*   **Consigne Min** : 25°C (0% de vitesse)
*   **Consigne Max** : 35°C (100% de vitesse)
*   **Durée Boost** : 10 minutes

*Ces valeurs sont ajustables directement depuis le dashboard.*

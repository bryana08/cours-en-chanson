# Service OCR

Reçoit une photo de cours manuscrit, appelle Google Cloud Vision API (Document Text Detection), renvoie le texte extrait.

**Stack suggérée** : Python (FastAPI)

## Fallback
Si le score de confiance de l'OCR est bas, renvoyer un statut permettant à l'utilisateur de corriger le texte manuellement côté frontend.

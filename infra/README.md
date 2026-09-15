# Infrastructure

Configuration Docker Compose pour l'orchestration locale des microservices :
- PostgreSQL (utilisateurs, métadonnées des chansons)
- RabbitMQ (pipeline asynchrone OCR → extraction → paroles → audio)
- MinIO (stockage photos, fichiers audio)

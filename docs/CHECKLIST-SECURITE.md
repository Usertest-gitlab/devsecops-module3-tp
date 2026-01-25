# Checklist Sécurité DevSecOps

Cette checklist permet de vérifier la conformité d'un projet aux bonnes pratiques DevSecOps.

---

## 1. Code Source

| Critère | Statut | Commentaire |
|---------|--------|-------------|
| Pas de secrets en dur dans le code | ☐ | Vérifier avec `git secrets` ou Gitleaks |
| Pas de credentials dans les commits | ☐ | Historique git vérifié |
| Dépendances à jour | ☐ | Dernière vérification : |
| Vulnérabilités connues corrigées | ☐ | Scan Trivy/Snyk |

---

## 2. Container / Docker

| Critère | Statut | Commentaire |
|---------|--------|-------------|
| Image de base minimale | ☐ | distroless, alpine, scratch |
| Multi-stage build | ☐ | Séparation build/runtime |
| User non-root | ☐ | `USER nonroot` ou équivalent |
| Pas de secrets dans l'image | ☐ | Pas de .env, credentials |
| Version de base épinglée | ☐ | Tag spécifique, pas `latest` |
| Scan vulnérabilités image | ☐ | 0 CRITICAL, 0 HIGH |

---

## 3. CI/CD Pipeline

| Critère | Statut | Commentaire |
|---------|--------|-------------|
| SAST configuré | ☐ | SonarQube, Semgrep |
| DAST configuré | ☐ | OWASP ZAP |
| Scan dépendances | ☐ | Trivy FS, npm audit |
| Scan container | ☐ | Trivy image |
| Pipeline bloquant sur vulns | ☐ | exit-code 1 |
| Secrets dans vault | ☐ | GitHub Secrets, pas en clair |
| Permissions minimales | ☐ | GITHUB_TOKEN restreint |

---

## 4. Conformité & Documentation

| Critère | Statut | Commentaire |
|---------|--------|-------------|
| SBOM généré | ☐ | CycloneDX ou SPDX |
| Licences vérifiées | ☐ | Pas de licence restrictive |
| Documentation sécurité | ☐ | SECURITY.md présent |
| Politique de divulgation | ☐ | Contact sécurité défini |
| Logs d'audit | ☐ | Traçabilité des actions |

---

## 5. Déploiement

| Critère | Statut | Commentaire |
|---------|--------|-------------|
| Environnement de prod protégé | ☐ | Approbation manuelle |
| Rollback possible | ☐ | Procédure documentée |
| Monitoring sécurité | ☐ | Alertes configurées |
| Backup vérifié | ☐ | Restauration testée |

---

## Signature

| Rôle | Nom | Date | Signature |
|------|-----|------|-----------|
| Développeur | | | |
| Tech Lead | | | |
| Security Officer | | | |

---

## Historique des révisions

| Version | Date | Auteur | Modifications |
|---------|------|--------|---------------|
| 1.0 | | | Création initiale |

---

*Template DevSecOps - Formation ENI 2026*

# SBOM - Software Bill of Materials

## Qu'est-ce qu'un SBOM ?

Un **SBOM** (Software Bill of Materials) est un inventaire complet de tous les composants logiciels utilisés dans une application :
- Dépendances directes et transitives
- Versions exactes
- Licences
- Provenance

## Pourquoi c'est important ?

### 1. Conformité réglementaire
- **Executive Order 14028** (USA) : Exige un SBOM pour les logiciels vendus au gouvernement
- **Cyber Resilience Act** (EU) : Impose des exigences de transparence
- **NIS2** : Renforce les obligations de sécurité

### 2. Gestion des vulnérabilités
- Identifier rapidement si une CVE affecte votre application
- Répondre aux incidents (ex: Log4Shell)
- Audit de sécurité

### 3. Gestion des licences
- Vérifier la compatibilité des licences
- Éviter les violations de licence
- Due diligence pour les acquisitions

## Formats standards

### CycloneDX
- Format léger orienté sécurité
- Supporte les vulnérabilités, licences, services
- Recommandé par OWASP

```json
{
  "bomFormat": "CycloneDX",
  "specVersion": "1.4",
  "components": [
    {
      "type": "library",
      "name": "example",
      "version": "1.0.0",
      "licenses": [{"license": {"id": "MIT"}}]
    }
  ]
}
```

### SPDX
- Format ISO/IEC 5962:2021
- Plus complet, orienté conformité
- Utilisé par Linux Foundation

```json
{
  "spdxVersion": "SPDX-2.3",
  "packages": [
    {
      "name": "example",
      "versionInfo": "1.0.0",
      "licenseConcluded": "MIT"
    }
  ]
}
```

## Génération du SBOM

### Avec Trivy

```bash
# Format CycloneDX
trivy image --format cyclonedx -o sbom.json myimage:tag

# Format SPDX
trivy image --format spdx-json -o sbom.json myimage:tag
```

### Avec Syft (Anchore)

```bash
# CycloneDX
syft myimage:tag -o cyclonedx-json > sbom.json

# SPDX
syft myimage:tag -o spdx-json > sbom.json
```

### Dans CI/CD

```yaml
- name: Generate SBOM
  uses: aquasecurity/trivy-action@0.24.0
  with:
    image-ref: 'myimage:tag'
    format: 'cyclonedx'
    output: 'sbom.json'

- name: Upload SBOM
  uses: actions/upload-artifact@v4
  with:
    name: sbom
    path: sbom.json
```

## Exploitation du SBOM

### Recherche de vulnérabilités

```bash
# Scanner un SBOM existant
trivy sbom sbom.json
```

### Vérification des licences

```bash
# Avec jq
jq '.components[].licenses[].license.id' sbom-cyclonedx.json | sort | uniq -c
```

### Intégration Dependency-Track

[Dependency-Track](https://dependencytrack.org/) permet de :
- Importer des SBOM
- Suivre les vulnérabilités en continu
- Alerter sur les nouvelles CVE
- Gérer les politiques de licence

## Bonnes pratiques

1. **Générer à chaque build** : Le SBOM doit refléter l'état actuel
2. **Archiver avec les releases** : Associer chaque version à son SBOM
3. **Automatiser** : Intégrer dans CI/CD
4. **Vérifier les licences** : Avant chaque release
5. **Scanner régulièrement** : Les vulnérabilités sont découvertes après le build

## Artifacts générés

Ce projet génère automatiquement :

| Fichier | Format | Usage |
|---------|--------|-------|
| `sbom-cyclonedx.json` | CycloneDX | Sécurité, vulnérabilités |
| `sbom-spdx.json` | SPDX | Conformité, licences |
| `sbom-table.txt` | Texte | Lecture humaine |

## Références

- [CycloneDX Specification](https://cyclonedx.org/specification/overview/)
- [SPDX Specification](https://spdx.dev/specifications/)
- [NTIA SBOM Minimum Elements](https://www.ntia.gov/page/software-bill-materials)
- [CISA SBOM](https://www.cisa.gov/sbom)

---

*Documentation Module 5 DevSecOps - ENI 2026*

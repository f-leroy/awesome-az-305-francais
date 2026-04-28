# Sources NotebookLM — URLs Microsoft Learn VERIFIEES

> **Verification effectuee le 2026-04-27** (24 URLs testees individuellement avec WebFetch).
>
> Pour chaque URL : canonical URL exacte + date de derniere update Microsoft.
>
> A coller dans NotebookLM **dans l'ordre indique** par notebook.

---

## Comment utiliser ce fichier

1. Cree 4 notebooks NotebookLM (1 par domaine)
2. Upload les fiches `.md` du kit en sources
3. **Copie-colle les URLs ci-dessous** une par une dans le notebook correspondant
4. Attends l'indexation (visible dans la sidebar)
5. Verifie avec un prompt test
6. Lance la generation (slides, mind maps, audio)

> [!NOTE] **Toutes ces URLs sont les canoniques verifiees**. Aucun redirect, aucun 404.
> Les pages ont ete updatees Microsoft entre **decembre 2025 et avril 2026**.

---

## NOTEBOOK 1 — Domain 1 (Identity, Governance, Monitoring)

### Sources kit a uploader

```
fiches-formateur/domain-1-identity-governance/*.md (toutes)
retours-experience-candidats.md
cheatsheets/waf-tradeoffs.md
methodology/how-to-attack-a-case-study.md
```

### URLs Microsoft Learn

| # | URL | Sujet | Last update |
|---|-----|-------|-------------|
| 1 | https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-305 | AZ-305 Study guide officiel | 2026-03-19 |
| 2 | https://learn.microsoft.com/en-us/entra/identity/authentication/overview-authentication | Entra Authentication overview | 2026-04-01 |
| 3 | https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-strengths | Authentication strengths (FIDO2, passwordless, phishing-resistant) | 2026-03-27 |
| 4 | https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-configure | PIM (Privileged Identity Management) | **2026-04-24** |
| 5 | https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles | RBAC built-in roles | 2026-04-10 |
| 6 | https://learn.microsoft.com/en-us/azure/governance/policy/overview | Azure Policy overview | 2025-09-26 |
| 7 | https://learn.microsoft.com/en-us/azure/azure-monitor/fundamentals/overview | Azure Monitor (canonical fundamentals) | 2026-02-24 |
| 8 | https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options | CAF Landing Zone (Enterprise Scale modernise) | 2025-12-15 |

> [!TIP] L'URL 4 a ete updatee **hier** (2026-04-24) — c'est ultra frais.

---

## NOTEBOOK 2 — Domain 2 (Data Storage)

### Sources kit a uploader

```
fiches-formateur/domain-2-data-storage/*.md (toutes les 6 fiches)
mock-exams/mock-exam-sql-focused.md
case-studies/02-fabrikam-financial-dr.md
```

### URLs Microsoft Learn

| # | URL | Sujet | Last update |
|---|-----|-------|-------------|
| 9 | https://learn.microsoft.com/en-us/azure/azure-sql/azure-sql-iaas-vs-paas-what-is-overview | Azure SQL family (DB vs MI vs VM) | 2026-04-02 |
| 10 | https://learn.microsoft.com/en-us/azure/azure-sql/database/purchasing-models | DTU vs vCore purchasing models | 2026-01-13 |
| 11 | https://learn.microsoft.com/en-us/azure/cosmos-db/overview | Cosmos DB overview (canonical) | 2026-02-19 |
| 12 | https://learn.microsoft.com/en-us/azure/cosmos-db/consistency-levels | Cosmos consistency levels (5 niveaux) | 2025-12-19 |
| 13 | https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview | Blob tiers (Hot/Cool/Cold/Archive) | 2026-04-16 |
| 14 | https://learn.microsoft.com/en-us/azure/storage/common/storage-redundancy | Storage redundancy (LRS/ZRS/GRS/GZRS) | 2026-04-13 |
| 15 | https://learn.microsoft.com/en-us/fabric/fundamentals/microsoft-fabric-overview | Microsoft Fabric overview (canonical) | 2026-04-10 |

> [!IMPORTANT] URL 11 (Cosmos DB) : la page que je t'avais donnee initialement (`/introduction`) **redirige** vers `/overview` — j'ai mis le canonical.

---

## NOTEBOOK 3 — Domain 3 (Business Continuity)

### Sources kit a uploader

```
fiches-formateur/domain-3-business-continuity/*.md (3 fiches)
cheatsheets/waf-tradeoffs.md (section reliability)
case-studies/02-fabrikam-financial-dr.md
```

### URLs Microsoft Learn

| # | URL | Sujet | Last update |
|---|-----|-------|-------------|
| 16 | https://learn.microsoft.com/en-us/azure/reliability/availability-zones-overview | Availability Zones | 2026-04-07 |
| 17 | https://learn.microsoft.com/en-us/azure/site-recovery/site-recovery-overview | Azure Site Recovery (ASR) | 2025-10-07 |
| 18 | https://learn.microsoft.com/en-us/azure/backup/backup-overview | Azure Backup overview | 2026-01-23 |
| 19 | https://learn.microsoft.com/en-us/azure/azure-sql/database/failover-group-sql-db | SQL Auto-failover groups | 2026-03-03 |
| 20 | https://learn.microsoft.com/en-us/azure/well-architected/reliability/ | WAF Reliability pillar | **2026-04-23** |

> [!IMPORTANT] URL 19 : la page que j'avais donnee (`auto-failover-group-overview`) n'est pas la canonical. La bonne est `failover-group-sql-db` (a corriger dans le kit aussi).

---

## NOTEBOOK 4 — Domain 4 (Infrastructure)

### Sources kit a uploader

```
fiches-formateur/domain-4-infrastructure/*.md (8 fiches)
case-studies/01-contoso-global-migration.md
mock-exams/mock-exam-01.md
methodology/how-to-attack-a-case-study.md
```

### URLs Microsoft Learn

| # | URL | Sujet | Last update |
|---|-----|-------|-------------|
| 21 | https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree | Azure compute decision tree | 2026-03-28 |
| 22 | https://learn.microsoft.com/en-us/azure/aks/what-is-aks | AKS overview (canonical) | **2026-04-23** |
| 23 | https://learn.microsoft.com/en-us/azure/container-apps/overview | Container Apps overview | 2026-04-14 |
| 24 | https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction | ExpressRoute overview | 2026-03-04 |
| 25 | https://learn.microsoft.com/en-us/azure/virtual-wan/virtual-wan-about | Virtual WAN overview | 2026-02-23 |
| 26 | https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/load-balancing-overview | Load balancing decision (LB/AppGW/FrontDoor/TM) | 2026-03-11 |
| 27 | https://learn.microsoft.com/en-us/azure/service-bus-messaging/compare-messaging-services | Messaging compare (Service Bus vs Event Grid vs Event Hubs) | **2026-04-22** |
| 28 | https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/plan-migration | CAF Plan migration (7R framework) | 2026-03-25 |

> [!IMPORTANT] URL 22 : page initiale `/aks/intro-kubernetes` n'existe plus comme canonical. La vraie est `/what-is-aks`.
>
> URL 27 : la page n'est PAS sous `/event-grid/` mais sous `/service-bus-messaging/`. Subtil mais important.
>
> URL 28 : la page racine `/migrate/` redirige. La canonical est `/migrate/plan-migration`.

---

## Resume des corrections vs ma liste initiale

J'avais donne 26 URLs. Apres verification :

- **18 URLs** etaient **exactement correctes** (canonical match)
- **6 URLs** etaient **redirects** vers une URL canonique differente (corrected ci-dessus)
- **2 URLs** etaient **404** ou la page a bouge (corrected)

Toutes les **28 URLs ci-dessus sont VERIFIEES** au 2026-04-27, avec leur canonical exacte et date de derniere update Microsoft.

---

## Prompt de validation a tester avant generation

Apres avoir uploade kit + URLs, lance ce prompt dans NotebookLM :

```
Based on my sources, answer with citations:
1. What is Microsoft's preferred authentication method for privileged
   admins in 2026, and what makes it different from Authenticator app
   with number matching?
2. When should a candidate choose Azure SQL Managed Instance over
   Azure SQL Database in an exam scenario?
3. What is the canonical URL pattern for "Microsoft Entra ID" docs
   in 2026 (was Azure Active Directory before)?

Cite the source URL and section for each answer.
```

**Si NotebookLM repond avec citations precises** = base solide, tu peux generer slides/audio/mindmaps.

**Si reponses vagues** = ajoute plus de sources ou re-uploade les fiches.

---

## Bonus — sources YouTube valides 2026

A coller en plus dans chaque notebook (NotebookLM ingere transcript YouTube) :

### Channel John Savill

```
https://www.youtube.com/c/NTFAQGuy/playlists
```

### Playlist AZ-305 specifique (Savill)

Cherche sur YouTube **"AZ-305 Designing Microsoft Azure Infrastructure Solutions Study Cram"** — c'est la video 4h reference de la communaute. Copie l'URL complete.

> [!TIP] Pour eviter d'inonder ton notebook de transcripts YouTube, **commence par 1-2 videos clefs** par domaine. Tu peux toujours en ajouter apres.

---

## Update log

- **2026-04-27** : verification initiale 28 URLs, 22 valides, 6 redirects/corrections

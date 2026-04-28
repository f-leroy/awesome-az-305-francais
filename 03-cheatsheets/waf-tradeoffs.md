# Cheatsheet — Well-Architected Framework Tradeoffs

> Le document le plus important du kit. A imprimer recto-verso et distribuer aux eleves **jour 1**.
> Source : https://learn.microsoft.com/en-us/azure/well-architected/

---

## Les 5 piliers du WAF (a memoriser par coeur)

| # | Pilier | Mnemonique | Question cle |
|---|--------|------------|--------------|
| 1 | **Reliability** | "ca tombe pas" | Comment je survis a une panne ? |
| 2 | **Security** | "pas pirate" | Comment je resiste aux attaques ? |
| 3 | **Cost Optimization** | "pas cher" | Comment je paie le bon prix ? |
| 4 | **Operational Excellence** | "ca tourne bien" | Comment je deploie et maintiens ? |
| 5 | **Performance Efficiency** | "ca va vite" | Comment je reponds a la charge ? |

> [!IMPORTANT] L'exam AZ-305 teste la capacite a **arbitrer** entre ces 5 piliers.
> Tu ne peux JAMAIS maxer les 5 en meme temps. Il faut choisir.

---

## Les 10 tradeoffs classiques (a enseigner par coeur)

### 1. Reliability ↔ Cost

| Tu veux plus de... | Tu sacrifies... |
|--------------------|-----------------|
| Availability Zones (3 AZ) | +50 a +200% cout compute |
| Geo-redundant backups (GRS) | +100% cout storage |
| Multi-region active-active | x2 infra complete |

> Exam pattern : "HA requirement + minimum cost" = **choisir AZ au lieu de multi-region**.

### 2. Reliability ↔ Performance

| Choix | Gain fiabilite | Perte performance |
|-------|----------------|-------------------|
| Synchronous replication | RPO = 0 | Latence ecriture ++ |
| Cross-region read replicas | DR ready | Consistency eventual |
| Retry avec backoff exponentiel | Resilience | Latence queue |

> Exam pattern : "strong consistency + global" = **tradeoff impossible** → privilegier la contrainte imposee.

### 3. Security ↔ Operational Excellence

| Tu imposes... | Tu compliques... |
|---------------|------------------|
| Private Endpoints partout | DNS + routing + support |
| Managed Identity exclusively | Migration tous secrets |
| Just-in-Time access (PIM) | UX admin, workflows approval |

> Exam pattern : "most secure + minimize admin overhead" = **PIM avec approbation automatique**.

### 4. Cost ↔ Performance

| Moins cher | Mais... |
|------------|---------|
| Basic tier (App Service B1) | Pas de scaling auto, pas de SLA |
| Standard storage | IOPS limite |
| Burstable VM (B-series) | Credits epuisables sous charge |
| Serverless Cosmos | Throughput non garanti |

> Exam pattern : "predictable workload + LEAST cost" = **Reserved Instances** (economie 30-72%).

### 5. Security ↔ Performance

| Controle securite | Cout performance |
|-------------------|------------------|
| TLS everywhere | +5-15ms par hop |
| WAF sur App Gateway | +10-50ms par requete |
| Firewall L7 inspection | +20-100ms |
| Always Encrypted (SQL) | Impact queries WHERE sur colonnes chiffrees |

> Exam pattern : "sub-10ms latency" = tu **dois sacrifier** du controle L7.

### 6. Operational Excellence ↔ Cost

| Best practice ops | Cout |
|-------------------|------|
| Environnements dev/staging/prod separes | x3 infra |
| Monitoring complet (Log Analytics + App Insights) | ingestion $$ |
| IaC + CI/CD | temps initial elevé |

### 7. Reliability ↔ Operational Excellence

| Tu rajoutes... | Ops complexity |
|----------------|----------------|
| Multi-region active-active | traffic manager + sync + monitoring croise |
| ASR (site recovery) | test DR quartely obligatoire |
| Database replicas | failover tests |

### 8. Performance ↔ Cost

| Perf boost | Cout |
|------------|------|
| Premium storage (SSD) | x2-x4 vs Standard HDD |
| Accelerated Networking | VM SKU plus grande |
| Ultra Disk | $$$$ |
| Cosmos DB autoscale | budget explose si burst |

### 9. Security ↔ Cost

| Controle | Cout |
|----------|------|
| Defender for Cloud (tous plans) | +15-30% facture |
| Azure Firewall Premium | 1400 USD/mois base |
| Private Link everywhere | endpoints $ |
| Key Vault Premium (HSM) | HSM dedies $$$$ |

### 10. Complexite architecture ↔ Everything

> [!WARNING] **Piege du design-heavy** : un design brillant mais trop complexe **perd sur l'exam**.
>
> Microsoft preferera **toujours** une solution **PaaS > IaaS**, **managed > self-managed**, **native > third-party**.

---

## Grille de decision rapide (a afficher en salle)

```
╔════════════════════════════════════════════════════╗
║  QUESTION EXAM : quel critere PRIORISER ?          ║
╠════════════════════════════════════════════════════╣
║                                                    ║
║  "ZERO downtime"        → Reliability              ║
║  "compliance / audit"   → Security                 ║
║  "minimum cost"         → Cost                     ║
║  "sub-Xms latency"      → Performance              ║
║  "minimum admin"        → Operational Excellence   ║
║                                                    ║
║  "best overall"         → suivre WAF + CAF guide   ║
║  "FIRST step"           → prerequis technique      ║
║  "MOST secure"          → Managed Identity + PE    ║
║  "LEAST privilege"      → RBAC granulaire          ║
║                                                    ║
╚════════════════════════════════════════════════════╝
```

---

## Les 3 rules of thumb Microsoft (a marteler aux eleves)

### Rule 1 — Managed over self-managed

Quand tu as le choix :
```
Azure SQL Managed Instance > SQL on VM
Azure Kubernetes Service   > Kubernetes on VM
Azure Functions            > VM runing cron
Azure AD (Entra ID)        > AD DS on VM
```

### Rule 2 — Native over third-party

Quand Microsoft a un produit first-party :
```
Azure Firewall             > Palo Alto NVA
Defender for Cloud         > CrowdStrike on VM
Log Analytics              > Splunk on VM
Azure Backup               > Veeam on VM
```

> [!NOTE] Ce n'est pas "mieux" techniquement — c'est la reponse attendue a l'exam.

### Rule 3 — Identity over network

Old world : perimeter security (firewall, VPN).
Azure world : **identity is the new perimeter**.

```
Conditional Access         > IP whitelisting
Managed Identity           > Connection strings
Private Endpoints + CA     > VNet isolation seule
```

---

## Les 6 "NEVER" a apprendre aux eleves

> [!WARNING] Ces reponses sont **TOUJOURS fausses** sur l'exam :

1. **Never** : connection strings ou credentials hard-coded
2. **Never** : SMS comme MFA "secure"
3. **Never** : AD FS pour une nouvelle implementation (deprecie)
4. **Never** : Owner ou Contributor au niveau subscription
5. **Never** : storage account public pour donnees sensibles
6. **Never** : cross-region sync pour "low latency" (incompatible)

Si tu vois une de ces reponses dans un QCM, **elimine-la sans meme lire le reste**.

---

## Les 6 "ALWAYS" a apprendre aux eleves

> [!TIP] Ces patterns sont **TOUJOURS preferables** sur l'exam :

1. **Always** : Managed Identity > Service Principal > Connection string
2. **Always** : Private Endpoint > Service Endpoint > Firewall IP rules
3. **Always** : Zone-redundant > Locally-redundant (sauf contrainte cout explicite)
4. **Always** : PIM + JIT > permanent admin roles
5. **Always** : Bicep/ARM templates > manual Portal config
6. **Always** : Paired region pour DR (respecte SLA Microsoft)

---

## Comment utiliser cette cheatsheet en salle

> [!IMPORTANT] Methode pedagogique :
>
> 1. Distribuer imprimee au **jour 1**
> 2. Y **referer a chaque case study** ("regardez la section Security ↔ Cost")
> 3. A la fin de chaque session, demander : **"Quel pilier on vient de sacrifier et pourquoi ?"**
> 4. Au **mock exam final**, l'eleve doit pouvoir la recopier de memoire en 5 min

La cheatsheet est l'**outil mental** que l'eleve utilisera en conditions exam. S'il la sait par coeur, il a deja 30% des points.

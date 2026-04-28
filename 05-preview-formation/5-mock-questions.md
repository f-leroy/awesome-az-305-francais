# 🎯 5 Mock Questions AZ-305 — Preview formation

> Echantillon de **5 questions** sur les **60+** disponibles en formation complete.
>
> Format **identique a l'exam reel** : 4 options, 1 reponse, explication detaillee.

---

## Question 1 — Identity & Authentication

You are designing an authentication solution for a global e-commerce platform with **3 million external customers**. The solution must support **social login** (Google, Facebook) and **minimize cost**.

**Which service should you recommend ?**

- A) Azure AD B2B with guest accounts
- B) **Azure AD B2C** (or Microsoft Entra External ID) with social identity providers
- C) Microsoft Entra ID with hybrid identity
- D) Azure Identity Protection with risk-based policies

<details>
<summary>📖 Voir la reponse + explication</summary>

### Reponse : **B** — Azure AD B2C / Microsoft Entra External ID

**Pourquoi B est correct** :
- B2C / External ID = service dedie pour customers retail (millions)
- Native support social login (Google, Facebook, Apple)
- Cost-effective : Monthly Active Users (MAU) pricing
- Custom branding + user flows

**Pourquoi les autres sont fausses** :
- **A** : B2B = pour partenaires business, pas pour customers retail. Guest accounts ne scale pas pour millions.
- **C** : Hybrid identity = pour employes on-prem + cloud, pas pour clients
- **D** : Identity Protection = ML risk detection, pas un service auth

**Mots-cles a reperer** :
- "external customers" → B2C / External ID
- "social login" → confirme B2C
- "millions" → confirme B2C (vs B2B qui ne scale pas)

> 💡 **Note 2026** : Microsoft migre progressivement vers "Microsoft Entra External ID". Les deux noms (B2C et External ID) peuvent apparaitre dans les questions.

</details>

---

## Question 2 — Database Selection

You need to migrate an **on-premises SQL Server 2019 database** that uses **SQL Server Agent jobs**, **Service Broker**, and **CLR assemblies**. The migration must use **minimum refactoring**.

**Which Azure service should you recommend ?**

- A) Azure SQL Database (General Purpose)
- B) Azure SQL Database (Hyperscale)
- C) **Azure SQL Managed Instance**
- D) SQL Server on Azure Virtual Machine

<details>
<summary>📖 Voir la reponse + explication</summary>

### Reponse : **C** — Azure SQL Managed Instance

**Pourquoi C est correct** :
- SQL MI = **SEUL** service Azure SQL qui supporte Service Broker
- Supporte SQL Agent jobs (SQL DB ne supporte pas)
- Supporte CLR assemblies
- Compatibility ~99% avec SQL Server on-prem
- "Minimum refactoring" matched

**Pourquoi les autres sont fausses** :
- **A et B** (SQL DB) : ne supportent **pas** Service Broker, ne supportent **pas** SQL Agent jobs
- **D** (SQL on VM) : fonctionnerait mais "minimum refactoring" prefere PaaS (et SQL on VM = "rehost" pas vraiment "minimum refactoring" au sens cloud-native)

**Mots-cles a reperer** :
- "SQL Server Agent" → JAMAIS SQL DB
- "Service Broker" → JAMAIS SQL DB, **TOUJOURS** SQL MI
- "Minimum refactoring" → SQL MI prefere a SQL on VM

> 💡 **Pattern recurrent** : 70% des questions SQL Server migration ont SQL MI comme bonne reponse en 2026.

</details>

---

## Question 3 — Network Security

You need to secure an **Azure Storage account** used by VMs in a VNet. The requirements are :
- **No public internet access** to the storage account
- Only the VNet can access
- **Audit all access attempts**

**What should you recommend ?**

- A) Storage firewall with selected IPs
- B) Service Endpoint for the subnet
- C) **Private Endpoint + disable public network access**
- D) VPN gateway with forced tunneling

<details>
<summary>📖 Voir la reponse + explication</summary>

### Reponse : **C** — Private Endpoint + disable public network access

**Pourquoi C est correct** :
- Private Endpoint = IP **privee** dans ta VNet pour acceder au PaaS
- "Disable public network access" = bloque litteralement tout acces depuis internet
- Trafic reste dans le **backbone Microsoft**
- Audit complet via Diagnostic Settings

**Pourquoi les autres sont fausses** :
- **A** : Firewall avec IPs n'empeche pas le public endpoint d'exister, donc l'attaque possible
- **B** : Service Endpoint optimise le routing mais le **public endpoint reste actif**
- **D** : VPN forced tunneling = overkill et complexe pour ce cas

**Mots-cles a reperer** :
- "No public internet access" → **Private Endpoint** uniquement
- "Most secure" + PaaS → toujours Private Endpoint en 2026

> 💡 **Pattern Microsoft 2026** : Microsoft pousse Private Endpoints comme **best practice** pour tous les PaaS. Service Endpoints = legacy a eviter.

</details>

---

## Question 4 — Business Continuity

You manage a web application deployed to **Azure App Service** in **West Europe**. You need DR with :
- **RTO 4 hours, RPO 1 hour**
- **Minimum cost**
- **Automatic failover**

**What should you recommend ?**

- A) Azure Site Recovery replicating the App Service
- B) **Deploy to a secondary region (North Europe) in warm-standby with Azure Traffic Manager automatic failover**
- C) Deploy active-active in West Europe and North Europe with Front Door Premium
- D) Azure Backup with geo-redundant storage

<details>
<summary>📖 Voir la reponse + explication</summary>

### Reponse : **B** — Warm-standby + Traffic Manager

**Pourquoi B est correct** :
- App Service deploye dans 2 regions (warm-standby = stopped en secondary)
- Traffic Manager = automatic failover via DNS health probes
- Cost minimum : tu paies juste storage en secondary (App Service stopped)
- Match les 3 requirements : RTO/RPO + cost + automatic

**Pourquoi les autres sont fausses** :
- **A** : ⚠️ **PIEGE CLASSIQUE** — **ASR ne supporte PAS App Service**. ASR = IaaS uniquement (VMs).
- **C** : Active-active = solide mais **cout x2** (contredit "minimum cost")
- **D** : Backup ne fournit **pas** de DR orchestree (juste donnees, pas service)

**Mots-cles a reperer** :
- "App Service" + "DR" → JAMAIS ASR (piege)
- "Minimum cost" + "automatic" → warm-standby + TM
- "Active-active" → si "minimum cost" pas mentionne

> 💡 **Le PIEGE #1 du domaine 3** : 80% des candidats choisissent A par reflexe. ASR ne marche pas pour PaaS. **A retenir absolument.**

</details>

---

## Question 5 — Compute & Architecture

You are designing a solution for **12 microservices** that process **events from Azure Service Bus**. The team has **no Kubernetes expertise**, and the solution must **scale to zero** when idle.

**What should you recommend ?**

- A) Azure Kubernetes Service (AKS) with KEDA installed
- B) **Azure Container Apps with KEDA scaling rules**
- C) Azure App Service with Linux containers
- D) Azure Container Instances for each microservice

<details>
<summary>📖 Voir la reponse + explication</summary>

### Reponse : **B** — Azure Container Apps with KEDA

**Pourquoi B est correct** :
- Container Apps = **built-in KEDA** (scale-to-zero natif)
- Pas besoin d'expertise Kubernetes
- Optimal pour microservices event-driven
- Match les 3 contraintes : pas K8s expertise + scale-to-zero + microservices

**Pourquoi les autres sont fausses** :
- **A** : AKS + KEDA fonctionnerait mais "no Kubernetes expertise" l'exclut. AKS = expertise required.
- **C** : App Service ne fait **pas** scale-to-zero natif (sauf tricks)
- **D** : Container Instances = **pas d'orchestration** ni scaling. Pour 12 microservices = inadapte.

**Mots-cles a reperer** :
- "Microservices" + "scale to zero" + "no K8s expertise" → **toujours Container Apps** en 2026
- "KEDA" → indice fort Container Apps (ou AKS+KEDA)

> 💡 **Note 2026** : Microsoft pousse Container Apps comme l'option moderne pour event-driven workloads. Differencier de Container Instances (1 container standalone, pas d'orchestration).

</details>

---

## 📊 Resultats — comprendre votre score

```
✅ 5/5 : Excellent — vous etes pret a passer l'AZ-305
🟡 4/5 : Tres bon — revisez les domaines rates
🟠 3/5 : OK — il vous faut encore preparation
🔴 ≤2/5 : Plan d'apprentissage structure necessaire
```

## 🎓 Vous voulez les 55 autres questions ?

Cette preview vous montre la **qualite du materiel**. La formation complete inclut :

- ✅ **30 questions Mock Exam General** (couvre les 4 domaines)
- ✅ **15 questions Mock Exam SQL-focused** (databases deep dive)
- ✅ **10 questions Mock Exam Identity** (FIDO2, PIM, CA)
- ✅ Explications detaillees pour CHAQUE option (bonne ET mauvaises)
- ✅ Patterns Microsoft expliques
- ✅ **2 case studies completes** (Contoso + Fabrikam)
- ✅ Methode "Attack a case study" (45 min de coaching)

📧 Demande devis : [fr3dlry@gmail.com](mailto:fr3dlry@gmail.com)

🎯 Formations en francais, presentiel ou distanciel.

---

## 💡 Comment utiliser ces 5 questions

```
Etape 1 : Bloque 15 minutes
Etape 2 : Reponds aux 5 sans regarder les explications
Etape 3 : Compare avec les reponses
Etape 4 : Lis les explications (meme si tu as eu juste)
Etape 5 : Identifie tes patterns faibles
```

---

[⬅️ Mots-cles Exam](../04-vocabulaire/exam-keywords.md) | [Methode Case Study ➡️](methode-case-study-intro.md)

# Domaine 4 — Infrastructure

> **Poids exam** : **30-35%** (LE plus important — souvent plus de questions networking)
>
> **Niveau de difficulte** : ⭐⭐⭐⭐ (large mais predictible)

## 🎯 Decision tree principal — Compute

```mermaid
graph TD
    A[Choisir Compute] --> B{Event-driven<br/>court ?}
    
    B -->|Oui < 10 min| C[Azure Functions<br/>Consumption]
    B -->|Non| D{Container<br/>scale-to-zero ?}
    
    D -->|Oui simple| E[Container Apps<br/>+ KEDA]
    D -->|Non| F{Full Kubernetes<br/>CRDs/operators?}
    
    F -->|Oui| G[AKS]
    F -->|Non| H{Web app<br/>standard ?}
    
    H -->|Oui| I[App Service]
    H -->|Non| J{OS control<br/>legacy ?}
    
    J -->|Oui| K[Virtual Machines]
    J -->|Non| L[Re-evaluer requirements]
    
    style C fill:#10B981,color:#fff
    style E fill:#10B981,color:#fff
    style G fill:#3B82F6,color:#fff
    style I fill:#3B82F6,color:#fff
    style K fill:#F59E0B,color:#fff
```

## 🎯 Decision tree — Load Balancing

```mermaid
graph TD
    A[Load Balancing] --> B{HTTP s ?}
    
    B -->|Non TCP UDP| C[Azure Load Balancer<br/>Standard]
    B -->|Oui HTTP S| D{Scope ?}
    
    D -->|Single region| E[Application Gateway<br/>WAF v2]
    D -->|Global multi-region| F{Need CDN<br/>edge WAF ?}
    
    F -->|Oui| G[Front Door<br/>Premium]
    F -->|Non basic| H[Front Door<br/>Standard]
    F -->|DNS based legacy| I[Traffic Manager]
    
    style C fill:#3B82F6,color:#fff
    style E fill:#10B981,color:#fff
    style G fill:#10B981,color:#fff
```

## 🎯 Decision tree — Connectivite on-prem

```mermaid
graph TD
    A[On-prem to Azure] --> B{Use case ?}
    
    B -->|Single user laptop| C[P2S VPN]
    B -->|Office datacenter| D{Bandwidth<br/>requirement ?}
    
    D -->|Low cost <1Gbps| E[S2S VPN<br/>over internet]
    D -->|Dedicated private<br/>1-100 Gbps| F[ExpressRoute]
    
    B -->|Multi-region<br/>multi-office 15+| G[Virtual WAN<br/>managed hub-spoke]
    
    F --> F1{Scope ?}
    F1 -->|1 region only| F2[ExpressRoute Local<br/>cheapest]
    F1 -->|Geopolitical area| F3[ExpressRoute Standard]
    F1 -->|Global all regions| F4[ExpressRoute Premium]
    
    style F2 fill:#10B981,color:#fff
    style F4 fill:#3B82F6,color:#fff
    style G fill:#3B82F6,color:#fff
```

## 📚 Sous-competences officielles

### Design compute solutions (25-30%)

- Specify components of a compute solution based on workload
- Recommend a virtual machine-based solution
- Recommend a container-based solution
- Recommend a serverless-based solution
- Recommend a compute solution for batch processing

### Design an application architecture (20-25%)

- Recommend a messaging architecture
- Recommend an event-driven architecture
- Recommend a solution for API integration
- Recommend a caching solution for applications
- Recommend an application configuration management
- Recommend an automated deployment solution

### Design migrations (15-20%)

- Evaluate migration solution leveraging CAF
- Evaluate on-premises servers, data, applications
- Recommend solution for migrating to IaaS / PaaS
- Recommend solution for migrating databases
- Recommend solution for migrating unstructured data

### Design network solutions (30-35%)

- Recommend internet connectivity
- Recommend on-premises connectivity
- Recommend network performance optimization
- Recommend network security
- Recommend load-balancing and routing

## 🔑 Concepts cles

### Compute services compares

| Service | Use case | Scale to zero ? | GPU ? |
|---------|----------|-----------------|-------|
| **VM / VMSS** | Legacy, full control | ❌ | ✅ |
| **AKS** | Cloud-native, multi-app | Complex | ✅ |
| **Container Apps** | Microservices, event-driven | ✅ KEDA | ❌ |
| **App Service** | Web apps, APIs standard | ❌ | ❌ |
| **Functions Consumption** | Event-driven < 10 min | ✅ | ❌ |
| **Functions Premium** | Long-running | ❌ (min 1 warm) | ❌ |
| **Container Instances** | 1 container standalone | ❌ | ❌ |

### Messaging — la trinite

```mermaid
graph TB
    A[Messaging] --> B[Service Bus]
    A --> C[Event Grid]
    A --> D[Event Hubs]
    
    B --> B1[MESSAGES<br/>Transactional<br/>Orders / workflows]
    C --> C1[EVENTS<br/>Azure events<br/>Reactive]
    D --> D1[STREAMS<br/>Telemetry IoT<br/>Millions events/s]
    
    B1 --> B2[Queues + Topics<br/>FIFO sessions<br/>Dead letter]
    C1 --> C2[Pub-sub<br/>Webhooks<br/>Filters]
    D1 --> D2[Partitioned<br/>Kafka compatible<br/>1-90d retention]
    
    style B fill:#10B981,color:#fff
    style C fill:#3B82F6,color:#fff
    style D fill:#F59E0B,color:#fff
```

### Migration — Framework 7R (CAF)

```mermaid
graph LR
    A[Migration] --> B{Strategy ?}
    
    B --> R1[Rehost<br/>lift & shift]
    B --> R2[Replatform<br/>lift, tinker]
    B --> R3[Refactor<br/>containerize]
    B --> R4[Rearchitect<br/>microservices]
    B --> R5[Rebuild<br/>from scratch]
    B --> R6[Retire<br/>delete]
    B --> R7[Repurchase<br/>SaaS]
    
    R1 -.- R1d[Fastest<br/>least benefit]
    R7 -.- R7d[No code<br/>SaaS replacement]
```

## 🎯 Patterns exam recurrents

### Pattern "scale-to-zero"

```
"Microservices + scale to zero + minimum operational overhead"
                          ↓
                  Container Apps + KEDA

PIEGES :
  ❌ Functions Premium (NE scale PAS to zero)
  ❌ AKS + KEDA (overkill, ops elevee)
  ❌ App Service (ne fait pas scale-to-zero sans tricks)
  ✅ Container Apps = parfait match
```

### Pattern "Front Door vs App Gateway"

```
"Global + WAF + CDN" → Front Door Premium
"Regional + WAF + path routing" → App Gateway WAF v2
"Multi-region + non-HTTP" → Traffic Manager (DNS)
"Single region L4" → Load Balancer Standard
```

### Pattern "Migration FIRST step"

```
"Migration plan from on-prem to Azure FIRST step ?"
                        ↓
                Azure Migrate Assessment

JAMAIS la 1ere etape :
  ❌ Deploy infrastructure
  ❌ Refactor code
  ❌ Choose compute service
  
TOUJOURS en 1er :
  ✅ Discovery + Assessment
```

### Pattern "Most secure + private"

```
"PaaS access + no public internet"
              ↓
        Private Endpoint + disable public access

PIEGES :
  ❌ Service Endpoint (public endpoint reste actif)
  ❌ Firewall IP allowlist (public access enabled)
  ❌ VPN forced tunneling (overkill et complexe)
```

## 📺 Ressources video recommandees

### John Savill

- [AKS Master Class](https://www.youtube.com/c/NTFAQGuy/playlists) — 4h+ deep dive
- [Front Door vs App Gateway vs LB](https://www.youtube.com/c/NTFAQGuy/playlists)
- [Virtual WAN explained](https://www.youtube.com/c/NTFAQGuy/playlists)
- [ExpressRoute Deep Dive](https://www.youtube.com/c/NTFAQGuy/playlists)

## 📖 Documentation officielle

| Page | Priorite |
|------|----------|
| [Compute decision tree](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree) | 🔴 Critique |
| [Load balancing decision](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/load-balancing-overview) | 🔴 Critique |
| [Messaging services compared](https://learn.microsoft.com/en-us/azure/service-bus-messaging/compare-messaging-services) | 🔴 Critique |
| [AKS overview](https://learn.microsoft.com/en-us/azure/aks/what-is-aks) | 🔴 Critique |
| [Container Apps overview](https://learn.microsoft.com/en-us/azure/container-apps/overview) | 🔴 Critique |
| [ExpressRoute overview](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction) | 🟡 Important |
| [Virtual WAN overview](https://learn.microsoft.com/en-us/azure/virtual-wan/virtual-wan-about) | 🟡 Important |
| [CAF Migration plan](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/plan-migration) | 🟡 Important |

## ⚠️ Pieges exam — top 8

> [!WARNING]
>
> 1. **Functions Premium NE scale PAS to zero** (min 1 warm instance)
> 2. **Container Apps != Container Instances** (orchestration vs single container)
> 3. **App Service != global** (regional only)
> 4. **Traffic Manager = DNS** (pas L7 proxy comme Front Door)
> 5. **Load Balancer Basic = deprecie** sept 2025
> 6. **AKS Pod Identity = deprecie** → Workload Identity
> 7. **Default outbound SNAT = deprecating** → NAT Gateway
> 8. **Azure Blueprints = retiring juillet 2026** → Azure Policy + Deployment Stacks

## 🔥 Questions exam types

```
Q1: Microservices Service Bus, scale to zero, no K8s expertise ?
A: Azure Container Apps with KEDA

Q2: Global app + WAF edge + CDN ?
A: Azure Front Door Premium

Q3: 5 datacenters dedicated private 99.95% multi-region ?
A: ExpressRoute Premium + Global Reach OR Virtual WAN

Q4: 80 SQL Server databases online migration MI ?
A: Azure Database Migration Service (DMS) online

Q5: Storage account no public access + audit ?
A: Private Endpoint + disable public network access
```

---

[⬅️ Domain 3](domaine-3-business-continuity.md) | [📚 Cheatsheets ➡️](../03-cheatsheets/)

# 🌳 Decision Trees Azure — Cheatsheet visuel

> Les arbres de decision pour choisir le bon service Azure. **Format Mermaid** = render natif sur GitHub.

## 🖥️ Compute selection

```mermaid
graph TD
    Start[🤔 Quel compute<br/>choisir ?] --> Q1{Event-driven<br/>< 10 min ?}
    
    Q1 -->|Oui| F1[⚡ Azure Functions<br/>Consumption]
    Q1 -->|Non| Q2{Conteneur<br/>+ scale-to-zero ?}
    
    Q2 -->|Oui| F2[📦 Container Apps<br/>+ KEDA]
    Q2 -->|Non| Q3{Full Kubernetes<br/>operators/CRD ?}
    
    Q3 -->|Oui| F3[☸️ AKS]
    Q3 -->|Non| Q4{Web app<br/>standard ?}
    
    Q4 -->|Oui| F4[🌐 App Service]
    Q4 -->|Non| Q5{OS control<br/>ou GPU/legacy ?}
    
    Q5 -->|Oui| F5[💻 Virtual Machines]
    Q5 -->|Non| F6[🔄 Re-evaluer]
    
    style F1 fill:#10B981,color:#fff
    style F2 fill:#10B981,color:#fff
    style F3 fill:#3B82F6,color:#fff
    style F4 fill:#3B82F6,color:#fff
    style F5 fill:#F59E0B,color:#fff
```

## 🗄️ Database — Relational

```mermaid
graph TD
    Start[🤔 Quelle DB<br/>relational ?] --> Q1{Open source<br/>requis ?}
    
    Q1 -->|Oui PostgreSQL/MySQL| F1[🐘 PostgreSQL/MySQL<br/>Flexible Server]
    Q1 -->|Non SQL Server| Q2{Features SQL<br/>completes<br/>Service Broker<br/>SQL Agent ?}
    
    Q2 -->|Oui| F2[🔷 SQL Managed Instance]
    Q2 -->|Non standard SQL| Q3{Taille DB ?}
    
    Q3 -->|< 4 TB| Q4{Tier ?}
    Q3 -->|> 4 TB| F3[💎 SQL DB Hyperscale]
    
    Q4 -->|OLTP critical<br/>< 2ms latency| F4[⚡ SQL DB<br/>Business Critical]
    Q4 -->|Standard prod| F5[📊 SQL DB<br/>General Purpose]
    Q4 -->|Variable / dev| F6[😴 SQL DB<br/>Serverless]
    
    Q2 -->|Full OS control| F7[💻 SQL on Azure VM]
    
    style F2 fill:#10B981,color:#fff
    style F3 fill:#3B82F6,color:#fff
    style F4 fill:#10B981,color:#fff
    style F6 fill:#F59E0B,color:#fff
```

## 💾 Storage tier (Blob)

```mermaid
graph TD
    Start[🤔 Quel tier<br/>Blob ?] --> Q1{Frequence acces ?}
    
    Q1 -->|Active quotidien| F1[🔥 Hot]
    Q1 -->|Mensuel| F2[❄️ Cool<br/>min 30 jours]
    Q1 -->|Trimestriel| F3[🧊 Cold<br/>min 90 jours]
    Q1 -->|Compliance long-term| F4[🗄️ Archive<br/>min 180 jours<br/>rehydrate 1-15h]
    
    style F1 fill:#EF4444,color:#fff
    style F2 fill:#3B82F6,color:#fff
    style F3 fill:#06B6D4,color:#fff
    style F4 fill:#6366F1,color:#fff
```

## 📡 Storage redundancy

```mermaid
graph TD
    Start[🤔 Quel niveau<br/>redundancy ?] --> Q1{Need cross-region ?}
    
    Q1 -->|Non| Q2{Need zone-redundant ?}
    Q2 -->|Oui| F1[ZRS<br/>3 AZ in 1 region]
    Q2 -->|Non budget| F2[LRS<br/>3 copies 1 datacenter]
    
    Q1 -->|Oui DR| Q3{Need read access<br/>to secondary ?}
    Q3 -->|Non| Q4{Zone-redundant primary ?}
    Q3 -->|Oui| Q5{Zone-redundant primary ?}
    
    Q4 -->|Oui| F3[GZRS<br/>RECOMMANDE PROD]
    Q4 -->|Non| F4[GRS]
    
    Q5 -->|Oui| F5[RA-GZRS<br/>BEST OF BOTH]
    Q5 -->|Non| F6[RA-GRS]
    
    style F1 fill:#3B82F6,color:#fff
    style F3 fill:#10B981,color:#fff
    style F5 fill:#10B981,color:#fff
```

## ⚖️ Load Balancing

```mermaid
graph TD
    Start[🤔 Quel<br/>load balancer ?] --> Q1{HTTP s ?}
    
    Q1 -->|Non TCP UDP| F1[🔧 Load Balancer<br/>Standard L4]
    Q1 -->|Oui| Q2{Scope ?}
    
    Q2 -->|Single region| F2[🏢 App Gateway<br/>WAF v2 L7]
    Q2 -->|Global| Q3{Need CDN<br/>+ edge WAF ?}
    
    Q3 -->|Oui premium| F3[🌍 Front Door<br/>Premium]
    Q3 -->|Non basic L7| F4[🌍 Front Door<br/>Standard]
    Q3 -->|DNS-based<br/>non-HTTP| F5[🗺️ Traffic Manager<br/>legacy]
    
    style F2 fill:#10B981,color:#fff
    style F3 fill:#10B981,color:#fff
```

## 🌐 Connectivity on-prem to Azure

```mermaid
graph TD
    Start[🤔 Connect<br/>on-prem to Azure ?] --> Q1{Use case ?}
    
    Q1 -->|Single user laptop| F1[🔐 P2S VPN]
    Q1 -->|Office datacenter| Q2{Bandwidth ?}
    Q1 -->|Multi-region<br/>15+ offices| F2[🌐 Virtual WAN<br/>managed hub-spoke]
    
    Q2 -->|Low cost<br/>< 1 Gbps| F3[🛡️ S2S VPN<br/>over internet]
    Q2 -->|Dedicated private<br/>1-100 Gbps| Q3{Scope ?}
    
    Q3 -->|1 region| F4[⚡ ExpressRoute Local<br/>cheapest]
    Q3 -->|Geo area| F5[⚡ ExpressRoute Standard]
    Q3 -->|Global| F6[⚡ ExpressRoute Premium]
    
    style F2 fill:#10B981,color:#fff
    style F4 fill:#3B82F6,color:#fff
    style F6 fill:#10B981,color:#fff
```

## 📨 Messaging Services

```mermaid
graph TD
    Start[🤔 Messaging<br/>service ?] --> Q1{Type de payload ?}
    
    Q1 -->|Messages<br/>transactional| F1[📬 Service Bus<br/>Queues + Topics]
    Q1 -->|Events discrete<br/>reactive| F2[⚡ Event Grid<br/>Pub-sub]
    Q1 -->|Streams telemetry<br/>millions/s| F3[🌊 Event Hubs<br/>Kafka compat]
    Q1 -->|Real-time WebSocket<br/>to clients| F4[🔌 Web PubSub]
    
    style F1 fill:#10B981,color:#fff
    style F2 fill:#3B82F6,color:#fff
    style F3 fill:#F59E0B,color:#fff
```

## 🔐 Authentication choice

```mermaid
graph TD
    Start[🤔 Methode<br/>auth ?] --> Q1{Phishing-resistant<br/>requis ?}
    
    Q1 -->|Oui privileged admins| F1[🔑 FIDO2 Security Keys<br/>YubiKey]
    Q1 -->|Oui Windows fleet| F2[🪟 Windows Hello<br/>for Business]
    Q1 -->|Oui regulated<br/>PIV smartcard| F3[📛 Certificate-based]
    
    Q1 -->|Non passwordless ok| Q2{Mobile users ?}
    Q2 -->|Oui| F4[📱 Authenticator app<br/>passwordless mode]
    Q2 -->|Non| F5[📱 Authenticator app<br/>+ number matching]
    
    Q1 -->|Pas critique| F6[❌ SMS Voice<br/>DEPRECIES NE PAS UTILISER]
    
    style F1 fill:#10B981,color:#fff
    style F2 fill:#10B981,color:#fff
    style F3 fill:#10B981,color:#fff
    style F6 fill:#EF4444,color:#fff
```

## 🚀 Migration strategy (CAF 7R)

```mermaid
graph TD
    Start[🤔 Strategie<br/>migration ?] --> Q1{App fin de vie<br/>< 18 mois ?}
    
    Q1 -->|Oui| F1[🗑️ Retire<br/>Decommission]
    Q1 -->|Non| Q2{SaaS equivalent<br/>existe ?}
    
    Q2 -->|Oui CRM ERP| F2[🛒 Repurchase<br/>Dynamics 365 etc]
    Q2 -->|Non| Q3{Complexite<br/>+ differenciateur ?}
    
    Q3 -->|Tres complexe<br/>differenciateur| F3[🏗️ Rearchitect<br/>microservices]
    Q3 -->|Total rewrite<br/>cobol → cloud| F4[🆕 Rebuild]
    Q3 -->|Moyenne| Q4{Cloud benefits ?}
    
    Q4 -->|Eleves| F5[🔄 Refactor<br/>containerize]
    Q4 -->|Moyens| F6[🔧 Replatform<br/>SQL → SQL MI]
    Q4 -->|Faible<br/>simple rapide| F7[📦 Rehost<br/>lift and shift]
    
    style F1 fill:#EF4444,color:#fff
    style F6 fill:#10B981,color:#fff
    style F7 fill:#3B82F6,color:#fff
```

## 🔒 Network security layers

```mermaid
graph LR
    A[Internet] -->|L7 WAF + CDN| B[Front Door Premium]
    B -->|L7 routing + WAF| C[App Gateway WAF v2]
    C -->|L4 + state| D[Azure Firewall Premium<br/>+ TLS inspection]
    D -->|Subnet rules| E[NSG]
    E -->|Private| F[Azure Resources]
    
    style B fill:#10B981,color:#fff
    style D fill:#3B82F6,color:#fff
```

---

## 💡 Comment utiliser ces decision trees

1. **Pendant la prep** : memorise les decisions cles
2. **A l'exam** : reproduire mentalement le tree pour la question
3. **Imprime** ce fichier + colle au mur de bureau
4. **Refera** chaque tree de tete avant l'exam

> [!TIP] Si tu peux **reproduire les 8 trees de tete**, tu reussis 80% des questions de design AZ-305.

---

[⬅️ Cheatsheet WAF](waf-tradeoffs.md) | [Schemas ASCII ➡️](ascii-schemas.md)

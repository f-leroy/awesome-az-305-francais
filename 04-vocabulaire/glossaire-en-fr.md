# 📚 Glossaire EN/FR — Termes Azure AZ-305

> L'exam est en anglais. Comprendre le **vocabulaire technique exact** = +20% de points.

## 🎯 Comment utiliser ce glossaire

```
1. Lis chaque terme EN avec sa traduction FR
2. Repere ceux que tu confonds
3. Memorise par flashcards (Anki recommande)
4. Avant l'exam : revue rapide
```

---

## 🔐 Identity & Access

| Terme EN | Traduction FR | Definition |
|----------|---------------|------------|
| **Authentication** | Authentification | Prouver son identite |
| **Authorization** | Autorisation | Definir les droits d'acces |
| **Identity Provider (IdP)** | Fournisseur d'identite | Service qui gere les identites |
| **Single Sign-On (SSO)** | Authentification unique | Un login pour plusieurs apps |
| **Multi-Factor Authentication (MFA)** | Authentification multi-facteurs | 2+ facteurs |
| **Passwordless** | Sans mot de passe | Auth sans password |
| **Phishing-resistant** | Resistant au phishing | Auth liee crypto a l'origine |
| **Conditional Access** | Acces conditionnel | Policies d'acces dynamiques |
| **Privileged Identity Management (PIM)** | Gestion identites privilegiees | JIT admin access |
| **Just-In-Time (JIT)** | Juste-a-temps | Acces accordé a la demande |
| **Tenant** | Locataire | Instance Entra ID isolee |
| **Hybrid Identity** | Identite hybride | On-prem + cloud sync |
| **Federation** | Federation | Trust cross-tenant |
| **Guest user** | Utilisateur invite | User externe en B2B |
| **Workload Identity** | Identite de charge | Identite pour service (AKS) |
| **Managed Identity** | Identite geree | Service principal automatique |
| **Service Principal (SP)** | Principal de service | Compte applicatif |
| **Role-Based Access Control (RBAC)** | Controle acces base sur roles | Permissions par role |
| **Attribute-Based Access Control (ABAC)** | Controle acces base sur attributs | Conditions sur tags |
| **Access Review** | Revue d'acces | Recertification periodique |
| **Entitlement Management** | Gestion des droits | Access packages self-service |
| **Break-glass account** | Compte de secours | Acces d'urgence |
| **Lateral movement** | Mouvement lateral | Propagation attaquant |
| **Token theft** | Vol de jeton | Vol de session cookie |
| **Adversary-in-the-Middle (AiTM)** | Intercepteur | Attaque proxy phishing |

---

## 🗄️ Data & Storage

| Terme EN | Traduction FR | Definition |
|----------|---------------|------------|
| **Relational data** | Donnees relationnelles | Tables avec relations |
| **Semi-structured data** | Donnees semi-structurees | JSON, XML |
| **Unstructured data** | Donnees non structurees | Fichiers, images, video |
| **Schema** | Schema | Structure de donnees |
| **Partition** | Partition | Subdivision physique |
| **Sharding** | Partitionnement horizontal | Repartition par ligne |
| **Replication** | Replication | Copie de donnees |
| **Synchronous** | Synchrone | Bloquant, garanti |
| **Asynchronous** | Asynchrone | Non bloquant, eventual |
| **Consistency** | Coherence | Garantie de read sur writes |
| **Strong consistency** | Coherence forte | Linearisation, latest commit |
| **Eventual consistency** | Coherence eventuelle | Convergent dans le temps |
| **Hot tier** | Niveau chaud | Acces frequent |
| **Cool tier** | Niveau froid | Acces mensuel |
| **Cold tier** | Niveau tres froid | Acces trimestriel |
| **Archive tier** | Niveau archive | Long terme rarement accede |
| **Rehydration** | Rehydration | Restaurer Archive vers Hot |
| **Lifecycle management** | Gestion cycle de vie | Auto-tiering |
| **Soft delete** | Suppression douce | Recuperation possible |
| **Immutable storage** | Stockage immutable | WORM compliance |
| **Encryption at rest** | Chiffrement au repos | Donnees stockees chiffrees |
| **Encryption in transit** | Chiffrement en transit | TLS reseau |
| **Customer-Managed Key (CMK)** | Cle geree client | BYOK |
| **Service-Managed Key** | Cle geree service | MS gere |
| **TDE** | Transparent Data Encryption | Chiffrement transparent SQL |
| **Always Encrypted** | Toujours chiffre | Encryption client-side colonne |
| **Dynamic Data Masking (DDM)** | Masquage dynamique | Masking visuel |
| **Row-Level Security (RLS)** | Securite niveau ligne | Filtrage par contexte |

---

## 🔄 Business Continuity

| Terme EN | Traduction FR | Definition |
|----------|---------------|------------|
| **High Availability (HA)** | Haute disponibilite | Pas de downtime |
| **Disaster Recovery (DR)** | Reprise sur sinistre | Bascule region |
| **Backup** | Sauvegarde | Copie de donnees |
| **Recovery Time Objective (RTO)** | Objectif temps de reprise | Combien de temps down max |
| **Recovery Point Objective (RPO)** | Objectif point de reprise | Combien de donnees perdues max |
| **Failover** | Bascule | Passage primaire → secondaire |
| **Failback** | Retour | Retour sur primaire |
| **Active-active** | Actif-actif | 2+ regions actives simultanement |
| **Active-passive** | Actif-passif | 1 active + 1 standby |
| **Availability Zone (AZ)** | Zone de disponibilite | Datacenter physique |
| **Paired region** | Region appairee | Region soeur officielle |
| **Geo-replication** | Geo-replication | Replication cross-region |
| **Auto-failover group** | Groupe de bascule auto | Multi-DB auto failover |
| **Site Recovery (ASR)** | Reprise de site | Replication VM cross-region |
| **Drill** | Exercice | Test DR |
| **Resilience** | Resilience | Capacite a resister |

---

## 🖥️ Compute & Network

| Terme EN | Traduction FR | Definition |
|----------|---------------|------------|
| **Workload** | Charge de travail | App / processus |
| **Stateless** | Sans etat | Pas de persistance |
| **Stateful** | Avec etat | Persistance requise |
| **Scale up** | Scaler verticalement | Plus puissant |
| **Scale out** | Scaler horizontalement | Plus d'instances |
| **Auto-scaling** | Mise a l'echelle auto | Scaling base sur metrics |
| **Scale-to-zero** | Reduction a zero | Pas d'instance si idle |
| **Cold start** | Demarrage a froid | Delai de premier boot |
| **Reserved instance** | Instance reservee | Achat 1-3 ans discount |
| **Spot instance** | Instance spot | Capacity restante 80% off |
| **Serverless** | Sans serveur | Pas d'infra a gerer |
| **PaaS** | Platform as a Service | Plateforme manageée |
| **IaaS** | Infrastructure as a Service | Infrastructure manageée |
| **SaaS** | Software as a Service | Logiciel manageé |
| **Containerization** | Conteneurisation | Empaquetage app |
| **Orchestration** | Orchestration | Coordination conteneurs |
| **Service mesh** | Maillage de services | Reseau microservices |
| **Sidecar** | Side-car | Container helper |
| **Ingress** | Entree | Trafic entrant |
| **Egress** | Sortie | Trafic sortant |
| **VNet** | Reseau virtuel | Reseau Azure |
| **Subnet** | Sous-reseau | Subdivision VNet |
| **Peering** | Appairage | Connexion VNet-VNet |
| **NSG** | Network Security Group | Firewall L4 |
| **Private Endpoint** | Endpoint prive | IP privee pour PaaS |
| **Service Endpoint** | Endpoint service | Backbone optimise |
| **Hub-spoke** | Centre-rayon | Topologie reseau |
| **VPN Gateway** | Passerelle VPN | Tunnel VPN site-a-site |
| **ExpressRoute** | Itineraire express | Connexion privee dediee |
| **Bastion** | Bastion | Acces remote securise |

---

## 📨 Messaging & Integration

| Terme EN | Traduction FR | Definition |
|----------|---------------|------------|
| **Message broker** | Courtier de messages | Service messaging |
| **Queue** | File d'attente | FIFO classique |
| **Topic** | Sujet | Pub-sub |
| **Subscription** | Abonnement | Souscripteur a topic |
| **Publisher** | Editeur | Emetteur de messages |
| **Subscriber** | Abonne | Recepteur |
| **Pub/sub** | Publication/abonnement | Pattern messaging |
| **At-least-once delivery** | Livraison au moins une fois | Garantie minimum |
| **Exactly-once delivery** | Livraison exactement une fois | Garantie idempotent |
| **Dead-letter queue (DLQ)** | File des messages morts | Messages non traites |
| **Throughput** | Debit | Messages/sec |
| **Latency** | Latence | Delai message |
| **Backpressure** | Contre-pression | Mecanisme regulation |
| **Idempotent** | Idempotent | Replay safe |
| **Webhook** | Crochet web | Callback HTTP |
| **Event-driven** | Evenementiel | Architecture reactive |
| **Stream** | Flux | Donnees continues |

---

## 🚀 Migration

| Terme EN | Traduction FR | Definition |
|----------|---------------|------------|
| **Lift and shift** | Lift and shift | Rehost as-is |
| **Rehost** | Re-heberger | Migration sans changement |
| **Replatform** | Re-platformer | Migration avec ajustements |
| **Refactor** | Refactoriser | Containerize, code change |
| **Rearchitect** | Re-architecturer | Microservices rewrite |
| **Rebuild** | Reconstruire | From scratch |
| **Retire** | Mettre au rebut | Decommission |
| **Repurchase** | Rachat | Replace par SaaS |
| **Cutover** | Bascule finale | Switch production |
| **Discovery** | Decouverte | Inventory phase |
| **Assessment** | Evaluation | Compatibility check |
| **Wave** | Vague | Groupe migration |

---

## 🎯 Patterns d'architecture

| Terme EN | Traduction FR | Definition |
|----------|---------------|------------|
| **Microservices** | Microservices | Petits services autonomes |
| **Monolith** | Monolithe | Un seul gros service |
| **API Gateway** | Passerelle API | Entree unique APIs |
| **Circuit breaker** | Disjoncteur | Pattern resilience |
| **Bulkhead** | Cloison | Isolation des ressources |
| **Throttling** | Limitation | Limiter debit |
| **Rate limiting** | Limitation taux | Cap requests |
| **CQRS** | Command Query Responsibility Segregation | Separation read/write |
| **Event Sourcing** | Approvisionnement par evenement | Reconstituer etat |
| **Saga** | Saga | Transaction distribuee |
| **Strangler Fig** | Figuier etrangleur | Migration progressive |

---

## ⚠️ Mots-cles exam (les plus importants)

| Mot-cle EN | Signal a interpreter |
|------------|---------------------|
| **FIRST** | Prerequis technique avant action |
| **LEAST** | Minimum (cost, privilege, effort) |
| **MOST** | Maximum (secure, reliable, scalable) |
| **MINIMUM** | Minimum (downtime, admin effort) |
| **BEST** | Best practice Microsoft officielle |
| **NOT** | Question inversee — lire 2x |
| **EXCEPT** | Tout sauf — lire 2x |
| **ONLY** | Restriction unique |
| **ALL** | Pour toutes les ressources |
| **NEW** | Pour de nouvelles ressources |
| **EXISTING** | Pour les ressources existantes |
| **AT LEAST** | Au minimum |

---

## 🎯 Faux amis a connaitre

> [!WARNING] **Pieges traduction** :

| EN | FR FAUX | FR CORRECT |
|----|---------|------------|
| **Library** | Librairie (lieu) | **Bibliotheque** |
| **Eventually** | Eventuellement | **A terme / finalement** |
| **Actually** | Actuellement | **En realite / en fait** |
| **Sensible** | Sensible (delicat) | **Sense / raisonnable** |
| **Resume** | Resume (texte) | **CV / reprendre** |
| **Concurrent** | Concurrent (rival) | **Simultane / parallele** |
| **Consistent** | Consistant (epais) | **Coherent** |
| **Eventually consistent** | Eventuellement coherent | **Coherent a terme** |

---

[⬅️ Retour cheatsheets](../03-cheatsheets/) | [Mots-cles Exam ➡️](exam-keywords.md)

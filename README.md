# cloud-computing-aws


Perfecto. Como ya has estudiado AWS Cloud Practitioner, no voy a tratar esto como una introducción básica, sino como un **manual de repaso completo para CLF-C02**, orientado a reconocer rápidamente qué servicio o concepto busca cada pregunta.

Actualmente, **AWS Certified Cloud Practitioner CLF-C02** tiene 65 preguntas y 90 minutos. AWS indica que 50 preguntas puntúan y 15 no puntúan; la nota mínima es **700/1000**. Los dominios actuales son: Cloud Concepts 24%, Security and Compliance 30%, Cloud Technology and Services 34%, y Billing, Pricing and Support 12%. [docs.aws.amazon.com](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/?utm_source=chatgpt.com)

# AWS Certified Cloud Practitioner — Repaso completo CLF-C02

## 1. Primero: ¿qué es cloud computing?

Cloud computing significa consumir recursos informáticos bajo demanda a través de Internet en lugar de comprar, instalar y mantener toda la infraestructura física tú mismo.

Piensa en:

**Tradicional / On-Premises**

Empresa → compra servidores → instala hardware → configura red → instala software → mantiene infraestructura.

**Cloud**

Empresa → solicita recursos → AWS los proporciona → empresa paga por lo que consume.

Por ejemplo, necesitas un servidor durante dos días.

On-premises:

> Comprar servidor → esperar instalación → configurarlo → usarlo.

AWS:

> EC2 → Launch Instance → utilizar → terminar instancia.

La idea fundamental del cloud es:

**On-demand + elasticidad + pago por uso + automatización.**

---

# 2. Las ventajas fundamentales del Cloud

AWS espera que reconozcas estas ideas inmediatamente.

### Agility

Puedes experimentar y desplegar rápidamente.

En vez de esperar semanas para comprar infraestructura:

> AWS → recursos disponibles en minutos.

### Elasticity

Los recursos pueden aumentar o disminuir según la demanda.

Ejemplo:

```text
10 usuarios
↓
2 servidores

10 000 usuarios
↓
20 servidores

vuelve a bajar la demanda
↓
2 servidores
```

Elasticidad ≠ escalabilidad.

**Scalability** = capacidad para crecer.

**Elasticity** = crecer y reducir recursos dinámicamente según la demanda.

### High Availability

Una aplicación continúa disponible incluso cuando parte de la infraestructura falla.

Normalmente:

```text
Region
 ├── Availability Zone A
 │    └── EC2
 │
 └── Availability Zone B
      └── EC2
```

Si una AZ falla, la otra puede seguir sirviendo tráfico.

### Fault Tolerance

El sistema está diseñado para continuar funcionando incluso cuando ocurre un fallo.

Es un nivel más fuerte que simplemente intentar tener alta disponibilidad.

### Global Reach

Puedes desplegar aplicaciones cerca de usuarios de diferentes partes del mundo utilizando la infraestructura global de AWS.

### Economies of Scale

AWS compra y opera infraestructura a una escala enorme.

Eso permite repartir costes entre muchísimos clientes.

### Trade fixed expense for variable expense

Concepto MUY importante.

On-premises:

> compras hardware antes de saber exactamente cuánto utilizarás.

Cloud:

> consumes recursos según necesidad y pagas según consumo/modelo contratado.

### Stop guessing capacity

En infraestructura tradicional debes estimar:

> "Necesitaremos probablemente 50 servidores."

Si compras 100 → desperdicias dinero.

Si compras 20 → no tienes suficiente capacidad.

Cloud permite adaptar capacidad mucho más fácilmente.

AWS incluye explícitamente estos conceptos de valor del cloud, elasticidad, agilidad, alta disponibilidad, right-sizing, automatización, costes variables y economías de escala en el dominio Cloud Concepts. [docs.aws.amazon.com](https://docs.aws.amazon.com/es_es/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02-domain1.html?utm_source=chatgpt.com)

---

# 3. CAPEX vs OPEX

Debes entender esto muy bien.

### CAPEX — Capital Expenditure

Inversión inicial.

Ejemplo:

```text
Comprar servidores
Comprar edificio/datacenter
Comprar switches
Comprar almacenamiento
```

Pagas mucho antes de utilizar la infraestructura.

### OPEX — Operational Expenditure

Gastos operativos.

```text
Consumir EC2
Consumir S3
Consumir RDS
pagar según utilización
```

Cloud permite pasar gran parte del modelo:

**CAPEX → OPEX / variable consumption.**

---

# 4. Infraestructura global de AWS

Hay tres conceptos fundamentales:

```text
Region
Availability Zone
Edge Location
```

## Region

Una Region es una zona geográfica donde AWS tiene infraestructura.

Ejemplos:

```text
us-east-1
eu-west-1
eu-central-1
```

Una Region contiene varias Availability Zones.

Al elegir región debes pensar en:

- latency
- compliance/data residency
- service availability
- pricing

No todos los servicios están necesariamente disponibles de la misma manera en todas las regiones.

---

# 5. Availability Zone — AZ

Una AZ es una ubicación físicamente separada dentro de una Region.

Ejemplo conceptual:

```text
eu-west-1
│
├── eu-west-1a
├── eu-west-1b
└── eu-west-1c
```

Para alta disponibilidad:

❌ Dos servidores en una sola AZ.

Mejor:

```text
EC2 → AZ-A
EC2 → AZ-B
```

### Regla de examen

Si lees:

> Protect application against data-center/AZ failure

Piensa:

**Multi-AZ.**

---

# 6. Edge Locations

Las Edge Locations permiten acercar contenido/servicios de red a los usuarios.

Servicio que debes asociar inmediatamente:

**Amazon CloudFront.**

```text
User
 ↓
Edge Location
 ↓
CloudFront
 ↓
Origin
```

Esto reduce latencia.

No confundas:

**Region ≠ Availability Zone ≠ Edge Location.**

---

# 7. AWS Well-Architected Framework

AWS define actualmente **seis pilares**: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization y Sustainability. [docs.aws.amazon.com](https://docs.aws.amazon.com/wellarchitected/latest/userguide/waf.html?utm_source=chatgpt.com)

Memoriza:

**OSRPCS**

### Operational Excellence

Operar, monitorizar y mejorar sistemas y procesos.

Piensa:

> automation, operations, observability, continuous improvement.

### Security

Proteger:

- información
- sistemas
- infraestructura

Piensa:

> IAM, encryption, least privilege, logging.

### Reliability

El sistema debe recuperarse de fallos y satisfacer la demanda.

Piensa:

> backups, Multi-AZ, recovery, distributed architecture.

### Performance Efficiency

Utilizar los recursos tecnológicos adecuados eficientemente.

Piensa:

> elegir correctamente EC2/database/storage y adaptarlos cuando cambien las necesidades.

### Cost Optimization

Evitar gastos innecesarios.

Piensa:

> right-sizing, Savings Plans, Reserved Instances, Spot, Cost Explorer.

### Sustainability

Reducir el impacto ambiental de las cargas cloud.

Piensa:

> maximizar utilización, reducir recursos innecesarios, tecnologías eficientes.

---

# 8. Shared Responsibility Model

Probablemente uno de los conceptos más importantes de todo CLF-C02.

Memoriza esta frase:

> **AWS = Security OF the Cloud**
>
> **Customer = Security IN the Cloud**

### AWS protege

La infraestructura física y subyacente:

```text
Data centers
Physical servers
Networking infrastructure
Hardware
Virtualization infrastructure
```

### Cliente protege

Dependiendo del servicio:

```text
Data
IAM users
Permissions
Application configuration
Guest OS
Security groups
Encryption choices
```

Pero hay una trampa importante:

**La responsabilidad cambia según el servicio.**

---

# 9. Responsabilidad: EC2 vs RDS vs Lambda

## EC2

EC2 es IaaS.

AWS:

```text
hardware
physical infrastructure
hypervisor
```

Cliente:

```text
guest OS
OS patches
applications
data
security groups
IAM configuration
```

## RDS

AWS administra más.

AWS:

```text
physical infrastructure
database infrastructure
OS/platform maintenance
many patching/backup capabilities
```

Cliente sigue siendo responsable de:

```text
data
database access
IAM
configuration
network controls
```

## Lambda

AWS administra prácticamente toda la infraestructura de ejecución.

Cliente:

```text
code
data
IAM permissions
application logic
configuration
```

### Regla mental

Cuanto más managed es el servicio:

**más responsabilidad operacional absorbe AWS.**

---

# 10. IAM — Identity and Access Management

Servicio fundamental de seguridad.

IAM controla:

> **Who can do what on which AWS resources.**

Conceptos:

```text
Users
Groups
Roles
Policies
```

## IAM User

Representa normalmente una identidad con credenciales dentro de AWS.

## IAM Group

Agrupa usuarios.

Ejemplo:

```text
Developers
 ├── Alice
 ├── Bob
 └── Zakaria
```

Asignas permisos al grupo en lugar de gestionar cada usuario individualmente.

## IAM Policy

Documento que define permisos.

Conceptualmente:

```json
{
  "Effect": "Allow",
  "Action": "...",
  "Resource": "..."
}
```

No necesitas memorizar JSON avanzado para Cloud Practitioner.

Debes entender:

> Policy = permissions.

## IAM Role

Aquí aparecen muchas preguntas.

Un Role proporciona permisos que una identidad o servicio puede asumir.

Ejemplo:

EC2 necesita leer S3.

❌ Guardar Access Keys dentro del código.

✔️ Crear IAM Role y asociarlo a EC2.

```text
EC2
 ↓ assumes
IAM Role
 ↓
S3
```

---

# 11. Principle of Least Privilege

Fundamental:

> Dar solamente los permisos necesarios para realizar una tarea.

No:

```text
Developer → AdministratorAccess
```

si únicamente necesita:

```text
Read S3 bucket X
```

En preguntas:

> "Which security best practice?"

Muy frecuentemente:

**least privilege.**

---

# 12. Root User

La cuenta root tiene control extremadamente alto.

Buenas prácticas:

- no utilizarla para tareas diarias
- habilitar MFA
- proteger sus credenciales
- utilizar usuarios/roles adecuados para operaciones normales

---

# 13. MFA

Multi-Factor Authentication.

Combina más de un factor de autenticación.

Ejemplo:

```text
Password
+
Authenticator/security key
```

Especialmente importante para root y cuentas privilegiadas.

---

# 14. AWS Organizations

Permite administrar múltiples AWS accounts centralmente.

Ejemplo:

```text
AWS Organization
│
├── Management account
│
├── Production
├── Development
├── Security
└── Testing
```

Conceptos importantes:

### Organizational Units — OUs

Agrupan cuentas.

### Service Control Policies — SCPs

Establecen límites sobre qué acciones pueden realizar las cuentas/identidades dentro de la organización.

Una confusión típica:

**SCP no funciona simplemente como "dar permisos".**

Piensa en él como un **guardrail/límite máximo de permisos**.

---

# 15. AWS Control Tower

Si Organizations gestiona múltiples cuentas, Control Tower ayuda a configurar y gobernar un entorno multi-account siguiendo buenas prácticas.

Palabras clave:

> landing zone  
> multi-account governance  
> guardrails

→ **AWS Control Tower**

---

# 16. AWS Artifact

Pregunta típica:

> Company needs AWS compliance reports such as SOC reports.

Respuesta:

**AWS Artifact**

Artifact proporciona acceso bajo demanda a documentación relacionada con compliance.

---

# 17. AWS Audit Manager

Ayuda a recopilar evidencia y realizar auditorías de uso/riesgo/compliance.

No confundas:

**Artifact** → documentos/reportes de compliance de AWS.

**Audit Manager** → automatizar recopilación de evidencia para auditorías.

---

# 18. AWS CloudTrail

CloudTrail registra actividad/API calls en AWS.

Pregunta:

> Who deleted this S3 bucket?

→ **CloudTrail**

> Who changed this security group?

→ **CloudTrail**

Piensa:

**CloudTrail = audit trail / API activity.**

---

# 19. Amazon CloudWatch

CloudWatch = observabilidad y monitorización.

```text
Metrics
Logs
Alarms
Dashboards
```

Ejemplo:

> Alert me if EC2 CPU > 80%.

→ **CloudWatch Alarm**

Diferencia crítica:

**CloudWatch** → performance/metrics/logs/alarms.

**CloudTrail** → quién hizo qué mediante acciones/API.

Memoriza:

```text
CloudWatch → HOW is the system behaving?
CloudTrail → WHO did WHAT?
```

---

# 20. AWS Config

AWS Config observa configuración de recursos y cambios en esa configuración.

Pregunta:

> Track how configuration of AWS resources changed over time.

→ **AWS Config**

Comparación:

```text
CloudWatch → performance
CloudTrail → API activity
Config → resource configuration
```

Esta comparación merece memorizarse.

---

# 21. AWS Shield

Protección contra DDoS.

### Shield Standard

Protección básica incluida automáticamente.

### Shield Advanced

Protección DDoS más avanzada para necesidades superiores.

Keyword:

> DDoS

→ **Shield**

---

# 22. AWS WAF

Web Application Firewall.

Protege aplicaciones web frente a tráfico HTTP(S) malicioso.

Puede utilizar reglas relacionadas con:

- IPs
- patrones
- web exploits
- requests

Keyword:

> filter malicious web requests

→ **WAF**

No confundas:

```text
WAF → web attacks
Shield → DDoS
```

---

# 23. AWS KMS

Key Management Service.

Gestiona claves criptográficas.

Keyword:

> encryption keys

→ **KMS**

---

# 24. AWS Secrets Manager

Guarda y gestiona secretos.

Ejemplos:

```text
database passwords
API credentials
secrets
```

Puede ayudar con rotación de secretos.

Pregunta:

> Store and automatically rotate database credentials.

→ **Secrets Manager**

---

# 25. Amazon GuardDuty

Threat detection.

Analiza diferentes señales para detectar actividad sospechosa/maliciosa.

Keyword:

> threat detection / suspicious activity

→ **GuardDuty**

---

# 26. Amazon Inspector

Busca vulnerabilidades en determinadas workloads AWS, por ejemplo EC2 y container images.

Keyword:

> vulnerability management/scanning

→ **Inspector**

Comparación:

```text
GuardDuty → threats/suspicious activity
Inspector → vulnerabilities
```

---

# 27. Amazon Macie

Macie ayuda a descubrir y proteger datos sensibles almacenados en S3.

Keyword:

> sensitive data / PII in S3

→ **Macie**

---

# 28. AWS Security Hub

Centraliza información de seguridad/findings procedentes de diferentes servicios.

Piensa:

```text
GuardDuty
Inspector
otros findings
      ↓
 Security Hub
```

Keyword:

> centralized security posture/findings

→ Security Hub.

---

# 29. Amazon EC2

Elastic Compute Cloud.

Servidores virtuales.

```text
EC2 = virtual machine
```

Seleccionas:

- instance type
- CPU
- memory
- storage
- networking
- operating system

Ejemplos de familias conceptuales:

```text
General purpose
Compute optimized
Memory optimized
Storage optimized
Accelerated computing
```

No necesitas memorizar cada familia para Practitioner, pero sí entender por qué existen.

---

# 30. EC2 pricing

Muy importante.

## On-Demand

Pagas por uso sin compromiso de largo plazo.

Ideal:

> workloads impredecibles o de corta duración.

## Reserved Instances

Compromiso para obtener descuento frente a On-Demand en escenarios adecuados.

Ideal:

> workloads estables/predecibles.

## Savings Plans

Compromiso de una cantidad de uso/gasto durante un periodo a cambio de precios reducidos.

AWS suele presentar Savings Plans como una opción flexible para reducir costes de compute.

## Spot Instances

Utilizan capacidad EC2 sobrante a precio muy reducido.

Pero pueden ser interrumpidas.

Perfectas para:

```text
batch jobs
fault-tolerant workloads
distributed processing
```

Mal ejemplo:

> base de datos crítica que no puede interrumpirse.

Keyword:

> cheapest compute + interruption acceptable

→ **Spot**

## Dedicated Hosts

Servidor físico dedicado a un cliente.

Puede ser relevante para:

> compliance o licensing requirements.

---

# 31. Auto Scaling

Ajusta automáticamente capacidad.

```text
Traffic ↑
→ instances ↑

Traffic ↓
→ instances ↓
```

Beneficios:

- availability
- elasticity
- cost optimization

---

# 32. Elastic Load Balancing — ELB

Distribuye tráfico entre múltiples targets.

```text
Users
  ↓
Load Balancer
 ↓ ↓ ↓
EC2 EC2 EC2
```

Combinación clásica:

**ELB + Auto Scaling + Multi-AZ**

= arquitectura escalable y altamente disponible.

---

# 33. AWS Lambda

Serverless compute.

Subes código y AWS administra servidores subyacentes.

```text
Event
 ↓
Lambda
 ↓
Code executes
```

Ejemplos:

```text
S3 upload → Lambda
API request → Lambda
EventBridge → Lambda
```

Ventajas:

- no administrar servidores
- automatic scaling
- pago asociado a ejecución/uso

Keyword:

> run code without provisioning servers

→ **Lambda**

---

# 34. Elastic Beanstalk

Permite desplegar aplicaciones mientras AWS facilita/provisiona la infraestructura necesaria.

Tú:

```text
upload application
```

Beanstalk:

```text
EC2
Load Balancer
Auto Scaling
etc.
```

Keyword:

> deploy web application without manually managing infrastructure configuration

→ Elastic Beanstalk.

---

# 35. Containers: ECS, EKS, ECR

## ECS

Elastic Container Service.

Orquestación de containers usando tecnología AWS.

## EKS

Elastic Kubernetes Service.

Kubernetes administrado.

Keyword:

> Kubernetes

→ **EKS**

## ECR

Elastic Container Registry.

Repositorio de container images.

```text
Docker/container image
 ↓
ECR
```

---

# 36. AWS Fargate

Compute serverless para containers.

Funciona con ECS/EKS.

Sin gestionar directamente servidores EC2 para ejecutar los containers.

Keyword:

> containers without managing servers

→ **Fargate**

---

# 37. S3 — Simple Storage Service

Uno de los servicios más importantes.

S3 = **object storage**.

Guarda:

```text
photos
videos
backups
logs
documents
static files
```

Conceptos:

```text
Bucket
Object
Key
```

No es:

❌ block storage tradicional  
❌ file system tradicional

Es:

✔️ object storage.

---

# 38. S3 Storage Classes

Debes entenderlas conceptualmente.

### S3 Standard

Datos accedidos frecuentemente.

### S3 Intelligent-Tiering

AWS puede mover objetos automáticamente entre tiers según patrones de acceso, con el modelo correspondiente.

Pregunta:

> Access pattern unknown or changing.

→ **Intelligent-Tiering**

### S3 Standard-IA

Infrequent Access.

Datos menos accedidos pero que requieren acceso rápido cuando se necesitan.

### S3 One Zone-IA

Infrequent Access almacenado en una única AZ.

Menor resiliencia que opciones multi-AZ.

### S3 Glacier classes

Archivado.

Para datos accedidos raramente y donde diferentes tiempos de recuperación pueden ser aceptables.

Keyword:

> long-term archival

→ **S3 Glacier**.

---

# 39. S3 Lifecycle Policies

Automatizan transición/eliminación de objetos.

Ejemplo:

```text
Day 0 → S3 Standard
Day 30 → Standard-IA
Day 90 → Glacier
Day 365 → Delete
```

Muy útil para optimización de costes.

---

# 40. S3 Versioning

Conserva versiones de objetos.

Puede ayudar frente a:

- sobrescrituras accidentales
- eliminaciones accidentales

---

# 41. EBS

Elastic Block Store.

**Block storage para EC2.**

Piensa:

```text
EC2 hard drive
```

Aunque técnicamente hay matices de arquitectura, para Practitioner:

**EC2 persistent block volume → EBS.**

---

# 42. Instance Store

Almacenamiento temporal asociado al host físico.

Si la instancia se detiene/termina según escenario, los datos pueden perderse.

Keyword:

> temporary high-performance local storage

→ Instance Store.

---

# 43. EFS

Elastic File System.

File storage compartido y escalable para Linux.

```text
EC2 A ─┐
EC2 B ─┼→ EFS
EC2 C ─┘
```

Varias instancias pueden acceder al mismo filesystem.

Comparación fundamental:

```text
S3  → Object
EBS → Block
EFS → File
```

Memorízalo.

---

# 44. AWS Storage Gateway

Conecta entornos on-premises con almacenamiento AWS.

Keyword:

> hybrid storage

→ **Storage Gateway**

---

# 45. AWS Snow Family

Dispositivos/soluciones para mover grandes cantidades de datos y ciertos escenarios edge.

Pregunta típica:

> Transfer huge amount of data where network connection is too slow.

→ AWS Snow Family.

---

# 46. RDS

Relational Database Service.

Base de datos relacional administrada.

Motores comunes incluyen:

- MySQL
- PostgreSQL
- MariaDB
- Oracle
- SQL Server
- Aurora

AWS administra muchas tareas operativas.

---

# 47. Amazon Aurora

Base de datos relacional compatible con MySQL/PostgreSQL diseñada por AWS.

Keyword:

> AWS relational database compatible with MySQL/PostgreSQL

→ **Aurora**

---

# 48. RDS Multi-AZ vs Read Replica

Esta diferencia es muy preguntable.

## Multi-AZ

Objetivo principal:

**High Availability / disaster recovery.**

```text
Primary DB
    ↓ synchronous replication
Standby DB
```

Si primary falla → failover.

## Read Replica

Objetivo principal:

**Read scalability.**

```text
Primary
 ↓
Read Replica
 ↓
read queries
```

Memoriza:

```text
Multi-AZ → availability
Read Replica → read performance/scaling
```

---

# 49. DynamoDB

NoSQL database completamente administrada/serverless en su operación.

Características conceptuales:

- key-value/document
- baja latencia
- alta escalabilidad
- managed

Keyword:

> NoSQL at massive scale

→ DynamoDB.

---

# 50. ElastiCache

Caching in-memory.

Utiliza tecnologías como Redis/Valkey/Memcached según la oferta/configuración.

Objetivo:

> reducir latencia y descargar databases.

```text
Application
 ↓
Cache
 ↓ if missing
Database
```

---

# 51. Amazon Redshift

Data warehouse.

Keyword:

> analytics/data warehouse/large-scale SQL analytics

→ **Redshift**

No confundir con RDS.

RDS:

> transactional relational applications.

Redshift:

> analytics/data warehousing.

---

# 52. Amazon Athena

Permite consultar datos almacenados en S3 usando SQL.

Serverless.

Keyword:

> SQL queries directly against S3 data

→ **Athena**

---

# 53. AWS Glue

Servicio de integración de datos, muy asociado a ETL/data catalog.

Keyword:

> ETL

→ **Glue**

---

# 54. Amazon EMR

Procesamiento de big data usando frameworks como Spark.

Keyword:

> Hadoop/Spark/big-data cluster processing

→ **EMR**

---

# 55. Amazon Kinesis

Procesamiento/ingestión de streaming data.

Ejemplos:

```text
clickstreams
IoT data
application events
real-time streams
```

Keyword:

> real-time streaming

→ **Kinesis**

---

# 56. Amazon QuickSight

Business Intelligence y visualización.

Keyword:

> dashboards / BI visualization

→ **QuickSight**

---

# 57. VPC — Virtual Private Cloud

Red virtual privada dentro de AWS.

Conceptualmente:

```text
VPC
│
├── Public Subnet
│      └── Web server
│
└── Private Subnet
       └── Database
```

Debes conocer:

- subnets
- route tables
- internet gateway
- NAT
- security groups
- NACLs

---

# 58. Public vs Private Subnet

### Public subnet

Tiene una ruta apropiada hacia Internet Gateway.

Normalmente:

```text
Load balancer
public web components
```

### Private subnet

Sin acceso público directo desde Internet.

Normalmente:

```text
databases
internal application servers
```

---

# 59. Internet Gateway

Permite conectividad entre una VPC y Internet cuando rutas/configuración lo permiten.

Keyword:

> VPC Internet connectivity

→ Internet Gateway.

---

# 60. NAT Gateway

Permite que recursos en una private subnet inicien conexiones hacia Internet sin aceptar conexiones entrantes no solicitadas directamente desde Internet.

Ejemplo:

```text
Private EC2
 ↓
NAT Gateway
 ↓
Internet
```

Pregunta:

> Private EC2 needs to download software updates from Internet.

→ NAT Gateway.

---

# 61. Security Groups

Firewall virtual asociado a recursos como EC2.

Características esenciales:

**Stateful.**

Controla inbound/outbound traffic.

---

# 62. Network ACL

Firewall a nivel de subnet.

Características:

**Stateless.**

Puede tener reglas allow y deny.

Comparación:

```text
Security Group → resource/instance level → stateful
NACL → subnet level → stateless
```

Pregunta clásica.

---

# 63. Route 53

DNS service.

```text
example.com
 ↓
Route 53
 ↓
AWS resource/IP
```

También soporta routing policies y health checking.

Keyword:

> DNS

→ Route 53.

---

# 64. CloudFront

Content Delivery Network — CDN.

Usa edge locations para entregar contenido cerca de usuarios.

```text
S3/origin
 ↓
CloudFront
 ↓
Edge Location
 ↓
User
```

Keyword:

> globally deliver content with low latency

→ CloudFront.

---

# 65. Direct Connect

Conexión de red dedicada entre infraestructura del cliente y AWS.

Keyword:

> dedicated private network connection to AWS

→ Direct Connect.

---

# 66. Site-to-Site VPN

Conexión cifrada a través de Internet entre red on-premises y AWS.

Comparación:

```text
VPN → encrypted connection over Internet
Direct Connect → dedicated network connection
```

---

# 67. SQS

Simple Queue Service.

Message queue.

```text
Producer
 ↓
SQS Queue
 ↓
Consumer
```

Permite desacoplar componentes.

Si Consumer cae:

> los mensajes pueden permanecer en la cola para ser procesados posteriormente según configuración.

Keyword:

> decouple applications / message queue

→ **SQS**

---

# 68. SNS

Simple Notification Service.

Pub/Sub.

```text
Publisher
 ↓
SNS Topic
 ↓ ↓ ↓
Email
SQS
Lambda
etc.
```

Keyword:

> publish message to multiple subscribers

→ SNS.

Comparación:

```text
SQS → Queue
SNS → Pub/Sub
```

---

# 69. EventBridge

Event bus.

Permite conectar aplicaciones mediante eventos.

```text
Application
 ↓ event
EventBridge
 ↓
Lambda / Step Functions / etc.
```

Keyword:

> event-driven integration/event bus

→ EventBridge.

---

# 70. Step Functions

Orquesta workflows.

Ejemplo:

```text
Lambda A
 ↓
Lambda B
 ↓
Decision
 ↙     ↘
C       D
```

Keyword:

> coordinate/orchestrate serverless workflow

→ Step Functions.

---

# 71. Migration services

Debes diferenciar varios.

### AWS Migration Hub

Centraliza seguimiento de migraciones.

### AWS Application Migration Service

Ayuda a migrar servidores/aplicaciones a AWS.

### AWS Database Migration Service — DMS

Migra bases de datos.

Keyword:

> migrate database with minimal downtime

→ DMS.

### AWS Schema Conversion Tool

Puede ayudar a convertir schemas cuando migras entre determinados motores de bases de datos diferentes.

---

# 72. AWS Cloud Adoption Framework — CAF

Ayuda a organizaciones a planificar y estructurar transformación/adopción cloud.

Debes reconocer las perspectivas:

```text
Business
People
Governance
Platform
Security
Operations
```

No confundas:

**CAF** → transformación/adopción organizacional.

**Well-Architected** → buenas prácticas para workloads/arquitecturas.

---

# 73. Las estrategias de migración

Debes reconocer las famosas estrategias "R".

Entre ellas:

### Rehost

"Lift and shift."

Mover aplicación con cambios mínimos.

### Replatform

"Lift, tinker and shift."

Realizar optimizaciones limitadas sin rediseño completo.

### Refactor / Re-architect

Rediseñar para aprovechar capacidades cloud-native.

### Repurchase

Sustituir aplicación por otro producto, frecuentemente SaaS.

### Retain

Mantener temporalmente donde está.

### Retire

Eliminar lo que ya no se necesita.

### Relocate

Mover infraestructura/workloads manteniendo en gran medida su arquitectura, especialmente en determinados escenarios.

No necesitas obsesionarte con terminología secundaria, pero sí reconocer escenarios.

---

# 74. Infrastructure as Code

IaC significa definir infraestructura mediante código/templates.

Servicio fundamental:

**AWS CloudFormation**

Ejemplo conceptual:

```yaml
EC2
VPC
S3
RDS
```

Template → CloudFormation → infraestructura.

Ventajas:

- repeatability
- automation
- consistency
- version control

Keyword:

> provision AWS infrastructure using templates

→ CloudFormation.

---

# 75. AWS Systems Manager

Ayuda a gestionar recursos y operaciones.

Casos:

- patching
- automation
- inventory
- parameter management
- remote operational tasks

Keyword:

> operational management of AWS resources

→ Systems Manager.

---

# 76. AWS Trusted Advisor

Analiza tu entorno y proporciona recomendaciones.

Áreas históricamente asociadas incluyen:

- cost optimization
- performance
- security
- fault tolerance
- service limits/quotas

Keyword:

> AWS recommendations/best-practice checks

→ Trusted Advisor.

---

# 77. AWS Health

Información sobre eventos que pueden afectar recursos/servicios AWS.

Piensa:

> "¿Existe un evento AWS que afecta a mis recursos?"

→ AWS Health.

---

# 78. AWS Support

Debes entender que AWS ofrece diferentes niveles de soporte y que las prestaciones varían.

Para examen, más importante que memorizar cada detalle cambiante es entender la progresión:

```text
Basic
Developer
Business
Enterprise
```

y reconocer que niveles superiores ofrecen acceso y capacidades de soporte más avanzadas.

Los detalles de planes pueden cambiar, por lo que conviene revisar la tabla oficial poco antes del examen.

---

# 79. AWS Pricing

Tres ideas dominantes:

### Pay as you go

Pagas por recursos consumidos según el modelo del servicio.

### Save when you commit

Compromisos pueden reducir precio.

Ejemplo:

> Savings Plans / Reserved models.

### Pay less by using more

En determinados servicios existen precios por volumen.

---

# 80. AWS Free Tier

Permite utilizar determinados servicios dentro de límites/promociones correspondientes.

No cometas este error:

> "AWS Free Tier significa que AWS es completamente gratis."

❌ No.

Solo determinados recursos y cantidades son gratuitos según las condiciones vigentes.

---

# 81. AWS Pricing Calculator

Sirve para **estimar costes antes de desplegar**.

Pregunta:

> Estimate monthly AWS cost for planned architecture.

→ **AWS Pricing Calculator**

---

# 82. AWS Cost Explorer

Analiza costes y utilización históricos/actuales y ayuda a entender tendencias.

Pregunta:

> Analyze spending patterns.

→ **Cost Explorer**

---

# 83. AWS Budgets

Configura presupuestos y alertas.

Ejemplo:

```text
Budget = $500/month

Actual/forecast approaches threshold
↓
Alert
```

Pregunta:

> Notify me when spending exceeds/approaches $X.

→ **AWS Budgets**

---

# 84. Cost and Usage Report — CUR

Proporciona información de costes y uso muy detallada.

Keyword:

> most detailed cost and usage data/reporting

→ Cost and Usage Report.

---

# 85. AWS Marketplace

Marketplace para encontrar, comprar y desplegar software/soluciones de terceros disponibles para AWS.

Ejemplo:

```text
security software
databases
monitoring tools
enterprise applications
```

---

# 86. Consolidated Billing

AWS Organizations permite consolidar facturación de múltiples cuentas.

```text
Organization
├── Dev account
├── Prod account
├── Test account
└── Security account

          ↓

     Consolidated bill
```

Puede simplificar administración financiera y permitir beneficios relacionados con uso agregado en determinados modelos.

---

# 87. Tags

Tags = metadata key/value.

Ejemplo:

```text
Environment = Production
Project = Migration
Team = Backend
CostCenter = 123
```

Sirven para:

- organización
- automation
- access control en ciertos escenarios
- cost allocation

Pregunta:

> Identify AWS costs by project/team.

Piensa:

**cost allocation tags.**

---

# 88. High Availability vs Scalability vs Elasticity

No los mezcles.

### High Availability

Sistema disponible pese a fallos.

```text
Multi-AZ
```

### Scalability

Capacidad para soportar crecimiento.

Puede ser:

**Vertical scaling**

```text
small server → bigger server
```

**Horizontal scaling**

```text
1 server → 10 servers
```

### Elasticity

Añadir/quitar recursos dinámicamente según demanda.

```text
2 → 20 → 3
```

---

# 89. Disaster Recovery

Debes reconocer conceptos:

### RTO — Recovery Time Objective

¿Cuánto tiempo máximo puede estar indisponible el sistema?

> **TIME**

### RPO — Recovery Point Objective

¿Cuánta información/datos podemos permitirnos perder medido en tiempo?

> **DATA**

Memorización:

```text
RTO → downtime
RPO → data loss window
```

---

# 90. AWS Backup

Servicio centralizado para gestionar/automatizar backups de múltiples servicios AWS compatibles.

Keyword:

> centrally manage backups

→ AWS Backup.

---

# 91. Machine Learning / AI services

Cloud Practitioner puede preguntar qué servicio corresponde a un caso de uso.

## Amazon SageMaker

Construcción, entrenamiento y despliegue de modelos de ML.

> ML platform

→ SageMaker.

## Amazon Rekognition

Analiza imágenes y vídeo.

> image/video analysis

→ Rekognition.

## Amazon Transcribe

Speech → text.

```text
Audio → text
```

## Amazon Polly

Text → speech.

```text
Text → voice
```

Memoriza:

```text
Transcribe → hear → text
Polly → speak
```

## Amazon Translate

Traducción automática.

## Amazon Comprehend

NLP/análisis de texto.

Puede detectar:

- sentiment
- entities
- key phrases

## Amazon Lex

Conversational interfaces/chatbots.

## Amazon Textract

Extrae texto/datos de documentos.

## Amazon Bedrock

Servicio administrado para construir aplicaciones de IA generativa utilizando foundation models.

Como el examen y la lista de servicios pueden evolucionar, AWS mantiene una lista oficial de servicios "in scope"; actualmente incluye categorías que abarcan analytics, application integration, compute, containers, financial management y muchas otras. [docs.aws.amazon.com](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/clf-02-in-scope-services.html?utm_source=chatgpt.com)

---

# 92. Diferencias que tienes que saber de memoria

Esta parte es probablemente la más rentable para tu examen.

| Necesidad | Servicio |
|---|---|
| Virtual server | EC2 |
| Serverless functions | Lambda |
| Object storage | S3 |
| Block storage | EBS |
| Shared file storage | EFS |
| Relational database | RDS |
| AWS MySQL/PostgreSQL-compatible relational DB | Aurora |
| NoSQL | DynamoDB |
| Cache | ElastiCache |
| Data warehouse | Redshift |
| Query S3 with SQL | Athena |
| ETL/data integration | Glue |
| Big data/Spark | EMR |
| Streaming data | Kinesis |
| BI dashboards | QuickSight |
| DNS | Route 53 |
| CDN | CloudFront |
| Private AWS network | VPC |
| Dedicated on-prem ↔ AWS connection | Direct Connect |
| Encrypted network connection over Internet | VPN |
| Message queue | SQS |
| Pub/Sub notifications | SNS |
| Event bus | EventBridge |
| Workflow orchestration | Step Functions |
| Metrics/alarms/logs | CloudWatch |
| API audit/activity | CloudTrail |
| Resource configuration history | Config |
| DDoS protection | Shield |
| Web firewall | WAF |
| Encryption keys | KMS |
| Secrets | Secrets Manager |
| Threat detection | GuardDuty |
| Vulnerability management | Inspector |
| Sensitive data in S3 | Macie |
| Security findings aggregation | Security Hub |
| Compliance reports | Artifact |
| Infrastructure as Code | CloudFormation |
| Multi-account management | Organizations |
| Multi-account governance | Control Tower |
| Cost analysis | Cost Explorer |
| Cost alerts/budgets | Budgets |
| Future cost estimation | Pricing Calculator |
| Detailed billing data | Cost and Usage Report |
| Database migration | DMS |
| Migration tracking | Migration Hub |
| Hybrid storage | Storage Gateway |
| Offline/large data transfer | Snow Family |

---

# 93. Las confusiones que AWS utiliza para hacerte fallar

### CloudWatch vs CloudTrail vs Config

Pregunta:

> CPU is 95%.

**CloudWatch**

> Who terminated EC2?

**CloudTrail**

> Was security group configuration changed?

**Config**

---

### S3 vs EBS vs EFS

> Store millions of images.

**S3**

> Disk for EC2.

**EBS**

> Shared Linux filesystem across EC2 instances.

**EFS**

---

### SNS vs SQS

> Send notification to multiple subscribers.

**SNS**

> Queue messages for asynchronous processing.

**SQS**

---

### RDS vs DynamoDB

> relational SQL application.

**RDS**

> massively scalable NoSQL key-value/document workload.

**DynamoDB**

---

### Shield vs WAF

> DDoS.

**Shield**

> malicious HTTP/web request filtering.

**WAF**

---

### GuardDuty vs Inspector vs Macie

> suspicious AWS activity.

**GuardDuty**

> software/workload vulnerabilities.

**Inspector**

> sensitive data in S3.

**Macie**

---

### Cost Explorer vs Budgets vs Pricing Calculator

Antes de desplegar:

**Pricing Calculator**

Después, analizar gastos:

**Cost Explorer**

Avisarme de límites/presupuestos:

**Budgets**

---

### Multi-AZ vs Read Replica

Availability:

**Multi-AZ**

Read scalability:

**Read Replica**

---

# 94. Cómo pensar durante las preguntas

No intentes responder basándote únicamente en palabras memorizadas. Identifica primero **el problema real**.

Ejemplo:

> A company needs to process messages asynchronously and ensure that messages remain available if the processing component temporarily fails.

Extrae:

```text
asynchronously
messages
component can fail
messages retained
```

Respuesta:

**SQS**

No SNS.

---

Otro:

> Company needs globally distributed static content with low latency.

Palabras:

```text
global
content
low latency
```

→ **CloudFront**

---

Otro:

> Security team needs to determine which IAM user deleted an S3 bucket.

```text
WHO
performed
API action
```

→ **CloudTrail**

---

Otro:

> Finance team wants an alert when monthly AWS costs exceed $5,000.

```text
cost
threshold
alert
```

→ **AWS Budgets**

---

# 95. Arquitectura que debes visualizar mentalmente

Imagina una aplicación web típica:

```text
                    USERS
                      │
                      ▼
                  Route 53
                      │
                      ▼
                 CloudFront
                      │
                      ▼
              Load Balancer
                 /       \
                /         \
              AZ-A        AZ-B
               │            │
              EC2          EC2
                \           /
                 \         /
                  Amazon RDS
                   Multi-AZ
```

Ahora añade:

```text
S3 → static objects
CloudWatch → monitoring
CloudTrail → auditing
IAM → permissions
KMS → encryption keys
Auto Scaling → elasticity
WAF → web protection
Shield → DDoS
```

Si entiendes esta arquitectura, ya estás conectando una parte enorme del examen.

---

# 96. Serverless architecture que debes reconocer

```text
User
 ↓
API
 ↓
Lambda
 ↓
DynamoDB
```

Complementado posiblemente con:

```text
S3
SQS
SNS
EventBridge
Step Functions
```

Aquí el cliente no está administrando servidores EC2.

---

# 97. Arquitectura híbrida

```text
On-Premises
     │
     ├── VPN
     │
     └── Direct Connect
            │
            ▼
           AWS
```

Datos:

```text
On-Prem
 ↓
Storage Gateway
 ↓
AWS Storage
```

Migración masiva:

```text
On-Prem
 ↓
Snow Family
 ↓
AWS
```

---

# 98. Qué debes memorizar y qué NO

AWS Cloud Practitioner **no es un examen de programación ni de arquitectura avanzada**. AWS incluso marca coding, architecture design, troubleshooting e implementation como tareas fuera del alcance esperado para el candidato CLF-C02. [docs.aws.amazon.com](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/?utm_source=chatgpt.com)

Por eso no pierdas demasiado tiempo memorizando:

```text
CLI commands
CloudFormation syntax
IAM JSON avanzado
EC2 configuration detallada
CIDR calculations complejas
Kubernetes commands
SQL
programming
```

Sí debes dominar:

```text
WHAT service does
WHY you would use it
WHEN you would choose it
DIFFERENCE from similar services
pricing concept
security responsibility
```

---

# 99. Tu mapa mental final

Cuando veas **Compute**:

```text
EC2
Lambda
Elastic Beanstalk
ECS
EKS
Fargate
Auto Scaling
Load Balancing
```

Cuando veas **Storage**:

```text
S3
EBS
EFS
Storage Gateway
Snow Family
Backup
```

Cuando veas **Database**:

```text
RDS
Aurora
DynamoDB
ElastiCache
Redshift
```

Cuando veas **Network**:

```text
VPC
Subnet
Security Group
NACL
Route 53
CloudFront
Direct Connect
VPN
```

Cuando veas **Security**:

```text
IAM
KMS
Secrets Manager
Shield
WAF
GuardDuty
Inspector
Macie
Security Hub
Artifact
```

Cuando veas **Monitoring/Governance**:

```text
CloudWatch
CloudTrail
Config
Organizations
Control Tower
Trusted Advisor
Systems Manager
CloudFormation
```

Cuando veas **Integration**:

```text
SQS
SNS
EventBridge
Step Functions
```

Cuando veas **Analytics**:

```text
Athena
Glue
EMR
Kinesis
Redshift
QuickSight
```

Cuando veas **Cost**:

```text
Pricing Calculator
Cost Explorer
Budgets
Cost and Usage Report
Organizations
Tags
Savings Plans
Reserved
Spot
```

---

# 100. Las 30 asociaciones que quiero que tengas automáticas

Si puedes contestar esto prácticamente sin pensar, estás en buen camino:

```text
Virtual machine → EC2
Object storage → S3
Block storage → EBS
File storage → EFS

SQL managed DB → RDS
NoSQL → DynamoDB
Data warehouse → Redshift
Cache → ElastiCache

Serverless code → Lambda
Kubernetes → EKS
Containers → ECS
Container images → ECR

DNS → Route 53
CDN → CloudFront
Private network → VPC

Queue → SQS
Pub/Sub → SNS
Events → EventBridge

Monitoring → CloudWatch
Audit API activity → CloudTrail
Configuration tracking → Config

Permissions → IAM
Encryption keys → KMS
Secrets → Secrets Manager

DDoS → Shield
Web firewall → WAF
Threat detection → GuardDuty
Vulnerabilities → Inspector
Sensitive S3 data → Macie

Infrastructure as Code → CloudFormation
```

Y finalmente:

```text
Estimate future AWS cost → Pricing Calculator

Analyze actual spending → Cost Explorer

Set cost threshold/alert → Budgets

AWS compliance documents → Artifact

Database migration → DMS

Large offline data migration → Snow Family

Multi-account management → Organizations

Organizational cloud adoption → AWS CAF

Architecture best practices → Well-Architected Framework
```

Ese tipo de asociación es exactamente lo que necesitas para responder rápido.

---

## Lo que más debes dominar antes del examen

No repartiría tu esfuerzo por igual. **Technology and Services (34%) + Security and Compliance (30%) representan conjuntamente el 64% del contenido puntuado**, así que esos dos bloques merecen especial atención. Cloud Concepts supone 24% y Billing/Pricing/Support 12%. [docs.aws.amazon.com](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/?utm_source=chatgpt.com)

Además, AWS incluye explícitamente en el alcance APIs, migration, compute, databases, networking, storage, IAM/security, Infrastructure as Code, EC2 purchasing options, AWS CAF, Well-Architected, shared responsibility, pricing y support, entre otros conceptos. [docs.aws.amazon.com](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/clf-technologies-concepts.html?utm_source=chatgpt.com)

Para tu repaso final, yo memorizaría especialmente estas comparaciones:

**CloudTrail / CloudWatch / Config**

**S3 / EBS / EFS**

**RDS / Aurora / DynamoDB / Redshift**

**SNS / SQS / EventBridge**

**Shield / WAF / GuardDuty / Inspector / Macie**

**Security Group / NACL**

**Multi-AZ / Read Replica**

**On-Demand / Reserved / Savings Plans / Spot**

**Cost Explorer / Budgets / Pricing Calculator**

**Organizations / Control Tower**

**CAF / Well-Architected**

**AWS responsibility / Customer responsibility**

Y una última cosa importante: no conviertas el repaso en memorización de 100 definiciones aisladas. El examen está diseñado con distractores plausibles. AWS confirma que las preguntas pueden ser de opción única o respuesta múltiple y que los distractores están diseñados precisamente para parecer razonables a quien conoce los conceptos solo parcialmente. [docs.aws.amazon.com](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/?utm_source=chatgpt.com)

Por eso, para cada servicio debes poder responder cuatro cosas mentalmente:

**¿Qué hace? → ¿Cuándo lo usaría? → ¿Con qué servicio se confunde? → ¿Cuál es la diferencia?**

Cuando puedes hacer eso con los servicios de este resumen, ya no estás simplemente memorizando AWS Cloud Practitioner: estás preparado para razonar las preguntas de **CLF-C02**.

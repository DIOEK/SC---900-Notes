# SC---900-Notes

Shared responsibility in the cloud
With on premisses datacenters all resposibility is placed at the owner of the hardware. In cloud enviromnment, the responsibility is shared between the cloud provider and the client.
The ratio of shared responsibility varies between IaaS SaaS as PaaS:
  * IaaS - everythnig BUT the fisical components of the system are of the clients responsability
  * PaaS - The cloud provider now manages also the OS that the applications are running on. The client now takes care of code, configuration, access control and data.
  * SaaS - The client only controls data, access mangement (who access the service) and how to configure tenant level services ( settings for all users of the service that is being hosted).

Some things, like authentication settings, cryptography of data, devices that access the service, are always your responsibility.
The shift to cloud has great benefits for security fir many times the clound provider takes some aspects of security that are very costly or consuming for the client to hold.

AI shared responsibility model

With the growing adoption of AI by companies, we can see that the responsibility is also shared between AI companies and the users:

The provider must take care of all phisical aspects of AI also platform aspects, such as content filtering and safeguards

the user must police what data goes as imput with the prompts, the way the users uses the model, mitigating ai specific risks, access management

It's mostly a mix, a mix between SaaS and PaaS responsibilities.

Defense in Depth

The concept of Apllying many layers to IT security.

 * Physical security: Defending physical assets. Gates, guards, hounds of hell, access cards etc.
 * Identity and access controls: layer where users get identified by MFA or RBAC
 * Perimeter security: Protects the boundaries of the network via firewalls  and trafic protection tools
 * Network security: Protects the network from within. Subnets, NSGs and rules that work inside the network.
 * Compute security: Protecting vms and containers. Closing ports, restricting adm access, maintaining updates and software.
 * Application Security: Makes sure that apps are safe, via secure dev practices, autentication and autorization inside software and input validation.
 * Data security: most important layer, RW permissions, encryption and data classification.

Each layer slows an attacker since, to pass on to the next one the previous must've been conquered. And eventually someone or something will.

CIA Triad

Confidentiality: Making sure that data can only be seen by the correct eyes. Encryption is very used here, but also RBAC A data breach happens when confidentiality is lost.

Integrity: The data must be as it should be, not tampered by third parties. Not only malicious actors can compromise this step, but also bugs or network problems during transmission. Cryptographic hashing, audit logs and database transaction controls make sure of the part of the triad.

Availability: Making sure the when data is needed, it will be available. It can be threatened by DDoS attacks that flood services with traffic until they stop responding, ransomware that encrypts data until a ransom is paid, hardware failures, software bugs, and natural disasters. Controls that support availability include redundant infrastructure, load balancing, automatic failover, regular backups and tested recovery plans, and DDoS protection services.

Many attacks will threaten more than one piece of the triad


Zero-Thrust Model

Trust no one, verify everything. That means basically: there are no safe spots, even inside a network or a corporation and security can never be relaxed. Basically with porous network boundaries being a thing (work from home, external datacenters, personal apparel being used for work), security providers had to addapt to a point where there can be no more trust even inside of the network since the danger of lateral movement is so large.

Three guiding principles of ZT
Explicit verification: basically all signals warrat authentication such as locality, device and indentity. These are called signals and all of them must be evaluated.
Use least privilege access: JIT(Just In Time) access, the act of giving access to something only when it's needed and then taking it back. And JEA(Just Enough Acess) giving only necessary access, no more.
Assume Breach: Assume you will be invaded some time, always assume the worst.

Seven Pillars of ZT
 * Identities, may be Users, Services or Devices. When an idendity attempts to access a resource, it must be verified and authenticated before access is granted.
 * Devices create surface area. Every device is a possible entry-point.
 * Applications are the way data is used. Apps also must be authenticated, reviwed and monitored.
 * Infrastructure wether on premisses or cloud infrastructure is the same: attack surface.Configuration compliance, unusual behavior and version currency must be used to keep track of off it. JIT access limits window of exposure. Telemetry allows for attack detection.
 * Networks must be segmented so that the compromise of on aspect of the netwrok doesn't compromise the whole of it.
 * VIsibility Automation and orchestration tie all the other pillars togheter and allows for easier threat acessment. This pillar leads to the creation of a Security information and event management (SIEM) and security orchestration, automated response (SOAR). The SIEM correlates all pillars to detect threats while SOAR triggers allow for instant response.

Cryptopgraphy and Hash

Encryption is to act to make data unreadable to unauthorized personnel. To use encrypted data it must be decrypted and for that the user must be in possession of a cryptographic key.

There are two types of encryption: symmetric and assymetric.

Symmetric encryption: there only one key for both decryption and encryption, that makes symmetric encryptption faster and well suited for vasta ammounts of data. It is also less secure, because sending the unic key over a network might be unsafe
Assymetric encryption: uses a key pair, one for encyption and other for decryption. The keys are mathematically related but you cannot derive one from the other. The public key encrypts while the private key decrypts. 
Data encrypted with the public key can only be decrypted with the corresponding private key.
Data signed with the private key can be verified with the corresponding public key.
Anyone can know the public key, therefore anyone can encrypt, but only you have the private key so only you can decrypt the data.
Assymetric encryption is used in many procols day to day, such as ssh and https.

Digital signatures are made possible by assymetric encryption, this means that anyone that has access to the public key can  verify the authenticity and integrity of data. Authenticity means that the data was sent by the expected sender. Integrity means that data sent has not been tampered with.

 * Encryption by data state
 Data at rest: data stored at a physical device or a storage account is encrypted so if an attacker has access to ir but not to the keys of encryption, the data remains unnavailable to him.
 Data in transit: encryption of data moving to one location to another. Meaning that data is unreadale to anyone that can intercept it over the network. HTTPS, VPN and TLS all aplly this principle.
 Data in use: data loaded into a computers memory or being worked on by a CPU. Generally here data is decrypted. Encryption of data in use is achieved through confidential computing technologies that create protected execution environments, sometimes called secure enclaves, where data can be processed without being exposed even to the operating system or hypervisor.

Key storage. NEVER storage the key at the sma place as te data it encrypts. Use dedicated hardware for key storage. Rotate keys often, allways change keys. Controll who has access to keys, specially private keys. Azure Key vault is an azure service for key storage.

 * Hashing
 Hashing converts data to a fixed-lenght string of characters called a hash. This process is non reversible, you cannot reverse a hash into the original imput, it is usefull for verifying data that you don't actually need to use.
 Hashing is very much used to secure passwords. When an user logs in the system passes the input password and compares the resulting hash with the original stored hash. SO the original password is never stored anywhere. However, basic hashing has a known vulnerability: because hash functions are deterministic, attackers can precompute hashes for millions of common passwords and look them up in tables—called rainbow tables or dictionary attacks—to find matches.
 Salting: Since rainbow tables are a thing. Passwords are usually salted, this means that a salt is a unique, randomly generated value created for each individual password and added to it before hashing. Since every password recieves a different salt two users with the same passwrod will generate different hashes.This makes precomputed rainbow tables ineffective, because the attacker would need a separate lookup table for every possible salt value. (but no impossible)

 Descrive governance, risk, and compliance(GRC) concepts

  * Governance, risk, and compliance (GRC): the path organizations must follow so they can navigate the threats to security, both internal and external.
  Governance - system of rules practices and processes an organization uses to direct and control it's activities. In the security context, some examples would be: defining policies for data is classified, handled and retained, establishing standarts for identity and access management across the organization, creating approval processes, assigning ownership and accountability, setting the overall direction for the organization's security strategy.
  * Risk management - process of identifying, assessing and responding to threats or events that can negatively impact organizational objectives and or customer trust. Organizations face risk from both external and internal sources.
   * Identifying - discovering potential risks to the organization's systems
   * Assess - Evaluate risk based on it's potential impact and likelyhood of it ocurring.
   * Respond - Developing a plan for each respective risk.
   * Monitor - Continuously track identified risks, measure the effectiveness of controls, and update the assessment as the environment changes.
  * Compliance - Compliance refers to adherence to the laws, regulations, standards, and policies that apply to an organization based on its industry, geography, and the types of data it handles.
  
  Some familiar compliance frameworks and regulations include:

    HIPAA (Health Insurance Portability and Accountability Act): US regulations governing the protection and handling of health information.
    ISO 27001: An international standard for information security management systems.
    SOC 2 (Service Organization Control 2): An auditing standard for service providers that store or process customer data.
    

  Compliance and security are not the same. Compliance reffers to the minimum regulated by law. Security goes beyond it encompasses all the processes, technologies, and practices that protect data and systems from threats.
  Data residency: refers to where data can be stored and how and when it can be transferred, processed, or accessed internationally.
  Data sovereignty: Data sovereignty refers to the concept that data is subject to the laws and regulations of the country/region where it's physically collected, held, or processed.
  Data privacy: Privacy refers to the appropriate handling of personal data—any information that relates to an identified or identifiable individual. 

  * Microsoft Entra
   It is a family of identity and Network Access Products.
   Covers: identity, governance, verified credentials, secure network access and identites for AI agents.

  * Microsoft Entra Product family
   * Zero Trust Access Controls
     * Microsoft Entra ID: It's a cloud-based identity and access management service that provides authentication, single sign-on (SSO), policy enforcement, and protection for users, devices, apps, and resources. If you use most of the Microsoft products such as Office 365, Azure or Dynamics CRM Online, you are already using Microsoft Entra ID. Non custom entra-Id domains are like: contoso.onmicrosoft.com
     * Microsoft Entra Domain Services: Entra ID for legate windows server software.
   * Secure access for employess: governance
    * Microsoft Entra Private Access: allows for private remote acess to company resources with no need for a VPN, like a printer for example.
    * Microsoft Entra Internet Access: allows and secure access fot web based and non web based SaaS.
    * Microsoft Entra ID Governance: simplifies identity and permissions management by automating access requests, assingments and reviews. It also helps protec critical assets via lifecycle management.
    * Microsoft Entra ID Protection: deals with risk identiry based risks, such as risky users and risky sign-ins. Can be used to create risk based policies, such as MFA obligation.
    * Microsoft Entra Verified ID: Issues credentials, digital signatures store at the devices and present them when needed

   * Secure Acces for partners
    * Microsoft Entra External ID: Safe access for costumer and partner facing apps

   * Secure Access in any cloud: 
    * Secure Entra Workload ID: allows workload identities - containers, applications, services that need authentication and authorization to interact with resources.

   * Secure Access for AI agents
    * Microsoft Entra Agent ID: authorizes and secures AI agents that need to interact with company resources.

   * How Microsoft Entra Products Work Together: The entra products wokr in layers. A new entry into an organization uses Entra ID to singgle sign-on to corporate apps. Governance then applies security policies to his acc, suhc as MFA. Protection evaluates each entry for risk and triggers strong authentication when needed. Internet Access allows for cloud and Internet resources. Private access eliminates the need for a VPN.

   * Microsoft Entra Licencing: 
    * Microsoft Entra ID Free: provided with basic Office and Azure subscriptions. Allows for basic reporting, self service password reset and user and group management.
    * Entra ID P1: conditional access, hybrid identity support and advanced group features. Included with Microsoft 365 E3, F1, F3, Enterprise Mobility + Security E3, and Microsoft 365 Business Premium.
    * Entra ID P2: risk based condiftional access, entra ID Protection and Proviledged Identity Management.  Included with Microsoft 365 E5 and Enterprise Mobility + Security E5.
    * Microsoft Entra Suit: licence that combines five entra products under a single offering, designed for organizations. s that want comprehensive identity and network access protection. A Microsoft Entra ID P1 subscription is required

   * Microsoft Entra admin center: allows for administrators to configure and manage all microsofot ID products.

Describe Microsoft Entra ID
 * Microsoft Entra ID is Microsoft's cloud-based identity and access management service.
  * Internal resources, such as apps on your corporate network and intranet, and cloud apps developed by your own organization.
  * External services, such as Microsoft 365, the Azure portal, and any SaaS applications used by your organization. 
  * Microsoft Entra ID can be syncronized with your existing on premisses Active Directory, as I already did before.
 
 * Identity Secure Store:
  * Entra ID has a score that it measures compliance with microsoft security policies 

 * Entra ID terminology
  * Tenant: Instance of Microsoft Entra ID in which information about a single organization resides, including users, groups, devices, and application registrations. A tenant also contains access and compliance policies for resources, such as applications registered in the directory. Each tenant  has a unique tenant ID and domain name such as contoso.onmicrosoft.com.
  * Directoty: The terms Microsoft Entra directory and Microsoft Entra tenant are often used interchangeably. The directory is a logical container within a Microsoft Entra tenant that holds and organizes the various resources and objects related to identity and access management including users, groups, applications, devices, and other directory objects.
  * Multi-tenant:  A multitenant organization is an organization that has more than one instance of Microsoft Entra ID (such as most I work with). 

 * Who uses Microsoft ENtra ID: most people that work with microsoft software. Developers use Microsoft Entra ID as a standards-based approach for adding single sign-on (SSO) to their apps, so that users can sign in with their preexisting credentials.

 * Types of Identities
  * There are three types of identities: human or user identities, the identities of physical devices, such as phones, desktops and IoT devices, and lastly, software based identities, such as apps, VM's, services and containers. These are workload identities.
     * User identities: represents people, such as employees and external users, such as customers or consultants. User identities can be classified by how they authenticate, such as internal or external, relative to the organization tenancy. Internal means that the organization has an account inside the orgranization. External means that he authenticates via en external Microsoft ID account, social network account or external account, such as google account.
      * User types: 
       * Internal member: typically considered employees of the organization. The object contained in the resources has UserType of Member.
       * External member: Object has UserType of Guest. Generally pertaning to guest, external users, providers, or people authenticatiing via some social network.
       * Internal Guest: This scenario is common in organizations consisting of multiple tenants. Members of a different company can authenticate inside a another company for example. UserType defined as member.
       * Internal Guest: This scenario exists when organizations set up internal Microsoft Entra accounts for external users such as distributors or vendors, but designate them as guests by setting the user object UserType to Guest. Now this is considered a legacy scenario.

       * Tenant: your organization's dedicated instance of microsoft entra ID, stores users, groups, devices and other resources. Acts as a security and administrative boundary, each tenant has a unique tenant ID and domain name.
       * Directory: logical container of the tenant, stores objects such as users, groups. Each tenatn only has one directory. A multitenant organization has more than one tenant inside   
       
  * Workload Identities: these are identities given to software workload. This exists because many times, software'll be needing credentials that are needed to access various resources, and from time to time, these accesses'll need to be given and/or revoqued. Microsoft Entra Workload ID takes care of this.
  * Service principals: Service principals are identities for applications. First to app must be registered to Microsoft Entra ID, then a service principal is created in each tenant where the application is used. The service principal enables core features such as authentication and authorization of the application to resources that are secured by the Microsoft Entra tenant.
  * Managed Identities: are a type of service principals. Automatically managed via Microsoft Entra ID eliminating the need for developers to manage credentials and  can be used without any extra cost.
   * There are two types of managed Identities: System-assigned and User-assigned.
    * System-assigned: Some Azure resources can be automatically assigned a identity tied to the lifecycle of the Azure resource. When the resource is deleted, the identity is deleted also.
    * User-assigned: You may also create a managed identity as a standalone Azure resource. Once you create a user-assigned managed identity, you can assign it to one or more instances of an Azure service. With user-assigned managed identities, the identity is managed separately from the resources that use it and deleting the resource does not delete the identity.

  * Agent Identity: literally identity for AI agents and their workloads. Agent identities support both attended scenarios, where the agent acts on behalf of a user, and unattended scenarios, where the agent operates autonomously. Microsoft Entra Agent ID is described in more detail in the next unit.

  * Device: 
  Microsoft Entra registered devices. The goal of Microsoft Entra registered devices is to provide users with support for bring your own device (BYOD) or mobile device scenarios.
   * Microsoft Entra joined. A Microsoft Entra joined device is a device joined to Microsoft Entra ID through an organizational account, which is then used to sign in to the device. Microsoft Entra joined devices are generally owned by the organization.
   * Microsoft Entra hybrid joined devices. Organizations with existing on-premises Active Directory implementations can benefit from the functionality provided by Microsoft Entra ID by implementing Microsoft Entra hybrid joined devices. These devices are joined to both your on-premises Active Directory and Microsoft Entra ID, and require an organizational account to sign in to the device.
  
  * Groups: Allow you to organize access to several objects at the same time. This aligns with the Zero Trust principle of limiting access to only those who need it. 
  Microsoft 365: A Microsoft 365 group, which is also often referred to as a distribution group, is used for grouping users according to collaboration needs.
  Security: A security group is the most common type of group and it's used to manage user and device access to shared resources.

* Describe Microsoft Entra Agent ID:
 * AI angents also need dedicated ID. While software work on hardcoded logic, AI agents might be less predictable.
  * Expanded attack surface: Since the agent freely interact with apps and other types of external systems, there are new pathways that can lead to attacks, such as prompt injections, that work on new ways.
  * Permission risks: Agents generally have broad permissions, so, it might access more that than necessary without proper controls.
  * Agent Sprawl: Uncontrolled expansion of agents across an organization, without adequate visibility, management, or lifecycle controls, can lead to security and compliance risks. Agents created for temporary purposes may remain in production indefinitely, with permissions that are rarely reviewed.

* How Microsoft Entra ID works:
  * Agent identity blueprints: serve as reusable templates that define e type or class of agents. It can even serve to hold the blue´rint to create more agents, making it very, very fast and agile to do so.
  * Agent identities: are individual blueprints to AI. Each identity has a unique identifier in Microsoft Entra ID, a display name and a sponsor, meaning a user or grouresponsible for the agent. They don't hold their own credentials, but requite the blueprint to as for  tokens on their behalf.

 * This blueprint-to-identity model enables centralized management while providing the flexibility needed for diverse AI agent deployment scenarios. Administrators can apply conditional access policies, disable permissions, or audit agents at scale through blueprint-based controls. Also Microsoft Entra Agent ID is platform agnostic, works on microsoft agents and also any kind of agent.

* Microsoft Authentication works on two scenarios, attended an unatended:
 * Atended: This agents acts on beahlf and with the guidance of a human user
 * Unatended: This agent has more authonomy

* Governance and Identity:
 * Conditional access: enables policy-based access controls and risk-based authentication specifically for agents. Administrators can create policies that evaluate agent risk before granting access.
 * Identity protection: provides real time threat detection and risk response for AI agents
 * Identity governance: provides lifecycle management, inclusind access assignment and compliance reporting.
 * Agent registry: centralized metadata management and secure agent discovery maintain visibility into all agents operating in their tenant.

* Describe hybrid identity: many businesses, and corporations are still a mixture of on-premises and cloud applications.
 * Microsoft’s identity solutions span on-premises and cloud-based capabilities. These solutions create a common identity for authentication and authorization to all resources, regardless of location. We call this hybrid identity.
 *  Hybrid identity
  * Inter-directory provisioning: provisioning an identity between two different directory service systems. The most common scenario is when an Active Directory user is also provisioned into Microsoft 365 ID.
  * Synchronization maches the cloud to the offline stuff.
  Microsoft Entra Cloud Sync is Microsoft's recommended synchronization tool for accomplishing hybrid identity. It uses a lightweight cloud provisioning agent that acts as a bridge between Microsoft Entra ID and Active Directory.

  Microsoft Entra Connect Sync is an earlier on-premises synchronization tool that's being replaced by Cloud Sync.

Security copilot: Basicamente um copylot que pode ajudar em várias funções de segurança 
Introdução ao Microsoft Security Copilot, uma ferramenta de análise de segurança baseada em nuvem e alimentada por IA que permite que os analistas respondam rapidamente às ameaças, processem sinais na velocidade do computador e avaliem os riscos mais rapidamente do que seria possível.

Investigue e corrija ameaças de segurança - obtenha contexto para incidentes para classificar rapidamente alertas de segurança complexos em resumos acionáveis e remedie mais rapidamente com orientação de resposta passo a passo
Crie consultas na Linguagem de Consulta Kusto (KQL) ou analise scripts suspeitos — elimine a necessidade de escrever manualmente scripts na linguagem de consulta ou de realizar engenharia reversa em scripts de malware, utilizando a tradução em linguagem natural para permitir que cada membro da equipe execute tarefas técnicas.
Entenda os riscos e gerencie a postura de segurança da organização - obtenha uma visão ampla do seu ambiente com riscos priorizados para descobrir oportunidades de melhorar a postura com mais facilidade
Solucione problemas de TI mais rapidamente - sintetize informações relevantes rapidamente e receba insights acionáveis para identificar e resolver problemas de TI rapidamente
Definir e gerenciar políticas de segurança - definir uma nova política, fazer referência cruzada com outras para verificar conflitos e resumir as políticas existentes para gerenciar o contexto organizacional complexo de forma rápida e fácil
Configure fluxos de trabalho de ciclo de vida seguros - crie grupos e defina parâmetros de acesso com orientação passo a passo para garantir uma configuração perfeita para evitar vulnerabilidades de segurança
Desenvolver relatórios para as partes interessadas - obter um relatório claro e conciso que resuma o contexto e o ambiente, questões em aberto e medidas de proteção preparadas para o tom e a linguagem do público do relatório

Funciona como um LLM baseado na OpenAI, dados não são utilizados para treinar modelos de IA sendo tratados como privativos
Sessão – uma conversa específica no Copilot. O Copilot mantém o contexto em uma sessão.
Prompt – Uma instrução ou pergunta específica em uma sessão. Um usuário insere um prompt na barra de prompts.
Funcionalidade – uma função que o Copilot usa para resolver parte de um problema. Uma capacidade às vezes pode ser referida como uma habilidade.
Plug-in – um conjunto de funcionalidades de um recurso específico.
Espaço de trabalho- os espaços de trabalho do Copilot são ambientes de trabalho separados do Copilot dentro do locatário no qual sua instância do Copilot está operando.
Agentes - Os agentes do Microsoft Security Copilot são ferramentas de IA que gerenciam tarefas de TI e segurança de forma autônoma, melhorando a resposta a ameaças, reduzindo cargas de trabalho manuais e melhorando a eficiência em operações de segurança cibernética em escala.
Orchestrator – sistema do Copilot para compor recursos em conjunto para responder ao prompt de um usuário.

 Workspaces

Os espaços de trabalho do Copilot são ambientes de trabalho separados do Copilot dentro do locatário no qual sua instância do Copilot está operando.

Para ajudá-lo a entender melhor o conceito de workspaces, usamos a analogia da casa com várias salas. Cada sala é configurada para ser otimizada para sua função e para as pessoas que usam essa sala. Quando alguém entra na casa, pode ter acesso a alguns quartos, mas não a outros.
 Orquestrador

O orquestrador é o sistema do Copilot para compor recursos em conjunto para responder ao prompt de um usuário. Essa função é ilustrada em mais detalhes na unidade subsequente, que descreve como o Copilot processa solicitações de prompt.

Enviar um prompt: o processo começa quando um usuário envia um prompt na barra de prompts.

Orquestrador: o Security Copilot envia as informações para o backend do Copilot conhecido como orquestrador. O orquestrador é o sistema do Copilot para compor recursos em conjunto para responder à solicitação de um usuário. Ele determina o contexto inicial e constrói um plano usando todos os recursos disponíveis (habilidades).

Contexto de criação: depois que um plano é definido e criado, o Copilot executa esse plano para obter o contexto de dados necessário para responder ao prompt.

Plug-ins: durante a execução do plano, o Copilot analisa todos os dados e padrões para fornecer insights inteligentes. Isso inclui a análise de todos os plug-ins e fontes de dados, habilitados e disponíveis para o Copilot.

Respondendo: o Copilot combina todos os dados e o contexto e utiliza o poder de seu LLM avançado para compor uma resposta que utiliza uma linguagem que faça sentido para um ser humano.

Resposta: antes que a resposta possa ser enviada de volta ao usuário, o Copilot formata e analisa a resposta como parte do compromisso da Microsoft com a IA responsável.

Recebimento da resposta: o processo culmina com o usuário recebendo a resposta do Copilot.


Log do processo: todo o processo descrito acima fica salvo em um LOG do processo. 
Descreva os elementos de um prompt eficaz

Meta – informações específicas relacionadas à segurança de que você precisa
Contexto – por que você precisa dessas informações ou como usá-la
Expectativas – formato ou público-alvo para o qual você deseja que a resposta seja adaptada
Origem – informações conhecidas, fontes de dados ou plug-ins que o Copilot deve usar

Descrever como habilitar o Microsoft Security Copilot:
Identificar sua categoria de cliente
Provisionar capacidade do Copilot (se necessário)
Configurar o ambiente padrão
Atribuir permissões de função

Identificar sua categoria de cliente: Microsoft 365 E5 e E7 - O Security Copilot está incluído com sua licença do Microsoft 365 E5 e E7 não é necessário configuração do Azure nem provisionamento manual de capacidade.
Para cliente não Microsoft do E5 e E7: Se o Security Copilot não estiver incluído na sua licença, você deverá seguir as etapas de integração manual

Para os clientes não Microsoft 365 E5 e E7, o Security Copilot funciona com uma capacidade provisionada e um modelo de excedente. A capacidade aprovisionada é faturada por hora, enquanto a capacidade de utilização excedida é faturada na utilização. pode alocar uma quantidade de utilização excedida para garantir que existem SCUs adicionais disponíveis quando as unidades aprovisionadas inicialmente estão esgotadas durante picos inesperados de cargas de trabalho.

Antes que os usuários possam começar a usar o Copilot, os administradores precisam provisionar e alocar a capacidade. Para provisionar a capacidade:

    Você deve ter uma assinatura do Azure.

    Você precisa ser um proprietário do Azure ou colaborador do Azure, em um nível de grupo de recursos, no mínimo.

    Você precisa ser um Administrador de Segurança ou superior no locatário onde o Security Copilot está sendo integrado.

Microsoft Entra ID Governance

Leverages AI driven insights to help organizations automatically ensure that the right people have access to the right stuff inside a clouda




asasas
   


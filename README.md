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

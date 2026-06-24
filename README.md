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

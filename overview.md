# Tech Overview

Most projects on the Coronasafe Network are dockerized and can be easily deployed on various container orchestration services for scalability. This documentation contains instructions for setting up our Care Network project in a production environment on the Kubernetes service provided by Amazon \(AWS EKS\). The same principles can be applied to other projects under the Coronasafe Network.

For help in setting up a local version of the project for development, see [Setting up the project locally](local.md)

Before deployment make sure that both the care and care\_fe repos from the Coronasafe Network Github Organization are forked into the required organization's Account. This step makes it easier for the projects to remain synced, The Care project will keep receiving security updates and features which can be easily synced up with the deployment fork. Any Security issue must be reported to the Coronasafe Network admin before being implemented in any forks. 


# No Silver Bullet: Use the right architecture

Notes:

* Architecture Characteristics and Goals:
  * Layers (Logical Architecture):
    * Maintainability
    * Testability
    * Agility
    * Cost Optimization
  * Tiers or Services (Physical Architecture):
    * Scalability
    * Deployment
    * Faut tolerance
    * Reliability/Availability
  * Cross-Cutting Concerns:
    * Accessibility
    * Security
    * Usability
    * Privacy
  * For example, Microservices is a deployment model.
* Separation of Concerns (**THE KEYPOINT OF MORE MAINTAINABLE SOFTWARE**):
  * Interface Layer: Every application has one.
  * Interface Control Layer: Some code that is controlling the interface (like MVC).
  * Business Layer: Why does the application even exists if you don't have it.
  * Data Access Layer: The way to access the data storage (like an ORM).
  * Data Storage: The actual storage.
  * Orthogonal Concerns: Security and logging and other stuff.
* N-Layer Maps to N-Tier:
  * 1-Tier not separating anything (good for offline use).
  * 2-Tier was good, but security is kinda shit (secrets are on the clients device).
  * 3-Tier A doesn't have the cool user validation because all the logic is on the server.
  * 3-Tier B is a better 2-tier application, because the security of the database is on the server.
  * 3-Tier C has one DLL with the business code, but deployed on both the client and the server.
  * Web is old and super cheap.
* N-Layer Maps to Services:
  * Every microservice is an App.
  * And each service has Separation of Concerns.
* Service application is a nonsequitur:
  * If an app is composed of services then:
    * An app is composed of apps
    * Clearly nonsense.
  * Service-based system:
    * An app is an app.
    * A service is an app.
    * A system is composed of services.
    * Some apps serve users (called apps).
    * Some apps serve other apps (called services).
* App Boundaries:
  * Inside an app: Trust across layers and tiers.
  * Between apps: apps are basically black boxes.
* All calls are RPC calls, not a lot of applications do actual REST.

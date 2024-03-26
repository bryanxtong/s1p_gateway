This version is using HTTP-Based Spring Cloud Kubernetes Discovery Server and Spring Cloud Kubernetes Config Server and support load balance for apps
# Deploy Spring Cloud Discovery Server(resources/spring-cloud-kubernetes-discoveryserver.yml)
# Deploy Spring Cloud Config Server(resources/spring-cloud-kubernetes-configserver.yml)
# Deploy Spring Cloud Configuration Watcher(resources/spring-cloud-kubernetes-configuration-watcher.yml)

# S1P :: Gateway
Based on the new Spring Cloud Gateway, configured to use the Spring Cloud Kubernetes Discovery and Config modules to automatically register routes to (k8s) services matching with the following SPEL Filter:
**metadata.labels['s1p'] = true**  

Only if the services contain this label will be automatically registered and the gateway will forward requests to them.

```
       <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
       </dependency>
       <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-kubernetes-discoveryclient</artifactId>
       </dependency>
       <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-loadbalancer</artifactId>
       </dependency>
       <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
       </dependency>
``` 

You can also find inside the [charts/s1p-gateway/templates](charts/s1p-gateway/templates) directory the descriptors 
needed to deploy this gateway and to grant access to the Kubernetes APIs. The Role, RoleBinding and Services accounts
are configured to enable the deployed container to access the Kubernetes APIs from inside a Pod. 


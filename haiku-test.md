# **V3 TESTS FOR PRODUCTION SUPPORT**


### NODE DEPLOYMENT AND CONFIGURATION

> New node group deployment

  - Deploy a new node grroup with the desired configuration.
    - Nodes are created and registered with the cluster in the ready state.
    - Nodes meet the specified configuration in the claim file.
    - Workloads can be scheduled on the new nodes.

> Node autoscaling validation

  - Configure auto-scaling for a node group and validate scale-up and scale-down events.
    - Nodes scale up and down based on workload demand.
    - New nodes are automatically registered and ready for workload scheduling.

> Node Configuration Validation

  - Validate the configuration of newly deployed nodes as per the claim file.
    - Nodes are provisioned with the correct configuration.
    - Security groups, disk size, and instance types match the specified requirements.

> Networking Configuration Validation

  - Ensure the nodes are correctly configured for networking.
    - Nodes can communicate with the cluster network, other nodes, and external resources.
    - Pods running on the nodes can resolve DNS.

> AMI Validation

  - Validate that nodes are using the correct Amazon Machine Image as per claim file.
    - Nodes are deployed with the correct AMI as per the claim file.
    - Nodes include required configurations, tools, and patches.

> Testing High Availability

  - Validate high availability of workloads during node failures or rollouts.
    - Workloads are rescheduled to healthy nodes without downtime.
    - The cluster maintains stability during node failures.

> Validating Node Security

  - Ensure nodes are configured with proper security groups, IAM roles, and access controls.

> Disk and Storage Configuration

  - Validate the disk size and volume configuration for newly deployed nodes.
    - Disk size and type match the node group configuration.
    - Applications requiring persistent storage can mount and use volumes.

> Node Group Rollout Testing

  - Perform a rolling update of a node group to apply updated configurations or replace nodes.

### Pod Scheduling and Application Health

> Basic Pod Scheduling

  - Test the basic scheduling of pods on available nodes in the cluster.
    - Pods are scheduled on nodes with sufficient resources.
    - All pods are in running state without delays.

> Node Affinity and Anti-Affinity Scheduling

  - Validate pod scheduling based on node affinity and anti-affinity rules.
    - Pods with nodeAffinity rules are scheduled only on matching nodes.
    - Pods with antiAffinity rules are distributed across nodes as specified.

> Pod Scheduling with Taints and Tolerations

  - Ensure that pods are scheduled only on nodes with matching tolerations for their taints.
    - Pods without tolerations are not scheduled on tainted nodes.
    - Pods with tolerations are scheduled successfully on tainted nodes.


> Application Health Post-Scaling

  - Validate application health and pod scheduling during scale-up and scale-down events.
    - Application scales up or down without downtime or performance degradation.
    - Newly scheduled pods are healthy and functional.

> Application Health During Rolling Updates

  - Perform a rolling update for an application and validate health and pod scheduling.
    - Pods are updated one at a time.
    - The application remains healthy and accessible throughout the update.

> Rescheduling During Node Failures

  - Test application health and pod rescheduling during node failures or cordoning.
    - Pods are rescheduled to healthy nodes without downtime.
    - Application remains accessible and functional.

> Multi-Zone Scheduling and Availability

  - Validate that workloads are distributed across availability zones for high availability.
    - Pods are distributed evenly across nodes in different availability zones.
    - No single AZ failure disrupts application availability.

> Application Readiness and Liveness Probes

  - Validate that applications are monitored for health using readiness and liveness probes.
    - Readiness probes ensure that traffic is routed only to healthy pods.
    - Liveness probes detect and restart unhealthy pods.

> Network Policies and Pod Communication

  - Test pod-to-pod and pod-to-service communication under different network policies.
    - Pods comply with defined network policies for communication.
    - Unauthorized communication is blocked.

> Application Health During Resource Exhaustion

  - Validate application behavior when a node is under high CPU or memory load.
    - Application remains functional and responsive under resource pressure.
    - Resource limits prevent excessive resource usage by individual pods.

> Application Performance Post-Rescheduling

  - Validate application performance after pods are rescheduled to different nodes.
    - Applications maintain consistent performance post-rescheduling.
    - No data loss or connectivity issues occur during rescheduling.


### **PIPELIINEE VALIDATION**

> Validate Application Deployment via ArgoCD

  - Test an end-to-end application deployment using ArgoCD.
    - Application is deployed successfully to the target environment.
    - ArgoCD reflects the correct application sync status (Healthy and Synced).

> Infrastructure Provisioning via Crossplane**

  - Test infrastructure provisioning pipelines using Crossplane to create cloud resources.
    - Crossplane provisions cloud resources (e.g., RDS, S3) as defined in the configuration.
    - Resources meet the specified configuration (e.g., size, region, tags).

> Deployment Rollback Validation**

  - Test rollback functionality for application deployments.
    - Rollback restores the application to the previous stable version.
    - Application remains functional and healthy post-rollback.

> Pipeline Trigger Validation

  - Validate that pipeline triggers execute deployments or provisioning workflows as intended.
    - Pipelines are triggered automatically based on events (e.g., Git commit, pull request).
    - Deployment is initiated without manual intervention.


> Validation of Addon Upgrades
 
  - Test the pipeline’s ability to upgrade Kubernetes addons (e.g., CoreDNS, kube-proxy, VPC CNI).
    - Addons are upgraded successfully without affecting the cluster’s functionality.
    - New versions are reflected in the cluster.


> Validate Pipeline Error Handling
  
  - Simulate errors during the pipeline run to test error handling and logging mechanisms.
    - Pipeline identifies and reports errors clearly.
    - Partial or faulty deployments are rolled back automatically if configured.


  - Test deployment workflows across multiple environments (e.g., dev, staging, prod).
    - Pipelines deploy to the correct environments based on branch or configuration.
    - Environment-specific settings are applied correctly.


> Performance Testing Pipeline
 
  - Validate that pipelines execute performance tests on applications before production deployment.
    - Performance tests are executed successfully, and results are reported.
    - Deployment proceeds only if performance thresholds are met.


> ArgoCD Sync Policy Validation
  
  - Test the behavior of applications with different sync policies (manual vs. automatic).
    - Manual sync requires explicit user approval for changes.
    - Automatic sync deploys changes without manual intervention.

  
  - Test security aspects of the pipeline, including access controls and secret management.
    - Pipelines do not expose sensitive data (e.g., secrets, credentials).
    - Unauthorized users cannot trigger or modify pipelines.


> Validate Resource Cleanup**
  
  - Test that the pipeline cleans up unused or temporary resources after deployment or testing.
    - Temporary resources (e.g., test databases, staging environments) are deleted after use.
    - No orphaned resources remain in the environment.


> Validate Rollout Strategy**
  
  - Test the pipeline’s rollout strategy (e.g., blue/green, canary).
    - Applications are deployed using the specified rollout strategy.
    - Rollout transitions are smooth, with no downtime or errors.


### **CONFIGURATION AND CODE QUALITY** 

>> YAML and Helm Chart Validation**
  
  - Validate Kubernetes YAML manifests and Helm charts for syntax, schema compliance, and best practices.
    - All manifests are syntactically correct and follow Kubernetes schema definitions.
    - Best practices (e.g., resource requests/limits, labels, annotations) are adhered to.



### **2. Secrets Management Validation**
 - Ensure secrets are securely stored and managed, avoiding hardcoded secrets in code or manifests.

  -
  - Secrets are stored securely (e.g., AWS Secrets Manager, Kubernetes Secrets).
  - No secrets are hardcoded in manifests or version control.



### **3. Configuration Drift Validation**
 - Ensure configurations in the cluster match those in the Git repository (GitOps compliance).

  -
  - Configurations in the cluster are in sync with the Git repository.
  - Any drift is detected and corrected automatically or manually.


### **4. Resource Configuration Validation**
 - Validate resource configurations such as CPU, memory, and replica counts.

  -
  - All deployments have appropriate resource requests and limits.
  - Workloads are scaled based on expected traffic or workload demands.



### **5. Code Quality for Infrastructure as Code (IaC)**
 - Validate Terraform, Crossplane, or other IaC configurations for syntax and best practices.

  -
  - IaC code is syntactically correct and adheres to organizational standards.
  - Changes are reviewed and tested before deployment.



### **6. Validation of Kubernetes Addons Configurations**
 - Validate the configurations of Kubernetes addons (e.g., CoreDNS, VPC CNI, kube-proxy).

  -
  - Addon configurations are compatible with the cluster and workloads.
  - Updates to addons do not break cluster functionality.


### **7. Version Control and Branch Management**
 - Validate the branching strategy and ensure configuration changes are tracked and reviewed.

  -
  - Configuration changes follow a defined branching strategy (e.g., Git Flow).
  - All changes are reviewed and approved before merging.



### **8. Compliance with Organizational Policies**
 - Validate that configurations and code comply with organizational policies and industry standards.

  -
  - Configurations adhere to security, naming, and tagging policies.
  - Compliance violations are identified and remediated.



### **9. Testing Error Handling and Rollback**
 - Validate the error handling and rollback capabilities in configurations and deployments.

  -
  - Pipelines detect and stop on configuration errors.
  - Rollback restores the previous state without manual intervention.



### **10. Performance Testing for Configurations**
 - Test the impact of configuration changes on application performance.

  -
  - Configuration changes (e.g., scaling, resource updates) improve or maintain performance.
  - No degradation is observed after applying changes.



### **11. Logging and Monitoring Configuration Validation**
 - Ensure logging and monitoring configurations capture the necessary metrics and logs.

  -
  - Application and infrastructure logs are collected and accessible.
  - Monitoring dashboards display accurate metrics for troubleshooting.



### **12. Security Validation for Configurations**
 - Validate that configurations enforce security best practices (e.g., RBAC, network policies).

  -
  - Configurations restrict access to sensitive resources and namespaces.
  - Applications and pods comply with security policies.




--------------------------------------------

**Rollback and Recovery** is a critical aspect of maintaining stability and resilience in your EKS clusters when using AWS EKS, Addons, Crossplane, and ArgoCD. It ensures that infrastructure and applications can revert to a stable state after failures or incorrect changes. Below are the **key validation areas**, **scenarios**, expected outcomes, and validation steps for rollback and recovery:

---

### **1. Application Deployment Rollback**
 - Rollback an application to a previous stable version after a failed deployment.

  -
  - The application is reverted to the previous version.
  - Service remains available during and after the rollback.
  


### **2. Addon Rollback**
 - Rollback an addon (e.g., CoreDNS, VPC CNI) to a previous version after an upgrade failure.

  -
  - The addon is reverted to the stable version.
  - Cluster functionality (e.g., DNS resolution, networking) is restored.



### **3. Crossplane Resource Recovery**
 - Restore a cloud resource provisioned via Crossplane after a configuration or deletion error.

  -
  - The deleted or misconfigured resource is recreated with the correct state.
  - Applications dependent on the resource recover without data loss.



### **4. Node Failure Recovery**
 - Simulate a node failure and validate workload rescheduling to healthy nodes.

  -
  - Pods running on the failed node are rescheduled to healthy nodes.
  - No data loss or prolonged downtime for applications.



### **5. Cluster Rollback**
 - Rollback a cluster-level configuration change (e.g., cluster version, node group configuration).

  -
  - Cluster functionality is restored to the previous stable state.
  - Workloads remain unaffected during the rollback.



### **6. ArgoCD GitOps Rollback**
 - Rollback an incorrect configuration or deployment via ArgoCD.

  -
  - The cluster configuration is restored to match the previous Git repository state.
  - No manual intervention is required post-rollback.



### **7. Persistent Volume Recovery**
 - Restore persistent volumes (PVs) or claims (PVCs) after accidental deletion or corruption.

  -
  - Data is recovered from snapshots or backups.
  - Applications regain access to their data stores.



### **8. Application State Recovery**
 - Restore application state after a deployment or runtime failure.

  -
  - Applications return to their last known good state.
  - No data loss or downtime occurs.



### **9. Pipeline Recovery**
 - Recover from a failed CI/CD pipeline deployment.

  -
  - The pipeline resumes or reverts to a stable state.
  - No partial or broken configurations are applied to the cluster.



### **10. Disaster Recovery**
 - Recover the cluster from a complete failure (e.g., AWS region outage, cluster deletion).

  -
  - The cluster is recreated in a new region or from backups.
  - Applications and data are restored with minimal downtime.



---------------------------

**Performance Testing** from an infrastructure point of view focuses on validating the stability, scalability, and resource efficiency of the EKS cluster and its associated components (AWS EKS, Addons, Crossplane, and ArgoCD). Below are the **key validation areas**, **scenarios**, **expected outcomes**, and **validation steps** for performance testing.

---

### **1. Cluster Autoscaling Under Load**
 - Test the cluster’s ability to scale nodes up and down under heavy workload demand.

  -
  - Nodes are added automatically when workloads require more resources.
  - Nodes are terminated when they are no longer needed, adhering to scale-down thresholds.
  - No downtime for workloads during scaling operations.



### **2. Pod-to-Pod Networking Performance**
 - Measure the latency and throughput of communication between pods across nodes.

  -
  - Intra-cluster latency is within acceptable limits (e.g., <1ms for same-node communication, <10ms for inter-node communication).
  - Network throughput meets application requirements.



### **3. Storage Performance**
 - Evaluate the I/O performance of storage solutions used in the cluster (e.g., EBS volumes, EFS).

  -
  - Read/write IOPS and throughput align with the storage type specifications (e.g., gp3, io1).
  - Stateful applications (e.g., databases) maintain consistent performance under load.



### **4. Application Scalability**
 - Test the application’s ability to scale horizontally (number of replicas) and vertically (resource allocation).

  -
  - Applications scale up and down without downtime or performance degradation.
  - Resource usage scales linearly with the workload.



### **5. Addon Performance Validation**
 - Measure the performance overhead of Kubernetes addons (e.g., CoreDNS, kube-proxy, VPC CNI).

  -
  - Addons consume minimal resources (CPU, memory) relative to the cluster size.
  - Addons do not introduce significant latency or errors.



### **6. Application Response Time Under Load**
 - Validate application performance (response time, throughput) under various levels of traffic.

  -
  - Application response times remain within acceptable limits (e.g., <100ms under normal load, <500ms under peak load).
  - Throughput scales with traffic volume.



### **7. Crossplane Resource Provisioning Latency**
 - Test the latency of provisioning cloud resources (e.g., RDS, S3) using Crossplane.

  -
  - Resources are provisioned within the expected time frame (e.g., <2 minutes for RDS, <1 minute for S3).
  - Resource configuration matches the specifications in the manifests.



### **8. Ingress Controller Performance**
 - Test the performance of the Ingress controller under heavy traffic.

  -
  - Ingress handles traffic efficiently without introducing latency or errors.
  - TLS termination, routing, and load balancing work correctly under load.



### **9. API Server Responsiveness Under Load**
 - Measure the responsiveness of the Kubernetes API server under heavy API traffic.

  -
  - API server latency remains low (<500ms for common operations like `kubectl get`).
  - No API errors or timeouts during high load.



### **10. Multi-Zone and Multi-Region Performance**
 - Test cluster performance and application availability across multiple availability zones or regions.

  -
  - Applications remain highly available during zonal outages.
  - Latency between zones or regions remains within acceptable limits.



### **11. Recovery Time Objective (RTO) and Recovery Point Objective (RPO) Testing**
 - Test the recovery time and data loss during infrastructure or application failures.

  -
  - Cluster and applications recover within defined RTO/RPO thresholds.
  - No significant data loss during recovery.


### **12. Monitoring and Alerting Performance**
 - Validate the performance of monitoring and alerting systems under high traffic or workload.

  -
  - Monitoring tools capture all relevant metrics without delays.
  - Alerts are triggered within expected thresholds (e.g., <1 minute).



-----------------------------------------

**Connectivity Testing** ensures that the infrastructure components of your EKS cluster, including AWS EKS, Addons, Crossplane, and ArgoCD, can communicate effectively with each other, within the cluster, and with external systems. Below are the **key validation areas**, **scenarios**, expected outcomes, and validation steps for connectivity testing from an infrastructure point of view.

---

### **1. Pod-to-Pod Connectivity**
 - Validate connectivity between pods within the same namespace and across namespaces.

  -
  - Pods can communicate within the same namespace and across namespaces as allowed by network policies.
  - No packet loss or significant latency in communication.



### **2. Pod-to-Service Connectivity**
 - Test connectivity between pods and Kubernetes services (ClusterIP, NodePort, LoadBalancer).

  -
  - Pods can reach services of all types without errors.
  - DNS resolution of services works correctly.



### **3. External Connectivity (Egress)**
 - Validate pod connectivity to external systems and the internet.

  -
  - Pods can reach external endpoints if allowed by network policies and security groups.
  - No packet loss or connection errors when accessing external services.



### **4. Service-to-Database Connectivity**
 - Test connectivity between workloads and databases provisioned via Crossplane (e.g., RDS, DynamoDB).

  -
  - Services can connect to the database over the expected port (e.g., 3306 for MySQL, 5432 for PostgreSQL).
  - Connection latency is within acceptable limits, and no timeouts occur.



### **5. Crossplane Resource Connectivity**
 - Validate connectivity between Crossplane-managed resources and the cluster or external systems.

  -
  - Provisioned resources (e.g., S3, RDS) are accessible from the cluster.
  - No misconfigurations in IAM roles, security groups, or endpoints.



### **6. ArgoCD-to-Git Repository Connectivity**
 - Validate that ArgoCD can connect to and sync with the configured Git repositories.

  -
  - ArgoCD can successfully authenticate with the Git repository and pull configurations.
  - Sync operations complete without errors.



### **7. Node-to-Pod Connectivity**
 - Test connectivity between nodes and pods, especially for workloads requiring direct node access.

  -
  - Nodes can communicate with the pods running on them or other nodes.
  - No connectivity issues during workload execution.



### **8. Ingress Connectivity**
 - Validate external connectivity to workloads via Ingress controllers (e.g., NGINX, ALB).

  -
  - Ingress routes traffic to the correct backend service.
  - TLS termination, if configured, works as expected.



### **9. Multi-Zone Connectivity**
 - Test connectivity between pods and services across multiple availability zones.

  -
  - Pods in different zones can communicate seamlessly.
  - Cross-zone latency remains within acceptable limits.



### **10. Network Policies Validation**
 - Validate that network policies enforce communication restrictions correctly.

  -
  - Pods adhere to the rules defined in the network policies.
  - Unauthorized communication is blocked.



### **11. Monitoring and Alerting for Connectivity Issues**
 - Validate monitoring and alerting systems to detect connectivity problems.

  -
  - Alerts are triggered for connectivity issues within the cluster.
  - Monitoring dashboards display real-time connectivity metrics.



### **12. External Traffic Egress Validation**
 - Test external traffic routing via NAT Gateway, Internet Gateway, or VPC Endpoints.

  -
  - External traffic routes correctly through the configured gateways or endpoints.
  - No unauthorized traffic leaves the VPC.


------------------------------------

Upgrade validation in an AWS EKS environment with Addons, Crossplane, and ArgoCD involves verifying that the cluster and its components remain functional, stable, and meet performance benchmarks after upgrades. Below are key scenarios for **upgrade validation**, their **expected outcomes**, and corresponding **validation steps**:

---

### **1. EKS Cluster Version Upgrade**
 - Upgrade the Kubernetes version of the EKS control plane and worker nodes.

  -
  - Control plane upgrades successfully with no downtime.
  - Worker nodes upgrade seamlessly, and all workloads continue functioning.
  - All APIs and workloads are compatible with the upgraded Kubernetes version.



### **2. Add-on Version Upgrade**
 - Upgrade Kubernetes add-ons (e.g., CoreDNS, kube-proxy, VPC CNI plugin).

  -
  - Add-ons upgrade successfully without breaking cluster functionality.
  - Upgraded add-ons maintain compatibility with the Kubernetes version and workloads.



### **3. ArgoCD Upgrade**
 - Upgrade the ArgoCD application and ensure synchronization with Git repositories continues seamlessly.

  -
  - ArgoCD upgrades without losing connectivity to Git repositories.
  - Sync operations and application deployments work as expected.



### **4. Crossplane Upgrade**
 - Upgrade Crossplane and ensure resource provisioning functionality remains intact.

  -
  - Crossplane upgrades successfully and continues managing cloud resources without issues.
  - Provisioned resources remain unaffected.



### **5. Ingress Controller Upgrade**
 - Upgrade ingress controllers (e.g., NGINX, ALB) to ensure continued traffic routing.

  -
  - Ingress controllers upgrade successfully without disrupting traffic.
  - TLS termination and routing rules work as expected post-upgrade.



### **6. Storage Upgrade Validation**
 - Upgrade storage components (e.g., EBS CSI driver) and validate data integrity and performance.

  -
  - Storage upgrades without data loss or corruption.
  - Applications using storage continue to function normally.


### **7. Network Policy Validation Post-Upgrade**
 - Validate network policies after upgrading the VPC CNI plugin or Kubernetes.

  -
  - Network policies continue to enforce traffic restrictions correctly.
  - No unintended traffic flows within or outside the cluster.


### **8. API Server and CRD Compatibility**
 - Test API server compatibility with custom resources (CRDs) and ensure applications using CRDs continue functioning.

  -
  - API server upgrades successfully and continues serving requests for CRDs.
  - No deprecation warnings or errors in logs.



### **9. Application Compatibility Testing**
 - Validate that workloads (stateful and stateless) function correctly after upgrades.

  -
  - Applications remain stable with no crashes or performance degradation.
  - Stateful applications maintain data integrity.



### **10. Monitoring and Alerting Validation**
 - Ensure monitoring and alerting systems (e.g., Prometheus, CloudWatch) function correctly post-upgrade.

  -
  - Metrics collection and alerting systems continue to work without interruptions.
  - Dashboards display accurate data.



-------------------

Changing the instance types in your EKS cluster involves ensuring that the new instance types are compatible, efficient, and do not cause disruption to running workloads. Below are key scenarios, expected outcomes, and validation steps for **instance type change validation**:

---

### **1. Node Group Migration to New Instance Type**
 - Change the instance type of an existing node group and ensure workloads migrate seamlessly.

  -
  - New nodes with the updated instance type are created.
  - Existing workloads are rescheduled to the new nodes without disruption.
  - Old nodes are drained and terminated gracefully.



### **2. Resource Compatibility Testing**
 - Verify that the new instance type supports all existing workloads and resource requirements.

  -
  - Workloads are scheduled successfully on the new instance type.
  - No resource contention or unexpected performance issues arise.



### **3. Performance Benchmarking**
 - Assess the performance of critical workloads on the new instance type.

  -
  - Performance benchmarks (e.g., latency, throughput) are within acceptable limits.
  - The new instance type provides comparable or better performance than the old type.



### **4. Networking Validation**
 - Ensure networking components (e.g., VPC CNI, ingress, egress) function correctly on the new instance type.

  -
  - New nodes can connect to the cluster network, other nodes, and external endpoints.
  - No disruption to pod-to-pod communication or ingress/egress traffic.


### **5. Pod Affinity/Anti-Affinity Validation**
 - Verify that pod affinity and anti-affinity rules work correctly with the new instance type.

  -
  - Pods are scheduled based on defined affinity/anti-affinity rules.
  - No scheduling conflicts or unexpected placements occur.



### **6. Scaling Behavior Validation**
 - Test cluster scaling with the new instance type (both upscaling and downscaling).

  -
  - Cluster scales up and down based on workload demands.
  - No delays in node provisioning or pod scheduling.



### **7. Cost Efficiency Validation**
 - Assess the cost impact of moving to the new instance type.

  -
  - New instance type meets performance requirements with lower or acceptable cost.
  - No unexpected resource over-provisioning or wastage.



> Add-on Compatibility Validation
  
  - Validate that Kubernetes add-ons (e.g., CoreDNS, VPC CNI) function correctly on the new instance type.
    - All add-ons remain functional and compatible with the new instance type.
    - No disruptions to cluster networking, DNS resolution, or logging.


> Storage Compatibility Validation
  
  - Ensure EBS volumes and other storage solutions are compatible with the new instance type.
    - Storage volumes attach and function correctly on the new instance type.
    - No data loss or I/O issues occur during the transition.


> Failover and High Availability Testing
  
  - Simulate node failures with the new instance type and verify failover behavior.
    - Workloads are rescheduled to healthy nodes without disruption.
    - Cluster maintains high availability during node failures.



> Security and IAM Validation
  
  - Validate that IAM roles and security configurations are correctly applied to the new instance type.
    - New nodes have the correct IAM roles and permissions.
    - Security groups allow required traffic without unnecessary exposure.


-----------------------------------

### **AMI ID update**

> Node Group AMI Update
  
  - Update the AMI ID for an existing managed or self-managed node group.
    - Nodes with the new AMI are created and added to the cluster.
    - Existing workloads migrate seamlessly to the new nodes without disruption.
    - Old nodes are drained and terminated gracefully.


>> Compatibility Testing
  
  - Verify that the new AMI is compatible with the Kubernetes version and installed add-ons.
    - New nodes run without issues, and all add-ons function as expected.
    - No errors are reported in node or system logs.



> Workload Rescheduling
  
  - Test the rescheduling of existing workloads onto nodes with the new AMI.
    - Workloads are rescheduled without errors or downtime.
    - Application performance remains consistent after rescheduling.



> Security Patches and Updates Validation
 
  - Ensure that the new AMI includes the required security patches and updates.
    - New AMI resolves all previously identified vulnerabilities.
    - Nodes pass security and compliance scans.


> Networking Validation
  
  - Test networking functionality on nodes with the new AMI, including VPC CNI plugin and ingress/egress traffic.
    - Pods can communicate internally within the cluster and externally to the internet.
    - No disruptions to ingress/egress traffic flows.


> Storage Compatibility
  
  - Ensure storage solutions (e.g., EBS volumes, EFS, PVCs) work correctly with the new AMI.
    - Storage volumes are correctly attached to nodes with the new AMI.
    - No data loss or I/O issues occur during the update.



> Autoscaling and Scaling Down
 
  - Validate autoscaling and node scaling behavior with the new AMI.
    - Cluster scales up and down as expected, adding and removing nodes with the updated AMI.
    - Pods are rescheduled to new nodes during scaling operations.



> Add-on Compatibility Testing
  
  - Verify that Kubernetes add-ons (e.g., CoreDNS, kube-proxy, VPC CNI) remain functional after the AMI update.
    - Add-ons operate without errors or performance degradation.
    - Logs for add-on pods show no compatibility issues.



> Performance Testing
  
  - Benchmark the performance of nodes with the new AMI compared to previous nodes.
    - Performance metrics (e.g., CPU usage, memory utilization, latency) are comparable or improved.
    - No performance degradation in critical workloads.



> Failover Testing
  
  - Test node failover and workload recovery on nodes with the new AMI.
    - Workloads recover and are rescheduled without data loss or prolonged downtime.
    - Cluster maintains high availability during node failures.


-----------------------------------------------------------

### **DISK** or **VOLUME** change.

> Increase Disk Size of an Existing Volume
  
  - Increase the size of an existing EBS volume attached to a workload.
    - The volume is resized successfully without data loss.
    - Applications using the volume can utilize the increased capacity.
  

> Change the volume type
  
  - Change the type of an EBS volume to optimize for cost or performance (e.g., gp2 to gp3).
    - The volume type is updated successfully without data corruption.
    - Performance metrics (IOPS, throughput) align with the specifications of the new volume type.


> Migrate Workloads to a New Volume
  
  - Replace an existing volume with a new one (e.g., to use a different type or configuration).
    - Workloads are successfully migrated to the new volume without downtime or data loss.
    - Applications can read and write data to the new volume.


> Validate Disk Performance After Changes
  
  - Test the performance of resized or updated volumes to ensure they meet workload requirements.
    - IOPS and throughput match the specifications of the resized or updated volume.
    - Applications maintain consistent performance under load.


> Validate Volume Expansion for Stateful Workloads
  
  - Expand the disk size for stateful applications such as databases (e.g., MySQL, PostgreSQL).
    - The application recognizes the increased disk capacity.
    - Data integrity and application performance are maintained.


> Validate Backup and Recovery
  
  - Ensure backups and snapshots work as expected after resizing or changing the volume type.
    - Snapshots of the modified volume are created successfully.
    - Data can be restored from snapshots without corruption.


> Validate Multi-AZ Data Replication (for EFS or StatefulSets)
  
  - For multi-AZ setups, ensure that data replication works correctly after changing volume size or type.
    - Data replication remains consistent across availability zones.
    - No delays or failures occur in data synchronization.


> Validate Node Auto-Scaling with Updated Volumes
  
  - Test the behavior of auto-scaling groups with instances using updated disk sizes or types.
    - New nodes are created with the updated disk configuration.
    - No issues arise during workload rescheduling or node scaling events.



> Test Failure Scenarios
  
  - Simulate disk or volume failures to validate recovery processes after size or type changes.
    - Applications recover gracefully from disk-related failures.
    - No data loss or prolonged downtime occurs.


> Verify Cost Implications
 
  - Assess the cost impact of changing disk size or volume type.
    - The updated configuration aligns with budgetary constraints.
    - No unexpected increases in storage costs occur.



----------------------------------------------------

### **LABELS** and **TAINTS**

> Adding/Modifying Node Labels
  
  - Add or modify labels on nodes to support workload placement based on specific scheduling rules.
    - Nodes have the correct labels applied.
    - Workloads with nodeSelector or nodeAffinity rules are scheduled correctly.


> Removing Node Labels
 
  - Remove unused or incorrect labels from nodes.
    - Labels are removed without impacting workloads that no longer depend on them.
    - No orphaned workloads remain unscheduled.



> Adding/Modifying Taints on Nodes
  
  - Add or modify taints on nodes to control which workloads can run on them.
    - Nodes have the correct taints applied.
    - Only workloads with matching tolerations are scheduled on tainted nodes.
    - Non-tolerating workloads are evicted or unscheduled.


> Testing Tolerations with DaemonSets
  
  - Apply taints to nodes and validate that DaemonSets with appropriate tolerations are scheduled on all required nodes.
    - DaemonSet pods are scheduled on nodes with matching tolerations.
    - Nodes without tolerations are not scheduled with DaemonSet pods.


> Testing Taints with Auto-Scaling
  
  - Apply taints to nodes in an auto-scaling group and validate the behavior during scale-up and scale-down events.
    - New nodes inherit the taints from the launch template or configuration.
    - Workloads respect taint tolerations during auto-scaling.


> Testing Labels and Taints During Node Rollout
  
  - Perform a rolling update of node labels and taints during a node group upgrade.
    - Nodes are replaced with updated labels and taints without disrupting workloads.
    - Workloads are rescheduled correctly during the rollout.


> Testing Application-Specific Node Pools
  
  - Apply specific labels and taints to dedicated node pools for application segregation.
    - Applications are scheduled only on their dedicated node pools based on labels and taints.
    - No cross-pool workload interference occurs.


> Monitoring and Alerting Validation

  - Ensure monitoring and alerting systems detect misconfigured labels or taints.
    - Alerts are triggered for incorrectly configured labels or taints.
    - Monitoring tools (e.g., Prometheus, CloudWatch) display accurate node and pod status.



### **NODE CHANGES FOR WORKLOADS**

> Adding a New Node Group
  
  - Add a new node group to support specific workloads or provide additional resources.
    - The new node group is successfully created and registered with the cluster.
    - Workloads can be scheduled on the new nodes based on affinity and taint configurations.


> Draining and Removing Old Nodes
  
  - Decommission old nodes to replace them with upgraded ones.
    - Workloads are gracefully rescheduled to other nodes.
    - No disruption or downtime occurs during node removal.


> Changing Instance Types for a Node Group

  - Change the instance type for a node group to optimize cost or performance.
    - New nodes with the updated instance type are created.
    - Workloads migrate seamlessly to the new nodes without performance issues.


> Migrating Workloads to a Dedicated Node Group**
  
  - Migrate specific workloads to a dedicated node group for resource isolation or compliance.
    - Workloads are scheduled only on the dedicated node group.
    - Other workloads remain unaffected.


> Scaling Up Node Groups
  
  - Increase the number of nodes in a node group to handle increased workload demand.
    - New nodes are provisioned and registered with the cluster.
    - Workloads are scheduled evenly across the available nodes.


> Scaling Down Node Groups
  
  - Reduce the number of nodes in a node group during periods of low workload demand.
    - Nodes are gracefully terminated without impacting running workloads.
    - Pods are rescheduled onto remaining nodes.


> Tainting Nodes for Specific Workloads
  
  - Apply taints to nodes to restrict workloads and ensure only matching tolerations are scheduled.
    - Only workloads with matching tolerations are scheduled on tainted nodes.
    - Non-tolerating workloads are evicted from tainted nodes.


> Verifying Network Connectivity for New Nodes
 
  - Ensure new nodes are properly configured for networking (e.g., VPC CNI, security groups).
    - New nodes can communicate with other nodes and external resources.
    - No network-related errors occur in workloads.


> Validating Resource Requests and Limits
 
  - Ensure that node changes accommodate workloads’ resource requests and limits.
    - Workloads are scheduled without resource contention.
    - Nodes are not overcommitted, and pod performance remains stable.


> Verifying Node Health and Metrics
 
  - Ensure the health and performance of nodes after changes.
    - Nodes remain in a ready state, and metrics such as CPU, memory, and disk utilization are within acceptable thresholds.


> Testing High Availability
  
  - Validate workload distribution and failover behavior after node changes.
    - Workloads remain highly available during node changes.
    - Pods are evenly distributed across available nodes.


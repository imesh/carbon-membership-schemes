## Kubernetes Membership Scheme

Kubernetes membership scheme provides features for discovering WSO2 server clusters on Kubernetes.

### How it works
Once a Carbon server starts it will query container IP addresses in the given cluster via Kubernetes API using Kubernetes services. Thereafter Hazelcast network configuration will be updated with the above IP addresses. As a result the Hazelcast instance will get connected all the other members in the cluster. In addition once a new member is added to the cluster, all the other members will get connected to the new member.

### Installation

1. Apply Carbon kernel patch0012. This includes a modification in the Carbon Core component for
allowing to add third party membership schemes.

2. Copy following JAR files to the repository/components/lib directory of the Carbon server:

```
jackson-core-2.5.4.jar
jackson-databind-2.5.4.jar
jackson-annotations-2.5.4.jar
kubernetes-mscheme-carbon42-<version>.jar
```

3. Update axis2.xml with the following configuration:

```
<clustering class="org.wso2.carbon.core.clustering.hazelcast.HazelcastClusteringAgent" enable="true">
    <parameter name="membershipScheme">kubernetes</parameter>
    <parameter name="KUBERNETES_MASTER">http://172.17.8.101:8080</parameter>
    <parameter name="KUBERNETES_SERVICES">wso2esb</parameter>
    <parameter name="KUBERNETES_NAMESPACE">default</parameter>
</clustering>
```


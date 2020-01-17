# Kubernetes (K8S)

<img src="https://www.linuxfoundation.org/wp-content/uploads/2019/03/trademark-kubernetes-icon-correct-140x140.png">

Kubernetes is a container orchestration API


- kubectl -- The main tool to access and work in kubernetes
  - `kubectl get node` -- gets information about a node
  ```text
  NAME              STATUS   ROLES    AGE   VERSION
  bk-dell-charlie   Ready    <none>   49d   v1.17.0
  ```
  - `kubectl get node -o wide` -- displays more info for wider screens
  ```text
  NAME              STATUS   ROLES    AGE   VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
  bk-dell-charlie   Ready    <none>   49d   v1.17.0   192.168.1.21   <none>        Ubuntu 18.04.3 LTS   4.15.0-72-generic   containerd://1.2.5
  ```
  - `kubectl get node -o yaml` -- displays all information in YAML format
  ```yaml
  apiVersion: v1
    items:
    - apiVersion: v1
    kind: Node
    metadata:
        annotations:
        node.alpha.kubernetes.io/ttl: "0"
        volumes.kubernetes.io/controller-managed-attach-detach: "true"
        creationTimestamp: "2019-10-29T15:15:14Z"
        labels:
        beta.kubernetes.io/arch: amd64
        beta.kubernetes.io/os: linux
        kubernetes.io/arch: amd64
        kubernetes.io/hostname: bk-dell-charlie
        kubernetes.io/os: linux
        microk8s.io/cluster: "true"
        name: bk-dell-charlie
        resourceVersion: "3911726"
        selfLink: /api/v1/nodes/bk-dell-charlie
        uid: 430dc23b-abe9-4f4f-bedd-590e0b539485
    spec: {}
    status:
        addresses:
        - address: 192.168.1.21
        type: InternalIP
        - address: bk-dell-charlie
        type: Hostname
        allocatable:
        cpu: "4"
        ephemeral-storage: 958817328Ki
        hugepages-1Gi: "0"
        hugepages-2Mi: "0"
        memory: 16275496Ki
        pods: "110"
        capacity:
        cpu: "4"
        ephemeral-storage: 959865904Ki
        hugepages-1Gi: "0"
        hugepages-2Mi: "0"
        memory: 16377896Ki
        pods: "110"
        conditions:
        - lastHeartbeatTime: "2019-12-17T23:56:52Z"
        lastTransitionTime: "2019-12-07T03:30:53Z"
        message: kubelet has sufficient memory available
        reason: KubeletHasSufficientMemory
        status: "False"
        type: MemoryPressure
        - lastHeartbeatTime: "2019-12-17T23:56:52Z"
        lastTransitionTime: "2019-12-07T03:30:53Z"
        message: kubelet has no disk pressure
        reason: KubeletHasNoDiskPressure
        status: "False"
        type: DiskPressure
        - lastHeartbeatTime: "2019-12-17T23:56:52Z"
        lastTransitionTime: "2019-12-07T03:30:53Z"
        message: kubelet has sufficient PID available
        reason: KubeletHasSufficientPID
        status: "False"
        type: PIDPressure
        - lastHeartbeatTime: "2019-12-17T23:56:52Z"
        lastTransitionTime: "2019-12-07T03:30:53Z"
        message: kubelet is posting ready status. AppArmor enabled
        reason: KubeletReady
        status: "True"
        type: Ready
        daemonEndpoints:
        kubeletEndpoint:
            Port: 10250
        images:
        - names:
        - docker.io/bretfisher/shpod@sha256:a74dc9b4487e2697e423001d8de9e3362bd8124b83f7055f5b87d1724c4f037f
        - docker.io/bretfisher/shpod:latest
        sizeBytes: 96649467
        - names:
        - docker.io/library/httpd@sha256:649bd29cc9284f06cf1a99726c4e747a83679e04eea3311b55022dd247026138
        - docker.io/library/httpd:latest
        sizeBytes: 56586318
        - names:
        - docker.io/library/nginx@sha256:922c815aa4df050d4df476e92daed4231f466acc8ee90e0e774951b0fd7195a4
        - docker.io/library/nginx:latest
        sizeBytes: 50801905
        - names:
        - k8s.gcr.io/pause@sha256:f78411e19d84a252e53bff71a4407a5686c46983a2c2eeed83929b888179acea
        - k8s.gcr.io/pause:3.1
        sizeBytes: 317164
        nodeInfo:
        architecture: amd64
        bootID: 75cceb7f-fa0c-4e6b-8984-9d845ba26a1c
        containerRuntimeVersion: containerd://1.2.5
        kernelVersion: 4.15.0-72-generic
        kubeProxyVersion: v1.17.0
        kubeletVersion: v1.17.0
        machineID: 6f49cda27d824dee8c79dc1a1641cf59
        operatingSystem: linux
        osImage: Ubuntu 18.04.3 LTS
        systemUUID: 4C4C4544-0044-5310-8032-CAC04F465A31
    kind: List
    metadata:
    resourceVersion: ""
    selfLink: ""
  ```
  - `kubectl get nodes -o json | jq ".items[] | {name: .metadata.name} + .status.capacity"` -- query json response
  ```json
  {
    "name": "bk-dell-charlie",
    "cpu": "4",
    "ephemeral-storage": "959865904Ki",
    "hugepages-1Gi": "0",
    "hugepages-2Mi": "0",
    "memory": "16377896Ki",
    "pods": "110"
  }
  ```
  - `kubectl descrive node/bk-dell-charlie` -- displays information based on the type
  ```text
  Name:               bk-dell-charlie
    Roles:              <none>
    Labels:             beta.kubernetes.io/arch=amd64
                        beta.kubernetes.io/os=linux
                        kubernetes.io/arch=amd64
                        kubernetes.io/hostname=bk-dell-charlie
                        kubernetes.io/os=linux
                        microk8s.io/cluster=true
    Annotations:        node.alpha.kubernetes.io/ttl: 0
                        volumes.kubernetes.io/controller-managed-attach-detach: true
    CreationTimestamp:  Tue, 29 Oct 2019 11:15:14 -0400
    Taints:             <none>
    Unschedulable:      false
    Lease:
    HolderIdentity:  bk-dell-charlie
    AcquireTime:     <unset>
    RenewTime:       Tue, 17 Dec 2019 19:11:25 -0500
    Conditions:
    Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
    ----             ------  -----------------                 ------------------                ------                       -------
    MemoryPressure   False   Tue, 17 Dec 2019 19:06:54 -0500   Fri, 06 Dec 2019 22:30:53 -0500   KubeletHasSufficientMemory   kubelet has sufficient memory available
    DiskPressure     False   Tue, 17 Dec 2019 19:06:54 -0500   Fri, 06 Dec 2019 22:30:53 -0500   KubeletHasNoDiskPressure     kubelet has no disk pressure
    PIDPressure      False   Tue, 17 Dec 2019 19:06:54 -0500   Fri, 06 Dec 2019 22:30:53 -0500   KubeletHasSufficientPID      kubelet has sufficient PID available
    Ready            True    Tue, 17 Dec 2019 19:06:54 -0500   Fri, 06 Dec 2019 22:30:53 -0500   KubeletReady                 kubelet is posting ready status. AppArmor enabled
    Addresses:
    InternalIP:  192.168.1.21
    Hostname:    bk-dell-charlie
    Capacity:
    cpu:                4
    ephemeral-storage:  959865904Ki
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             16377896Ki
    pods:               110
    Allocatable:
    cpu:                4
    ephemeral-storage:  958817328Ki
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             16275496Ki
    pods:               110
    System Info:
    Machine ID:                 6f49cda27d824dee8c79dc1a1641cf59
    System UUID:                4C4C4544-0044-5310-8032-CAC04F465A31
    Boot ID:                    75cceb7f-fa0c-4e6b-8984-9d845ba26a1c
    Kernel Version:             4.15.0-72-generic
    OS Image:                   Ubuntu 18.04.3 LTS
    Operating System:           linux
    Architecture:               amd64
    Container Runtime Version:  containerd://1.2.5
    Kubelet Version:            v1.17.0
    Kube-Proxy Version:         v1.17.0
    Non-terminated Pods:          (1 in total)
    Namespace                   Name     CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
    ---------                   ----     ------------  ----------  ---------------  -------------  ---
    shpod                       shpod    0 (0%)        0 (0%)      0 (0%)           0 (0%)         38m
    Allocated resources:
    (Total limits may be over 100 percent, i.e., overcommitted.)
    Resource           Requests  Limits
    --------           --------  ------
    cpu                0 (0%)    0 (0%)
    memory             0 (0%)    0 (0%)
    ephemeral-storage  0 (0%)    0 (0%)
    Events:
    Type     Reason                   Age                From                         Message
    ----     ------                   ----               ----                         -------
    Normal   Starting                 45m                kube-proxy, bk-dell-charlie  Starting kube-proxy.
    Normal   Starting                 45m                kubelet, bk-dell-charlie     Starting kubelet.
    Warning  InvalidDiskCapacity      45m                kubelet, bk-dell-charlie     invalid capacity 0 on image filesystem
    Normal   NodeAllocatableEnforced  45m                kubelet, bk-dell-charlie     Updated Node Allocatable limit across pods
    Normal   NodeHasSufficientMemory  45m                kubelet, bk-dell-charlie     Node bk-dell-charlie status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    45m                kubelet, bk-dell-charlie     Node bk-dell-charlie status is now: NodeHasNoDiskPressure
    Normal   NodeHasSufficientPID     45m                kubelet, bk-dell-charlie     Node bk-dell-charlie status is now: NodeHasSufficientPID
    Warning  MissingClusterDNS        3s (x40 over 40m)  kubelet, bk-dell-charlie     kubelet does not have ClusterDNS IP configured and cannot create Pod using "ClusterFirst" policy. Falling back to "Default" policy.
  ```
- Exploring Resource Types
  - `kubectl api-reosurces` -- list of the reosueces available
  ```text
  NAME                              SHORTNAMES   APIGROUP                       NAMESPACED   KIND
    bindings                                                                      true         Binding
    componentstatuses                 cs                                          false        ComponentStatus
    configmaps                        cm                                          true         ConfigMap
    endpoints                         ep                                          true         Endpoints
    events                            ev                                          true         Event
    limitranges                       limits                                      true         LimitRange
    namespaces                        ns                                          false        Namespace
    nodes                             no                                          false        Node
    persistentvolumeclaims            pvc                                         true         PersistentVolumeClaim
    persistentvolumes                 pv                                          false        PersistentVolume
    pods                              po                                          true         Pod
    podtemplates                                                                  true         PodTemplate
    replicationcontrollers            rc                                          true         ReplicationController
    resourcequotas                    quota                                       true         ResourceQuota
    secrets                                                                       true         Secret
    serviceaccounts                   sa                                          true         ServiceAccount
    services                          svc                                         true         Service
    mutatingwebhookconfigurations                  admissionregistration.k8s.io   false        MutatingWebhookConfiguration
    validatingwebhookconfigurations                admissionregistration.k8s.io   false        ValidatingWebhookConfiguration
    customresourcedefinitions         crd,crds     apiextensions.k8s.io           false        CustomResourceDefinition
    apiservices                                    apiregistration.k8s.io         false        APIService
    controllerrevisions                            apps                           true         ControllerRevision
    daemonsets                        ds           apps                           true         DaemonSet
    deployments                       deploy       apps                           true         Deployment
    replicasets                       rs           apps                           true         ReplicaSet
    statefulsets                      sts          apps                           true         StatefulSet
    tokenreviews                                   authentication.k8s.io          false        TokenReview
    localsubjectaccessreviews                      authorization.k8s.io           true         LocalSubjectAccessReview
    selfsubjectaccessreviews                       authorization.k8s.io           false        SelfSubjectAccessReview
    selfsubjectrulesreviews                        authorization.k8s.io           false        SelfSubjectRulesReview
    subjectaccessreviews                           authorization.k8s.io           false        SubjectAccessReview
    horizontalpodautoscalers          hpa          autoscaling                    true         HorizontalPodAutoscaler
    cronjobs                          cj           batch                          true         CronJob
    jobs                                           batch                          true         Job
    certificatesigningrequests        csr          certificates.k8s.io            false        CertificateSigningRequest
    leases                                         coordination.k8s.io            true         Lease
    endpointslices                                 discovery.k8s.io               true         EndpointSlice
    events                            ev           events.k8s.io                  true         Event
    ingresses                         ing          extensions                     true         Ingress
    ingresses                         ing          networking.k8s.io              true         Ingress
    networkpolicies                   netpol       networking.k8s.io              true         NetworkPolicy
    runtimeclasses                                 node.k8s.io                    false        RuntimeClass
    poddisruptionbudgets              pdb          policy                         true         PodDisruptionBudget
    podsecuritypolicies               psp          policy                         false        PodSecurityPolicy
    clusterrolebindings                            rbac.authorization.k8s.io      false        ClusterRoleBinding
    clusterroles                                   rbac.authorization.k8s.io      false        ClusterRole
    rolebindings                                   rbac.authorization.k8s.io      true         RoleBinding
    roles                                          rbac.authorization.k8s.io      true         Role
    priorityclasses                   pc           scheduling.k8s.io              false        PriorityClass
    csidrivers                                     storage.k8s.io                 false        CSIDriver
    csinodes                                       storage.k8s.io                 false        CSINode
    storageclasses                    sc           storage.k8s.io                 false        StorageClass
    volumeattachments                              storage.k8s.io                 false        VolumeAttachment
  ```
  - `kubectl explain <type>` -- shows docs for an api-resource type
  ```text
    KIND:     Node
    VERSION:  v1

    DESCRIPTION:
        Node is a worker node in Kubernetes. Each node will have a unique
        identifier in the cache (i.e. in etcd).

    FIELDS:
    apiVersion	<string>
        APIVersion defines the versioned schema of this representation of an
        object. Servers should convert recognized schemas to the latest internal
        value, and may reject unrecognized values. More info:
        https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

    kind	<string>
        Kind is a string value representing the REST resource this object
        represents. Servers may infer this from the endpoint the client submits
        requests to. Cannot be updated. In CamelCase. More info:
        https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

    metadata	<Object>
        Standard object's metadata. More info:
        https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

    spec	<Object>
        Spec defines the behavior of a node.
        https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status

    status	<Object>
        Most recently observed status of the node. Populated by the system.
        Read-only. More info:
        https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status
  ```
    - Also see `kubectl explain <type>.<subtype>` and `kubectl explain <type> --recursive`
  - `kubectl get services`-- shows info about services running on a node
  - `kubectl get pods` -- displays info on running pods in the default namespace
  - `kubectl get pods --all-namespaces` -- displays info on running pods in all namespaces
  - `kubectl run <podname> --image <imagename> [<command_to_run>]` -- builds a deployment set and executes the image specified
  - `kubectl scale deploy/<deploymentname> --replicas <number_of_replicas>` create additional copies of the pod
[Back to Index](index.md)

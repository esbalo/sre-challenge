# Build pipeline
* I have decided to use github actions since the challenge has been shared through Github. 
This way everything is together and pretty well integrated.
Always using offical task when they are available.
* We are using docker for building the image so I decided to use the offical Docker image regsitry, DockerHub.


# Deploy application
* I have used Helm to create deployment as leading Kubernetes package manager and part of Cloud Native Fonudation. It is very well documented and wide-extended.
I created a deafult template and I added some changes to improve the behavior
    * Resources limits and request have the same values to grant [guaranteed](https://kubernetes.io/docs/concepts/workloads/pods/pod-qos/#guaranteed) QoS
    * Add PDB to ha control on [voluntary disruptions](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#voluntary-and-involuntary-disruptions)
    * Add antiaffinity rule to prevent pods to be in the same node if there are nodes available and avoid single point of failure.
    * Add prestop policy to avoid downtime when pods are deleting and give some time to update network rules (iptables). [Newer kubernetes version include this as a built-in action](https://github.com/kubernetes/enhancements/blob/master/keps/sig-node/3960-pod-lifecycle-sleep-action/README.md)
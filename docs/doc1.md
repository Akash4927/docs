---
id: doc1
title: OpenEBS Introduction
sidebar_label: Introduction
---

OpenEBS is a cloud native storage solution built with the goal of
providing containerized storage for containers. Using OpenEBS, a
developer can seamlessly get the persistent storage for stateful
applications with ease, much of which is automated, while using the
popular orchestration platforms such as Kubernetes.

Persistent storage presents significant challenges to the developer
interfacing with stateful applications such as databases. While a
developer can get the initial needs of persistent storage using Docker
volume plug-in, Kubernetes stateful sets and so on, there is lots more
to the storage needs of an application than just the connectivity.

**Note:**

OpenEBS integration support is provided only for Kubernetes.

A DevOps developer gets the following from the OpenEBS solution.

-   OpenEBS operator yaml file that installs the OpenEBS components onto
    a k8s cluster
-   A set of yaml files containing configuration examples of how to use
    OpenEBS storage classes
-   A CLI for monitoring the persistent volume and its replicas

Using the above tools, a developer can easily provision the persistent
storage from the hostdir of the minion node. Much of the tasks for the
developer are automated by the OpenEBS storage class, including,
scheduling the volume and replicas on k8s minions, connectivity to the
container via a mount point.

Components
----------

This section includes OpenEBS components.

OpenEBS platform contains the following main components:

> -   Maya - The helper storage orchestration engine that aids the
>     kubernetes orchestration of storage volumes
> -   Jiva - A docker image that is used to spin the storage volume
>     containers on Kubernetes nodes

### Maya

OpenEBS orchestration does not pre-empt or overwrite the Kubernetes
orchestration system. It rather fills the storage orchestration gaps
left behind by Kubernetes. For example, in OpenEBS, storage volume
provisioning workflow is handled by Kubernetes. Just like other
Kubernetes storage incubators, OpenEBS provides a new storage incubator
called "OpenEBS". This incubator will have a storage class called
"OpenEBS-storageclass". Internally, openebs-storageclass interacts with
Maya to decide on which node a given volume must be provisioned, when it
must be augmented automatically in capacity and so on. Maya also helps
in data protection operations such as taking snapshots, restoring from
snapshots and so on.

### Jiva

Jiva is the docker container image for storage volume containers. In
OpenEBS, the storage volumes are containerized. Each volume will have
atleast one storage controller and a storage replica, each of which will
be a Jiva container. The functionality embedded into the Jiva image
includes the following:

-   iSCSI target
-   Block replication controller (if the container is a controller)
-   Block storage handler (if the container is a replica)

Storage Policies
----------------

On their own, StorageClass lets you store and retrieve storage policies.
It is only when combined with OpenEBS components namely openebs
provisioner and maya api service that storage policies are applied
against a PersistentVolume (a Kubernetes kind). The OpenEBS volume
controller interprets the StorageClass' structured data as a record of
the user’s desired state, and continually takes action to achieve and
maintain that state.

Users can deploy and update OpenEBS volume controller (otherwise known
as Maya api service) on a running OpenEBS cluster, independently of the
cluster’s own lifecycle. OpenEBS volume controller hooks up to the
lifecycle of PersistentVolume (that is marked for OpenEBS via OpenEBS
provisioner) to apply these storage policies.

**See Also:**

Changelog\_
:



<!-- Hotjar Tracking Code for https://docs.openebs.io -->
<script>
    (function(h,o,t,j,a,r){
        h.hj=h.hj||function(){(h.hj.q=h.hj.q||[]).push(arguments)};
        h._hjSettings={hjid:785693,hjsv:6};
        a=o.getElementsByTagName('head')[0];
        r=o.createElement('script');r.async=1;
        r.src=t+h._hjSettings.hjid+j+h._hjSettings.hjsv;
        a.appendChild(r);
    })(window,document,'https://static.hotjar.com/c/hotjar-','.js?sv=');
</script>


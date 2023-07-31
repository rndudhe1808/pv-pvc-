# pv-pvc-killerkoda-node01
Deploying WordPress and MySQL in Kubernetes using Persistent Volumes (PV) and Persistent Volume Claims (PVC) with an NFS server created on "killerkoda node01" involves setting up a scalable and resilient environment for running a WordPress website with a MySQL database. Here's a step-by-step description of the process:

1. Set up NFS Server on "killerkoda node01":
   - Install NFS server software on "killerkoda node01" if not already installed.
   - Configure NFS exports on "killerkoda node01" to share a directory **(/test & /test2)** that will be used for storing the data of WordPress and MySQL.

2. Create Persistent Volumes (PVs) for WordPress and MySQL:
   - On the Kubernetes cluster, create PV definitions that represent the NFS shares exported by the "killerkoda node01".
   - Define the capacity and access modes of the PVs to match the requirements of WordPress and MySQL.

3. Deploy WordPress:
   - Create a Persistent Volume Claim (PVC) for WordPress, which will automatically bind to an available PV.
   - Deploy the WordPress application using a Kubernetes Deployment or StatefulSet, depending on your needs.
   - Configure the WordPress container to use the mounted PVC as the location to store uploads, themes, and plugins, ensuring that data persists even if the pod is rescheduled.

4. Deploy MySQL:
   - Create a Persistent Volume Claim (PVC) for MySQL to bind it to an available PV.
   - Deploy the MySQL database using a Kubernetes Deployment or StatefulSet, depending on your requirements.
   - Configure the MySQL container to use the mounted PVC as the location to store database files.

5. Connect WordPress to MySQL:
   - Ensure that the WordPress application can access the MySQL database by using environment variables.

6. Testing and Scaling:
   - Test the WordPress website to ensure it is functioning correctly with the MySQL database.
   - Monitor the resources and performance of both WordPress and MySQL pods to determine if scaling is necessary.

Advantages of using PV and PVC with NFS:
- **Data Persistence**: With PV and PVC, data persists even if the pods are rescheduled or restarted, ensuring that no data is lost in case of container failures.
- **Scalability**: PV and PVC allow you to scale your WordPress and MySQL deployments independently by adding more replicas, and the data will be shared consistently across all instances.
- **Decoupling Storage from Compute**: PV and PVC provide a decoupled approach, separating the storage configuration from the application, making it easier to manage and maintain the storage layer separately from the application layer.
- **High Availability**: By utilizing PVs, you can ensure high availability by creating multiple replicas of your NFS server and using volume replication features of NFS.

Keep in mind that the exact steps and configuration details may vary based on your specific Kubernetes setup and NFS server configuration. Make sure to refer to the official documentation and best practices for Kubernetes and NFS to ensure a smooth and secure deployment.

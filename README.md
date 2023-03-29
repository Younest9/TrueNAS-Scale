# TrueNAS Scale

TrueNAS SCALE provides simple access to the well-established Linux container ecosystem and makes application deployment easy. With support for KVM virtual machines, Kubernetes, and Docker containers, it’s easy to customize and add applications to suit a wide variety of needs.

TrueNAS SCALE is Open Source, based on Debian Linux, and free to download and use. With hundreds of thousands of testers and contributors, the TrueNAS community development model enables broader testing, and ultimately, a higher quality product, in addition to its unbeaten value. Join the “Storage Freedom” movement and enjoy the benefits of Open Source economics. 

## Features

*   **Containerized Applications** - TrueNAS SCALE provides a simple way to deploy and manage applications in containers. With support for Docker and Kubernetes, it’s easy to customize and add applications to suit a wide variety of needs.
*   **Virtual Machines** - TrueNAS SCALE provides a simple way to deploy and manage virtual machines. With support for KVM, it’s easy to customize and add virtual machines to suit a wide variety of needs.
*   **Open Source** - TrueNAS SCALE is Open Source, based on Debian Linux, and free to download and use. With hundreds of thousands of testers and contributors, the TrueNAS community development model enables broader testing, and ultimately, a higher quality product, in addition to its unbeaten value. Join the “Storage Freedom” movement and enjoy the benefits of Open Source economics.
*   **Enterprise Storage** - TrueNAS SCALE provides some enterprise storage features such as ZFS, snapshots, replication, and more.
*   **Simplified Storage Management** - TrueNAS SCALE provides a simple way to manage storage. With support for iSCSI, NFS, and SMB, it’s easy to customize and add storage to suit a wide variety of needs.
*   **Simplified Network Management** - TrueNAS SCALE provides a simple way to manage network interfaces. With support for VLANs, it’s easy to customize and add network interfaces to suit a wide variety of needs.
*   **Simplified User Management** - TrueNAS SCALE provides a simple way to manage users. With support for LDAP, it’s easy to customize and add users to suit a wide variety of needs.
*   **Simplified System Management** - TrueNAS SCALE provides a simple way to manage system settings. With support for system settings, it’s easy to customize and add system settings to suit a wide variety of needs.

## Installation

TrueNAS SCALE can be installed on a variety of hardware platforms.

### Hardware Requirements

*   2GB RAM
*   2GB of disk space
*   1GB network interface

### Installation Process

1.  Download the latest TrueNAS SCALE ISO image from the [TrueNAS SCALE Download Page](https://www.truenas.com/download-truenas-scale/).
2.  Burn the ISO image to a USB drive, or if you are using a virtual machine, mount the ISO image.
3.  Boot the system from the USB drive or ISO image.
4.  Follow the on-screen instructions to install TrueNAS SCALE.

### Post-Installation Process

1.  Log in to the TrueNAS SCALE web interface using the credentials you set during installation.
2.  If you want to use a static IP address, go to **Network**, and click **Edit** next to the interface you want to configure.

    > If you want to use DHCP, you can skip this step.
    > 
    > If you want to use static IP address, you need to add a static DNS server to the interface.
3.  Create a pool by going to **Storage**, and click **Create Pool**.

    >  You can create a dataset by going to **Storage**, and click **Create Dataset**.
    >
    >  You can create a share by going to **Sharing**, and click **Create Share**.
    >
    >  You can create a user by going to **Accounts**, and click **Create User**.
    >
    >  You can create a group by going to **Accounts**, and click **Create Group**.

## Application Deployment

TrueNAS SCALE provides a simple way to deploy and manage applications in containers. With support for Docker and Kubernetes, it’s easy to customize and add applications to suit a wide variety of needs.

### Using Docker Images

You can deploy Docker containers from the TrueNAS SCALE web interface.

To deploy a Docker container, follow these steps:

1.  Log in to the TrueNAS SCALE web interface.
2.  Create a Dataset by going to **Storage**, and click **Create Dataset** (optional, but it's recommended to isolate app data).
3.  Click **Apps**.

    > If it's your first time using the Apps page, you will be prompted to select a pool.
    > 
    > If you haven't created a pool yet, you can do by going to **Storage**, and click **Create Pool**.
4.  Click **Launch Docker Image**.
5.  Enter the configuration options for the Docker container.
6.  Click **Save**.

### Using Built-in Applications (Built-in Charts)

You can deploy built-in applications from the TrueNAS SCALE web interface. To deploy a built-in application, follow these steps:

1.  Log in to the TrueNAS SCALE web interface.
2.  Create a Dataset by going to **Storage**, and click **Create Dataset** (optional, but it's recommended to isolate app data).
3.  Click **Apps**.

    > If it's your first time using the Apps page, you will be prompted to select a pool.
    > 
    > If you haven't created a pool yet, you can do by going to **Storage**, and click **Create Pool**.
4.  Click **Available Apps**.
5.  Click **Install** next to the application you want to deploy.
6.  Enter the configuration options for the application.
7.  Click **Save**.

### Using Custom Applications (Custom Charts)

You can deploy custom applications from the TrueNAS SCALE web interface. To deploy a custom application, follow these steps:

1.  Log in to the TrueNAS SCALE web interface.
2.  Click **Apps**.

    > If it's your first time using the Apps page, you will be prompted to select a pool.
    >
    > If you haven't created a pool yet, you can do by going to **Storage**, and click **Create Pool**.
3.  Click **Manage Catalogs**.
4.  Click **Add Catalog**.
5.  Enter the **URL** of the **custom chart (repository)**, the **preferred Trains**, the **branch**, and the **name** of the catalog.
6.  Click **Save**.
7.  Create a Dataset by going to **Storage**, and click **Create Dataset** (optional, but it's recommended to isolate app data).
8.  Click **Available Apps**.
    > You may wait a few minutes for the added chart's applications to appear in the list.
    >
    > After a few moments, you should now see new applications added to the list.
    >
    > If you don't see the new applications, click **Refresh All**.
9.  Click **Install** next to the application you want to deploy.
10.  Enter the configuration options for the application.
11. Click **Save**.

## Limitations

*   TrueNAS SCALE does not support Clustering.
*   TrueNAS SCALE does not support High Availability.
*   TrueNAS SCALE does not support TrueNAS Enterprise features such as TrueNAS Enterprise Plugins, TrueNAS Enterprise Active Directory, TrueNAS Enterprise LDAP, TrueNAS Enterprise Kerberos, TrueNAS Enterprise SNMP, TrueNAS Enterprise S3...
*   TrueNAS SCALE does not support TrueNAS Enterprise hardware features such as TrueNAS Enterprise Hardware Encryption, TrueNAS Enterprise Hardware Acceleration...
* TrueNAS SCALE does not offer a lot of customization options for the applications deployed from a docker image, or the official chart (Forcing you to exposing apps in nodePort always, not integrating a reverse proxy, etc.)
* [...]

## Known Issues

When Testing, we found the following issues : (The custom chart we used is TrueCharts)

*   When deploying apps from the official chart, the apps are accessible only on NodePort, we cannot configure them to use a certain type of service (ClusterIP, LoadBalancer, etc.). on the other hand, when deploying apps from the custom chart, we can configure the service type to use.
*   When deploying a reverse proxy from the custom chart, it works as expected, but pairing it with apps from the official chart, it's not possible to configure them to use the reverse proxy. (For example, when deploying a reverse proxy, and a Nextcloud app from the official chart, it's not possible to configure the ingress option of the Nextcloud app to use the reverse proxy). 
*   When deploying apps from a custom chart, there's an option to expose the apps as a ClusterIP, but not on the official chart (Same App, different chart).
*   When deploying apps from the custom chart, it's possible to add custom storage, but for some raison, it doesn't work as expected. The apps are deployed, but the storage is not mounted (All type of storage: NFS, HostPath, EmptyDir, PVC, etc.). Also, we can deploy an app using custom chart when there's no storage needed in the configuration, but when we add a storage, it doesn't work as expected (For a lot of apps using the custom chart).
*   When deploying apps using **Launch Docker Image** option, there's no option to configure the service type (NodePort, ClusterIP, LoadBalancer, etc.), it's always NodePort. Also, there's no option to configure the ingress option.
*   It's required to edit the **timezone** of TrueNAS SCALE to match the timezone of the host, otherwise, the apps deployed from the custom chart will not work as expected (For example, when deploying a Nextcloud app from the custom chart, the timezone is not set correctly, and the app is not working as expected).

## References

*   [TrueNAS SCALE Documentation](https://www.truenas.com/docs/scale/)
*   [TrueNAS SCALE Release Notes](https://www.truenas.com/docs/scale/release-notes/)
*   [TrueNAS SCALE Installation Guide](https://www.truenas.com/docs/scale/install/)
*   [TrueNAS SCALE User Guide](https://www.truenas.com/docs/scale/userguide/)
*   [TrueNAS SCALE API Reference](https://www.truenas.com/docs/scale/api/)
*   [TrueNAS SCALE Troubleshooting Guide](https://www.truenas.com/docs/scale/troubleshooting/)
*   [Youtube: TrueNAS Scale the ULTIMATE Home Server? Docker, kubernetes, Apps - Christian Lampa](https://www.youtube.com/watch?v=LJY9KBbL4j0)
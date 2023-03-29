# TrueNAS Scale

TrueNAS SCALE provides simple access to the well-established Linux container ecosystem and makes application deployment easy. With support for KVM virtual machines, Kubernetes, and Docker containers, it’s easy to customize and add applications to suit a wide variety of needs.

TrueNAS SCALE is Open Source, based on Debian Linux, and free to download and use. With hundreds of thousands of testers and contributors, the TrueNAS community development model enables broader testing, and ultimately, a higher quality product, in addition to its unbeaten value. Join the “Storage Freedom” movement and enjoy the benefits of Open Source economics. 

## Features

*   **Containerized Applications** - TrueNAS SCALE provides a simple way to deploy and manage applications in containers. With support for Docker and Kubernetes, it’s easy to customize and add applications to suit a wide variety of needs.
*   **Virtual Machines** - TrueNAS SCALE provides a simple way to deploy and manage virtual machines. With support for KVM, it’s easy to customize and add virtual machines to suit a wide variety of needs.
*   **Open Source** - TrueNAS SCALE is Open Source, based on Debian Linux, and free to download and use. With hundreds of thousands of testers and contributors, the TrueNAS community development model enables broader testing, and ultimately, a higher quality product, in addition to its unbeaten value. Join the “Storage Freedom” movement and enjoy the benefits of Open Source economics.
*   **Enterprise Storage** - TrueNAS SCALE provides enterprise storage features such as ZFS, snapshots, replication, and more.
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

## Application Deployment

TrueNAS SCALE provides a simple way to deploy and manage applications in containers. With support for Docker and Kubernetes, it’s easy to customize and add applications to suit a wide variety of needs.

### Using Docker Images

You can deploy Docker containers from the TrueNAS SCALE web interface. To deploy a Docker container, follow these steps:

1.  Log in to the TrueNAS SCALE web interface.
2.  Click **Apps**.
> If it's your first time using the Apps page, you will be prompted to select a pool.
> 
> If you haven't created a pool yet, you can do by going to **Storage**, and click **Create Pool**.
3.  Click **Launch Docker Image**.
4.  Enter the configuration options for the Docker container.
5.  Click **Save**.

### Using Built-in Applications (Built-in Charts)

You can deploy built-in applications from the TrueNAS SCALE web interface. To deploy a built-in application, follow these steps:

1.  Log in to the TrueNAS SCALE web interface.
2.  Click **Apps**.
> If it's your first time using the Apps page, you will be prompted to select a pool.
> 
> If you haven't created a pool yet, you can do by going to **Storage**, and click **Create Pool**.
3.  Click **Available Apps**.
4.  Click **Install** next to the application you want to deploy.
5.  Enter the configuration options for the application.
6.  Click **Save**.

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
7.  Click **Available Apps**.
> You may wait a few minutes for the added chart's applications to appear in the list.
>
> After a few moments, you should now see new applications added to the list.
>
> If you don't see the new applications, click **Refresh All**.
8.  Click **Install** next to the application you want to deploy.
9.  Enter the configuration options for the application.
10. Click **Save**.

## Limitations

*   TrueNAS SCALE does not support Clustering.
*   TrueNAS SCALE does not support High Availability.
*   TrueNAS SCALE does not support TrueNAS Enterprise features such as TrueNAS Enterprise Plugins, TrueNAS Enterprise Active Directory, TrueNAS Enterprise LDAP, TrueNAS Enterprise Kerberos, TrueNAS Enterprise SNMP, TrueNAS Enterprise S3...
*   TrueNAS SCALE does not support TrueNAS Enterprise hardware features such as TrueNAS Enterprise Hardware Encryption, TrueNAS Enterprise Hardware Acceleration...
* [...]

## References

*   [TrueNAS SCALE Documentation](https://www.truenas.com/docs/scale/)
*   [TrueNAS SCALE Release Notes](https://www.truenas.com/docs/scale/release-notes/)
*   [TrueNAS SCALE Installation Guide](https://www.truenas.com/docs/scale/install/)
*   [TrueNAS SCALE User Guide](https://www.truenas.com/docs/scale/userguide/)
*   [TrueNAS SCALE API Reference](https://www.truenas.com/docs/scale/api/)
*   [TrueNAS SCALE Troubleshooting Guide](https://www.truenas.com/docs/scale/troubleshooting/)
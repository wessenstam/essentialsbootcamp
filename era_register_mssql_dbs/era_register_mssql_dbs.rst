.. _era_register_mssql_dbs:

------------------------------
Era: Register MSSQL Databases
------------------------------

Overview
++++++++

.. note::

  Estimated time to complete: **30 MINUTES**

In this lab we will import existing MSSQL Databases into Era for management.

Register MSSQL Databases with Erasure
+++++++++++++++++++++++++++++++++++++

Before Era can be used with existing databases, they must be registered in Era. SQL Server supports multiple databases in the same instance. The process to register the first database is slightly different from registering the second database.

Register The WideWorldImporters Database
........................................

Once the **WideWorldImporters** database has been registered with Era, the Time Machine for the database will start creating snapshots and collecting transaction log backups.

#. Open \https://*ERA-VM-IP:8443*/ in a new browser tab.

#. Select the **Era > Getting Started** drop down menu and click **Databases**.

#. Select **Sources** in the **Databases** pane on the left-hand side of the screen.

#. Click **+ Register**.

#. In the **Register a Source Database** Dialoge box, select **Microsoft SQL Server**, and click **Next**.

#. On the **Database Server** screen, input the following and click **Next**:

   -  **Database is on a Server that is:** - Not Registered
   -  **IP Address or Name of VM** - *Initials*-Database IP
   -  **Instance Name** - MSSQLSERVER
   -  **Windows Administrator Name** - Administrator
   -  **Windows Administrator Password** - nutanix/4u
   -  **Connect to SQL Server Login** - Windws Admin User
   -  **User Name** - Administrator

   .. figure:: images/registerdb_01.png

#. On the **Database** screen, input the following and click **Next**:

   -  **Database Name on VM** - WideWorldImporters
   -  **Database Name in Era** - WideWorldImporters
   -  **Description** - (Optional) Description

   .. figure:: images/registerdb_02.png

#. On the **Time Machine** screen, input the following and click **Register**:

   -  **Recovery Model** - Full/Bulk-logged
   -  **Manage Log Backups with** - Era
   -  **Name** - WideWorldImporters_TM
   -  **Description** - (Optional) Description
   -  **SLA** - GOLD
   -  **Schedule** - Take Defaults

   .. figure:: images/registerdb_03.png

#. Monitor the registration operation by clicking **WideWorldImporters**.

   .. note::

     Wait for the operation to successfully complete before attempting to register another SQL Server database.

Register The WideWorldImportersDW Database
..........................................

The process to register the second database is slightly different since the database server has already been registered.

   .. note::

     This same process can be used to register additional databases on the same instance of SQL Server.

Once the **WideWorldImportersDW** database has been registered with Era, the Time Machine for the database will start creating snapshots and collecting transaction log backups.

#. Open \https://*ERA-VM-IP:8443*/ in a new browser tab.

#. Select the **Era > Getting Started** drop down menu and click **Databases**.

#. Select **Sources** in the **Databases** pane on the left-hand side of the screen.

#. Click **+ Register**.

#. In the **Register a Source Database** Dialoge box, select **Microsoft SQL Server**, and click **Next**.

#. On the **Database Server** screen, input the following and click **Next**:

   -  **Database is on a Server that is:** - Registered
   -  **Registered Database Servers** - *Initials*-MSSQL-PROD

   .. figure:: images/registerdb_04.png

#. On the **Database** screen, input the following and click **Next**:

   -  **Database Name on VM** - WideWorldImportersDW
   -  **Database Name in Era** - WideWorldImportersDW
   -  **Description** - (Optional) Description

#. On the **Time Machine** screen, input the following and click **Register**:

   -  **Recovery Model** - Full/Bulk-logged
   -  **Manage Log Backups with** - Era
   -  **Name** - WideWorldImportersDW_TM
   -  **Description** - (Optional) Description
   -  **SLA** - GOLD
   -  **Schedule** - Take Defaults

#. Monitor the registration operation by clicking **WideWorldImportersDW**.

.. _era_clone_mssqldb:

-------------------
Era: Clone MSSQL DB
-------------------

Overview
++++++++

.. note::

  Estimated time to complete: **30 MINUTES**

In this lab we will perform some basic management tasks in Era. We will create snapshots, perform log catch ups, and clone/refresh clone DBs.

Create a Manual Snapshot
++++++++++++++++++++++++

The Time Machine for a database will automatically create snapshots based on the defined schedule. There are use cases where creating a snapshot outside of the Time Machine’s automatic schedule is desired. For example, when cloning or refreshing from the current time, it is more efficient to create a manual snapshot and clone or refresh from the manual snapshot

To create a manual snapshot of the **WideWorldImporters** database, do the following:

#. Open \https://*ERA-VM-IP:8443*/ in a new browser tab.

#. Select **Sources** in the **Databases** pane on the left-hand side of the screen.

#. Select the **WideWorldImporters** database.

#. Click **WideWorldImporters_TM** to the right of **WideWorldImporters**.

   .. figure:: images/clonedb_01.png

#. Click **Actions > Snapshot**.

#. Give the snapshot the name *initials*-**Manual**-*date* (ex: xyz-Manual-01012019), and click **Create**.

#. Monitor the registration operation by clicking **The snapshot operation for** *initials*-**Manual**-*todays date* **has started. Click here to see the status**.

   .. note::

     Wait for the operation to complete before attempting to use the snapshot

Initiate a Manual Log Catch Up
++++++++++++++++++++++++++++++

If configured for point in time recovery, the Time Machine for a SQL Server database will automatically collect transaction log backups based on the defined schedule. The process to collect transaction log backups is called Log Catch Up. To clone or refresh from a point in time between the current time and the time of the last automatic log catch up, the log catch up process must be initiated manually to collect the transaction log backups. Once the manual log catch up is complete, an arbitrary point in time can be select from that time window.

To initiate a manual log catch up for the **WideWorldImporters** database, do the following:

#. Open \https://*ERA-VM-IP:8443*/ in a new browser tab.

#. Select **Sources** in the **Databases** pane on the left-hand side of the screen.

#. Select the **WideWorldImporters** database.

#. Click **WideWorldImporters_TM** to the right of **WideWorldImporters**.

#. Click **Actions > Log Catch Up**.

#. Click **Yes** to start the Log Catch Up.

#. Monitor the registration operation by clicking **The log catch up operation has started. Click here to see status**.

   .. note::

     Wait for the operation to complete before attempting to clone or refresh from a point in time between the current time and the time of the last automatic log catch up.

Cloning Your MSSQL Source
+++++++++++++++++++++++++

A database can be cloned, either from a snapshot or from an arbitrary point in time, using the Time Machine for the database. A database can be cloned to a new database server, or to an existing database server. This section provides instructions on how to clone to a new server.

   .. note::

     While the instructions in this section show how to clone the WideWorldImporters database, the same process can be used to clone any SQL Server database registered in Era.

To clone the **WideWorldImporters** database, do the following:

#. Open \https://*ERA-VM-IP:8443*/ in a new browser tab.

#. Select **Sources** in the **Databases** pane on the left-hand side of the screen.

#. Select the **WideWorldImporters** database.

#. Click **WideWorldImporters_TM** to the right of **WideWorldImporters**.

#. Click **Actions > Clone Database**.

#. The **Clone Database** dialog box appears.

#. On the **Time** screen, input the following and click **Next**:

   .. note::

     By default, Era will display the daily view for the current day. You can change the day by clicking the blue arrows on each side of the displayed date. Alternatively, you can change the day by clicking **Month** and selecting a different day from the calendar view. To switch back to the daily view, click **Day**.

   -  **Clone a** - Snapshot
   -  **Snapshot** - *initials*-**Manual**-*date*

   .. figure:: images/clonedb_02.png

   .. note::

     To clone from a point in time, do the following: Under Clone a, select Point in Time, Select the hour, minute and second from which to clone.

     -  To clone from 1:12:03am, the displayed value should be 01:12:03.
     -  To clone from 6:32:03pm, the displayed value should be 18:32:03.

#. On the **Database Server** screen, input the following and click **Next**:

   -  **Database Server** - Create New Server
   -  **Database Server Name** - *Initials*-MSSQL-PROD-Clone
   -  **Compute Profile** - DEFAULT_OOB_COMPUTE
   -  **Network Profile** - DEFAULT_OOB_NETWORK
   -  **Administrator Password** - nutanix/4u
   -  **Join Domain** - Unselcted

   .. figure:: images/clonedb_03.png

#. On the **Database** screen, input the following and click **Clone**:

   -  **Clone Name** - WideWorldImporters_Clone
   -  **Database Name on VM** - WideWorldImporters
   -  **Description** - (Optional) Description
   -  **Instance Name** - MSSQLSERVER

#. Monitor the clone operation by clicking The operation to clone **WideWorldImporters_Clone** has started. Click here to see status. at the top of the screen.

   .. note::

     Wait for the operation to complete before attempting to use the clone.

Refresh Your Cloned MSSQL Database
++++++++++++++++++++++++++++++++++

Once a database has been cloned, Era can refresh the clone to a different point in time. Using the Time Machine for the source database, a clone can be refreshed from either a snapshot or an arbitrary point in time. While the instructions in this section show how to refresh the clone **WideWorldImporters_Clone**, the same process can be used to refresh a clone of any SQL Server database.

To refresh the clone WideWorldImporters_Clone, do the following:

#. Open \https://*ERA-VM-IP:8443*/ in a new browser tab.

#. Select **Clones** in the **Databases** pane on the left-hand side of the screen.

#. Select the **WideWorldImporters_Clone** database.

#. Click **Refresh**.

#. The **Clone Database** dialog box appears, enter the following and click **Refresh**:

   -  **Refresh to a** - Snapshot
   -  **Snapshot** - Select Snapshot

   .. note::

     To refresh from a point in time, do the following: Under Refresh to a, select Point in Time, Select the hour, minute and second from which to clone.

     -  To clone from 1:12:03am, the displayed value should be 01:12:03.
     -  To clone from 6:32:03pm, the displayed value should be 18:32:03.

#. Monitor the refresh operation by clicking The operation to refresh WideWorldImporters_Clone has started. Click here to see status. at the top of the screen.

   .. note::

     Wait for the operation to complete before attempting to use the refreshed clone.

Takeaways
+++++++++

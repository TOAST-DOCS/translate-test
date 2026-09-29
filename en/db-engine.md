<!-- machine_translated: true -->

<!-- pre-align:aligned sig=56dd0b1a76a6 -->

<a id="database-rds-for-postgresql-db-engine"></a>
## Database > RDS for PostgreSQL > DB Engine { #database-rds-for-postgresql-db-engine }

<a id="db-engine"></a>
## DB Engine { #db-engine }
In PostgreSQL, the version number consists of version = `X.Y`. In NHN Cloud's RDS for PostgreSQL, `X` represents the major version, and `Y` represents the minor version.

<a id="db-engine-version-provided-by-rds"></a>
### DB Engine Version Provided by RDS { #db-engine-version-provided-by-rds }

You can use the following versions.

| Version              | Note                            |
|---------------------|-------------------------------|
| <strong>17</strong> |                               |
| PostgreSQL 17.10    |                               |
| PostgreSQL 17.6     |                               |
| PostgreSQL 17.4     |                               |
| PostgreSQL 17.2     | Cannot be newly created or used to add a Read Replica. |
| <strong>14</strong> |                               |
| PostgreSQL 14.23    |                               |
| PostgreSQL 14.19    |                               |
| PostgreSQL 14.17    |                               |
| PostgreSQL 14.15    | Cannot be newly created or used to add a Read Replica. |
| PostgreSQL 14.6     | Cannot be newly created or used to add a Read Replica. |

!!! warning "Caution"
    For PostgreSQL version 14.6, 14.15, and 17.2, upgrades to the latest version are [recommended](https://www.postgresql.org/support/security/CVE-2025-1094/).

<a id="perform-version-upgrades"></a>
### Perform Version Upgrades { #perform-version-upgrades }

Version upgrades proceed in sequence, and may proceed in a different order depending on the characteristics of each major version upgrade and minor version upgrade. 

Version upgrades proceed in sequence, and may proceed in a different order depending on the characteristics of each major version upgrade and minor version upgrade. 

It is recommended to perform a backup to prevent data loss before the version upgrade proceeds.

<a id="perform-version-upgrades-major-version-upgrade"></a>
#### Major Version Upgrade

A major version upgrade means changing the first place of the version number. For example, upgrading from 14.6 to 17.2 is a major version upgrade. 

In RDS for PostgreSQL, the major version upgrade can only be executed on the primary, and if executed, the version upgrade is carried out for all the DB instances within the DB instance group.

<a id="perform-version-upgrades-major-version-upgrade-order"></a>
#### Major Version Upgrade Order

You can perform a major version upgrade by modifying the primary DB instance.
The order of execution is as follows:

- Conduct the version upgrade pre-check on the Primary DB instance.
    - If the pre-check results are not problematic, proceed to upgrade the version.
    - The pre-check results are provided in the form of log files and can be checked via the `pg_upgrade.log` file in the **Log** tab of the DB instance details.    
- If the Primary exists alone within the DB instance group, the version upgrade for the Primary DB instance proceeds.
    - Downtime exists during the version upgrade.
    - Repair operation may proceed if the version upgrade fails, and if successful, DB instances will be reverted to a pre-version status.
    - If the repair operation also fails, you can attempt repair by rebuilding it.
- Proceed by selecting one of the DB instances (including Standby) in non-primary replication relationship.
    - Proceed the version upgrade for selected DB instances.
        - If you have a Standby, proceed with the version upgrade by prioritizing the read replica.
        - If the version upgrade fails, the version upgrade will not proceed for other DB instances, and you can attempt to recover them with a rebuild operation.
    - Change the type to Primary for the upgraded DB instances, and reset the upgrade progress and replication relationship for the remaining DB instances in the group.
        - The access address is unchanged and can be accessed via the existing access address.
        - Downtime exists for the read copy during the version upgrade.
        - If the version upgrade fails, the replication will remain discontinued, and you can attempt repairs through a rebuild operation.

!!! warning "Caution"
    During the step of upgrading DB instances in replication relationships other than the primary, write traffic to the primary is blocked, and only read traffic can be processed.
    DB instances that have successfully upgraded their version within a DB instance group can coexist with DB instances that have failed. A failed DB instance has its replication relationship broken, and you can attempt to recover by running a rebuild operation.

<a id="perform-version-upgrades-miner-version-upgrade"></a>
#### Miner Version Upgrade

A minor version upgrade means changing the second place of the version number. For example, upgrading from 14.6 to 14.15 is a minor version upgrade.

In RDS for PostgreSQL, minor version upgrades can be performed on read replicas as well as primaries, and if performed, the version upgrade will be performed on the target DB instance. For high availability primaries, the version upgrade will also proceed for the standby.

<a id="perform-version-upgrades-minor-version-upgrade-order"></a>
#### Minor Version Upgrade Order

- If you're trying to upgrade a version for a Primary, if there's a Standby, you go through the version upgrade together.
    - Downtime exists when version upgrades are performed solely as a Primary.
    - If version upgrades are being performed with a Standby, the process will be accompanied by a restart using troubleshooting, which may result in failure.
- If you are conducting a version upgrade for a Read Replica, then the version upgrade is performed with that DB instance alone.
    - Downtime exists during the version upgrade.
    - Repair operation may proceed if the version upgrade fails, and if successful, DB instances will be reverted to a pre-version status.
    - If the repair operation also fails, you can attempt repair by rebuilding it.

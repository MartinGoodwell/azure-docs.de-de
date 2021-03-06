# Übersicht

## [Was ist SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)
## [Data Warehouse-Workload](sql-data-warehouse-overview-workload.md)
## [Verteilte Daten](sql-data-warehouse-distributed-data.md)
## [Häufig gestellte Fragen](sql-data-warehouse-overview-faq.md)

# Erste Schritte

## [Tutorial für Anfänger](sql-data-warehouse-get-started-tutorial.md)
## [bewährten Methoden](sql-data-warehouse-best-practices.md)
## [Verwalten](sql-data-warehouse-overview-manage.md)
## [Erhalten von Support](sql-data-warehouse-get-started-create-support-ticket.md)


# Anleitung

## Sichern und Wiederherstellen

### [Sicherung – Übersicht](sql-data-warehouse-backups.md)
### [Wiederherstellung – Übersicht](sql-data-warehouse-restore-database-overview.md)
#### [Azure-Portal](sql-data-warehouse-restore-database-portal.md)
#### [PowerShell](sql-data-warehouse-restore-database-powershell.md)
#### [REST](sql-data-warehouse-restore-database-rest-api.md)

## Verbinden

### [Übersicht](sql-data-warehouse-connect-overview.md)
### [SSMS](sql-data-warehouse-query-ssms.md)
### [Visual Studio](sql-data-warehouse-query-visual-studio.md)
### [Installieren von Visual Studio](sql-data-warehouse-install-visual-studio.md)
### [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md)
### [Verbindungszeichenfolgen](sql-data-warehouse-connection-strings.md)

## Erstellen
### [Azure-Portal](sql-data-warehouse-get-started-provision.md)
### [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
### [T-SQL](sql-data-warehouse-get-started-create-database-tsql.md)

## Entwickeln

### [Übersicht](sql-data-warehouse-overview-develop.md)

### Tabellen

#### [Übersicht](sql-data-warehouse-tables-overview.md)
#### [CTAS](sql-data-warehouse-develop-ctas.md)
#### [Datentypen](sql-data-warehouse-tables-data-types.md)
#### [Verteilte Tabellen](sql-data-warehouse-tables-distribute.md)
#### [Indizes](sql-data-warehouse-tables-index.md)
#### [Identität](sql-data-warehouse-tables-identity.md)
#### [Partitionen](sql-data-warehouse-tables-partition.md)
#### [Replizierte Tabellen](design-guidance-for-replicated-tables.md)
#### [Statistiken](sql-data-warehouse-tables-statistics.md)
#### [Temporär](sql-data-warehouse-tables-temporary.md)

### Abfragen

#### [Dynamischer SQL-Code](sql-data-warehouse-develop-dynamic-sql.md)
#### [Gruppierungsoptionen](sql-data-warehouse-develop-group-by-options.md)
#### [Bezeichnungen](sql-data-warehouse-develop-label.md)

### T-SQL-Sprachelemente

#### [Schleifen](sql-data-warehouse-develop-loops.md)
#### [Gespeicherten Prozeduren](sql-data-warehouse-develop-stored-procedures.md)
#### [Transaktionen](sql-data-warehouse-develop-transactions.md)
#### [Bewährte Methoden für Transaktionen](sql-data-warehouse-develop-best-practices-transactions.md)
#### [Benutzerdefinierte Schemas](sql-data-warehouse-develop-user-defined-schemas.md)
#### [Variablenzuweisung](sql-data-warehouse-develop-variable-assignment.md)
#### [Ansichten](sql-data-warehouse-develop-views.md)

## Integrieren

### [Übersicht](sql-data-warehouse-overview-integrate.md)
### [Data Factory](sql-data-warehouse-integrate-azure-data-factory.md)
### [Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md)
### [Machine Learning-Tutorial](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
### [Power BI](sql-data-warehouse-integrate-power-bi.md)
### [Power BI-Visualisierung](sql-data-warehouse-get-started-visualize-with-power-bi.md)
### [Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md)

## Laden

### [Übersicht](sql-data-warehouse-overview-load.md)
### [Beispieldaten](sql-data-warehouse-load-sample-databases.md)
### [Azure Data Lake-Speicher](sql-data-warehouse-load-from-azure-data-lake-store.md)
### [AZCopy](sql-data-warehouse-load-from-sql-server-with-azcopy.md)
### [BCP](sql-data-warehouse-load-with-bcp.md)
### [Data Factory](sql-data-warehouse-load-with-data-factory.md)
### [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
### [PolyBase-Leitfaden](sql-data-warehouse-load-polybase-guide.md)
### [PolyBase aus Blob Storage](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
### [PolyBase aus SQL Server](sql-data-warehouse-load-from-sql-server-with-polybase.md)
### [RedGate](sql-data-warehouse-load-with-redgate.md)
### [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)

## Migrieren

### [Übersicht](sql-data-warehouse-overview-migrate.md)
### [Hilfsprogramm für die Migration](sql-data-warehouse-migrate-migration-utility.md)
### [Migrieren des Schemas](sql-data-warehouse-migrate-schema.md)
### [Migrieren von Code](sql-data-warehouse-migrate-code.md)
### [Migrieren von Daten](sql-data-warehouse-migrate-data.md)
### [Migrieren zu Storage Premium](sql-data-warehouse-migrate-to-premium-storage.md)

## Verwalten von Compute

### [Übersicht](sql-data-warehouse-manage-compute-overview.md)
### [Azure-Portal](sql-data-warehouse-manage-compute-portal.md)
### [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
### [REST-API](sql-data-warehouse-manage-compute-rest-api.md)
### [T-SQL](sql-data-warehouse-manage-compute-tsql.md)

## Leistung

### [Übersicht](sql-data-warehouse-overview-manage-user-queries.md)
### [Columnstore-Komprimierung](sql-data-warehouse-memory-optimizations-for-columnstore-compression.md)
### [Überwachen](sql-data-warehouse-manage-monitor.md)
### [Workload](sql-data-warehouse-develop-concurrency.md)

## Sicherheit

### [Übersicht](sql-data-warehouse-overview-manage-security.md)
### [Überwachung](sql-data-warehouse-auditing-overview.md)
### [Überwachung für kompatible Clients](sql-data-warehouse-auditing-downlevel-clients.md)
### [Authentifizierung](sql-data-warehouse-authentication.md)
### [Verschlüsselung](sql-data-warehouse-encryption-tde.md)
### [Verschlüsselung mit T-SQL](sql-data-warehouse-encryption-tde-tsql.md)
### [Bedrohungserkennung](sql-data-warehouse-security-threat-detection.md)

## Problembehandlung
### [Problembehandlung](sql-data-warehouse-troubleshoot.md)

# Referenz

## [Kapazitätsgrenzen](sql-data-warehouse-service-capacity-limits.md)
## [T-SQL-Sprachelemente](sql-data-warehouse-reference-tsql-language-elements.md)
## [T-SQL-Anweisungen](sql-data-warehouse-reference-tsql-statements.md)
## [T-SQL-Systemsichten](sql-data-warehouse-reference-tsql-system-views.md)
## [PowerShell-Cmdlets](sql-data-warehouse-reference-powershell-cmdlets.md)

# Ressourcen
## [Azure-Roadmap](https://azure.microsoft.com/roadmap/?category=databases)
## [Forum](https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse)
## [Preise](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)
## [Dienstupdates](https://azure.microsoft.com/updates/?product=sql-data-warehouse)
## [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-sqldw/)
## [Videos](https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse)

## Partner
### [Business Intelligence](sql-data-warehouse-partner-business-intelligence.md)
### [Datenintegration](sql-data-warehouse-partner-data-integration.md)
### [Datenverwaltung](sql-data-warehouse-partner-data-management.md)

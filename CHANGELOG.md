# Change Log
All notable changes to the "sql-bigquery" extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [1.5.0] - 2021-05-09
### Added
- Added new **DDL** statements snippets
  - `CREATE SCHEMA`
    - Prefix  
      `create schema`
    - Body
      ```sql
      CREATE SCHEMA ${1:[IF NOT EXISTS]} `${2:project}.${3:dataset}`
      ${4:[OPTIONS (
        description = \"description\",
        default_kms_key_name = \"projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[KEYRING]/cryptoKeys/[KEY]\",
        default_partition_expiration_days = 1,
        default_table_expiration_days = 1,
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]
      )]}
      ```
  - `CREATE MATERIALIZED VIEW`
    - Prefix  
      `create materialized view`
    - Body
      ```sql
      CREATE MATERIALIZED VIEW ${1:[IF NOT EXISTS] }`${2:project}.${3:dataset}.${4:materialized_view}`
      ${5:[PARTITION BY
        _PARTITIONDATE
        |DATE(_PARTITIONTIME)
        |<date_column>
        |DATE(<timestamp_column>|<datetime_column>)
        |DATETIME_TRUNC(<datetime_column>, {DAY|HOUR|MONTH|YEAR\\})
        |TIMESTAMP_TRUNC(<timestamp_column>, {DAY|HOUR|MONTH|YEAR\\})
        |TIMESTAMP_TRUNC(_PARTITIONTIME, {DAY|HOUR|MONTH|YEAR\\})
        |DATE_TRUNC(<date_column>, {MONTH|YEAR\\})
        |RANGE_BUCKET(<int64_column>, GENERATE_ARRAY(<start>, <end>[, <interval>]))]}
      ${6:[CLUSTER BY clustering_column_list]}
      ${7:[OPTIONS (
        description = \"description\",
        expiration_timestamp = TIMESTAMP \"YYYY-MM-DD HH:MI:SS UTC\",
        enable_refresh = false,
        refresh_interval_minutes = 1440,
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]
      )]}
      ```
  - `CREATE EXTERNAL TABLE`
    - Prefix  
      `create external table`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }EXTERNAL TABLE ${2:[IF NOT EXISTS] }`${3:project}.${4:dataset}.${5:external_table}`
      ${6:[(
        column type OPTIONS (description = \"comment\")
      )]}
      ${7:[WITH PARTITION COLUMNS]}
      ${8:[OPTIONS (
        description = \"description\",
        allow_jagged_rows = false,
        allow_quoted_newlines = false,
        compression = \"GZIP\",
        enable_logical_types = false,
        encoding = \"UTF8\"|\"ISO_8859_1\",
        expiration_timestamp = TIMESTAMP \"YYYY-MM-DD HH:MI:SS UTC\",
        field_delimiter = \",\"|\"\\t\"|\"other\",
        format = \"AVRO\"|\"CSV\"|\"DATASTORE_BACKUP\"|\"GOOGLE_SHEETS\"|\"NEWLINE_DELIMITED_JSON\"|\"ORC\"|\"PARQUET\",
        decimal_target_types = [\"NUMERIC\", \"BIGNUMERIC\"],
        hive_partition_uri_prefix = \"gs://bucket/path\",
        ignore_unknown_values = false,
        max_bad_records = 0,
        null_marker = NULL,
        projection_fields = \"\",
        quote = \"\\\"\",
        require_hive_partition_filter = false,
        sheet_range = \"sheet1!A1:B20\",
        skip_leading_rows = 0,
        uris = [\"gs://bucket/path/*\"]
      )]}
      ```
  - `DROP SCHEMA`
    - Prefix  
      `drop schema`
    - Body
      ```sql
      DROP SCHEMA ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:dataset}` ${5:[CASCADE|RESTRICT]}
      ```
  - `DROP EXTERNAL TABLE`
    - Prefix  
      `drop external table`
    - Body
      ```sql
      DROP EXTERNAL TABLE ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:external_table}`
      ```
  - `DROP MATERIALIZED VIEW`
    - Prefix  
      `drop materialized view`
    - Body
      ```sql
      DROP MATERIALIZED VIEW ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:materialized_view}`
      ```
  - `DROP FUNCTION`
    - Prefix  
      `drop function`
    - Body
      ```sql
      DROP FUNCTION ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:functionName}`
      ```
  - `DROP PROCEDURE`
    - Prefix  
      `drop procedure`
    - Body
      ```sql
      DROP PROCEDURE ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:ProcedureName}`
      ```
  - `ALTER SCHEMA SET OPTIONS`
    - Prefix  
      `alter schema`
    - Body
      ```sql
      ALTER SCHEMA ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:dataset}`
      SET OPTIONS (
      ${5:\tdescription = \"description\",
        default_kms_key_name = \"projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[KEYRING]/cryptoKeys/[KEY]\",
        default_partition_expiration_days = 1,
        default_table_expiration_days = 1,
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]}
      )
      ```
  - `ALTER TABLE ADD COLUMN`
    - Prefix  
      `alter table add column`
    - Body
      ```sql
      ALTER TABLE `${1:project}.${2:dataset}.${3:table}`
        ADD COLUMN ${4:[IF NOT EXISTS]} ${5:column_name} ${6:type}${7: OPTIONS (description = \"comment\")}
      ```
  - `ALTER TABLE DROP COLUMN`
    - Prefix  
      `alter table drop column`
    - Body
      ```sql
      ALTER TABLE `${1:project}.${2:dataset}.${3:table}`
        DROP COLUMN ${4:[IF EXISTS]} ${5:column_name}
      ```
  - `ALTER MATERIALIZED VIEW SET OPTIONS`
    - Prefix  
      `alter materialized view`
    - Body
      ```sql
      ALTER MATERIALIZED VIEW ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:materialized_view}`
      SET OPTIONS (
      ${5:\tdescription = \"description\",
        expiration_timestamp = TIMESTAMP \"YYYY-MM-DD HH:MI:SS UTC\",
        enable_refresh = false,
        refresh_interval_minutes = 1440,
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]}
      )
      ```
- Added new `INFORMATION_SCHEMA` views snippets
  - **View name** snippets
    - **Table** metadata
      - `INFORMATION_SCHEMA.COLUMN_FIELD_PATHS`
        - Prefix  
          `infocolumnfieldpaths`
        - Body
          ```sql
          INFORMATION_SCHEMA.COLUMN_FIELD_PATHS
          ```
      - `INFORMATION_SCHEMA.PARTITIONS`
        - Prefix  
          `infopartitions`
        - Body
          ```sql
          INFORMATION_SCHEMA.PARTITIONS
          ```
    - **Job** metadata
      - `INFORMATION_SCHEMA.JOBS_BY_USER`
        - Prefix  
          `infojobsbyuser`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_BY_USER
          ```
      - `INFORMATION_SCHEMA.JOBS_BY_PROJECT`
        - Prefix  
          `infojobsbyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.JOBS_BY_FOLDER`
        - Prefix  
          `infojobsbyfolder`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_BY_FOLDER
          ```
      - `INFORMATION_SCHEMA.JOBS_BY_ORGANIZATION`
        - Prefix  
          `infojobsbyorganization`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_BY_ORGANIZATION
          ```
    - **Job timeline** metadata
      - `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER`
        - Prefix  
          `infojobstimelinebyuser`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER
          ```
      - `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_PROJECT`
        - Prefix  
          `infojobstimelinebyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_TIMELINE_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER`
        - Prefix  
          `infojobstimelinebyfolder`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER
          ```
      - `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION`
        - Prefix  
          `infojobstimelinebyorganization`
        - Body
          ```sql
          INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION
          ```
    - **Reservations** metadata
      - `INFORMATION_SCHEMA.RESERVATION_CHANGES_BY_PROJECT`
        - Prefix  
          `inforeservationchangesbyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.RESERVATION_CHANGES_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.RESERVATIONS_BY_PROJECT`
        - Prefix  
          `inforeservationsbyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.RESERVATIONS_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES_BY_PROJECT`
        - Prefix  
          `infocapacitycommitmentchangesby_project`
        - Body
          ```sql
          INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.CAPACITY_COMMITMENTS_BY_PROJECT`
        - Prefix  
          `infocapacitycommitmentsbyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.CAPACITY_COMMITMENTS_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.ASSIGNMENT_CHANGES_BY_PROJECT`
        - Prefix  
          `infoassignmentchangesbyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.ASSIGNMENT_CHANGES_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT`
        - Prefix  
          `infoassignmentsbyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT
          ```
    - **Routine** metadata
      - `INFORMATION_SCHEMA.ROUTINES`
        - Prefix  
          `inforoutines`
        - Body
          ```sql
          INFORMATION_SCHEMA.ROUTINES
          ```
      - `INFORMATION_SCHEMA.ROUTINE_OPTIONS`
        - Prefix  
          `inforoutineoptions`
        - Body
          ```sql
          INFORMATION_SCHEMA.ROUTINE_OPTIONS
          ```
      - `INFORMATION_SCHEMA.PARAMETERS`
        - Prefix  
          `infoparameters`
        - Body
          ```sql
          INFORMATION_SCHEMA.PARAMETERS
          ```
    - **Streaming** metadata
      - `INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_PROJECT`
        - Prefix  
          `infostreamingtimelinebyproject`
        - Body
          ```sql
          INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_PROJECT
          ```
      - `INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_FOLDER`
        - Prefix  
          `infostreamingtimelinebyfolder`
        - Body
          ```sql
          INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_FOLDER
          ```
      - `INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_ORGANIZATION`
        - Prefix  
          `infostreamingtimelinebyorganization`
        - Body
          ```sql
          INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_ORGANIZATION
          ```
  - **SELECT query** snippets
    - **Table** metadata
      - `SELECT ... FROM INFORMATION_SCHEMA.COLUMN_FIELD_PATHS`
        - Prefix  
          `select info columnfieldpaths`
        - Body
          ```sql
          SELECT
            table_catalog,
            table_schema,
            table_name,
            column_name,
            field_path,
            data_type,
            description
          FROM
            `${1:project}.${2:dataset}`.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS
          ORDER BY
            table_name, column_name
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.PARTITIONS`
        - Prefix  
          `select info partitions`
        - Body
          ```sql
          SELECT
            table_catalog,
            table_schema,
            table_name,
            partition_id,
            total_rows,
            total_logical_bytes,
            total_billable_bytes,
            last_modified_time,
            storage_tier
          FROM
            `${1:project}.${2:dataset}`.INFORMATION_SCHEMA.PARTITIONS
          ORDER BY
            table_name, partition_id DESC
          ```
    - **Job** metadata
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_BY_USER`
        - Prefix  
          `select info jobsbyuser`
        - Body
          ```sql
          SELECT
            creation_time,
            project_id,
            project_number,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            start_time,
            end_time,
            query,
            state,
            reservation_id,
            total_bytes_processed,
            total_slot_ms,
            error_result,
            cache_hit,
            destination_table,
            referenced_tables,
            labels,
            timeline,
            job_stages,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_BY_USER
          ORDER BY
            creation_time DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_BY_PROJECT`
        - Prefix  
          `select info jobsbyproject`
        - Body
          ```sql
          SELECT
            creation_time,
            project_id,
            project_number,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            start_time,
            end_time,
            query,
            state,
            reservation_id,
            total_bytes_processed,
            total_slot_ms,
            error_result,
            cache_hit,
            destination_table,
            referenced_tables,
            labels,
            timeline,
            job_stages,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
          ORDER BY
            creation_time DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_BY_FOLDER`
        - Prefix  
          `select info jobsbyfolder`
        - Body
          ```sql
          SELECT
            creation_time,
            project_id,
            project_number,
            folder_numbers,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            start_time,
            end_time,
            state,
            reservation_id,
            total_bytes_processed,
            total_slot_ms,
            error_result,
            cache_hit,
            destination_table,
            referenced_tables,
            labels,
            timeline,
            job_stages,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_BY_FOLDER
          ORDER BY
            creation_time DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_BY_ORGANIZATION`
        - Prefix  
          `select info jobsbyorganization`
        - Body
          ```sql
          SELECT
            creation_time,
            project_id,
            project_number,
            folder_numbers,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            start_time,
            end_time,
            state,
            reservation_id,
            total_bytes_processed,
            total_slot_ms,
            error_result,
            cache_hit,
            destination_table,
            referenced_tables,
            labels,
            timeline,
            job_stages,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_BY_ORGANIZATION
          ORDER BY
            creation_time DESC
          ```
    - **Job timeline** metadata
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER`
        - Prefix  
          `select info jobstimelinebyuser`
        - Body
          ```sql
          SELECT
            period_start,
            period_slot_ms,
            project_id,
            project_number,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            job_creation_time,
            job_start_time,
            job_end_time,
            state,
            reservation_id,
            total_bytes_processed,
            error_result,
            cache_hit,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER
          ORDER BY
            period_start DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_TIMELINE_BY_PROJECT`
        - Prefix  
          `select info jobstimelinebyproject`
        - Body
          ```sql
          SELECT
            period_start,
            period_slot_ms,
            project_id,
            project_number,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            job_creation_time,
            job_start_time,
            job_end_time,
            state,
            reservation_id,
            total_bytes_processed,
            error_result,
            cache_hit,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_PROJECT
          ORDER BY
            period_start DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER`
        - Prefix  
          `select info jobstimelinebyfolder`
        - Body
          ```sql
          SELECT
            period_start,
            period_slot_ms,
            project_id,
            project_number,
            folder_numbers,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            job_creation_time,
            job_start_time,
            job_end_time,
            state,
            reservation_id,
            total_bytes_processed,
            error_result,
            cache_hit,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER
          ORDER BY
            period_start DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION`
        - Prefix  
          `select info jobstimelinebyorganization`
        - Body
          ```sql
          SELECT
            period_start,
            period_slot_ms,
            project_id,
            project_number,
            folder_numbers,
            user_email,
            job_id,
            job_type,
            statement_type,
            priority,
            job_creation_time,
            job_start_time,
            job_end_time,
            state,
            reservation_id,
            total_bytes_processed,
            error_result,
            cache_hit,
            total_bytes_billed,
            parent_job_id
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION
          ORDER BY
            period_start DESC
          ```
    - **Reservations** metadata
      - `SELECT ... FROM INFORMATION_SCHEMA.RESERVATION_CHANGES_BY_PROJECT`
        - Prefix  
          `select info reservationchangesbyproject`
        - Body
          ```sql
          SELECT
            change_timestamp,
            project_id,
            project_number,
            reservation_name,
            ignore_idle_slots,
            action,
            slot_capacity,
            user_email
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.RESERVATION_CHANGES_BY_PROJECT
          ORDER BY
            change_timestamp DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.RESERVATIONS_BY_PROJECT`
        - Prefix  
          `select info reservationsbyproject`
        - Body
          ```sql
          SELECT
            project_id,
            project_number,
            reservation_name,
            ignore_idle_slots,
            slot_capacity
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.RESERVATIONS_BY_PROJECT
          ORDER BY
            project_id
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES_BY_PROJECT`
        - Prefix  
          `select info capacitycommitmentchangesbyproject`
        - Body
          ```sql
          SELECT
            change_timestamp,
            project_id,
            project_number,
            capacity_commitment_id,
            commitment_plan,
            state,
            slot_count,
            action,
            user_email,
            commitment_start_time,
            commitment_end_time,
            failure_status,
            renewal_plan
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES_BY_PROJECT
          ORDER BY
            change_timestamp DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.CAPACITY_COMMITMENTS_BY_PROJECT`
        - Prefix  
          `select info capacitycommitmentsbyproject`
        - Body
          ```sql
          SELECT
            project_id,
            project_number,
            capacity_commitment_id,
            commitment_plan,
            state,
            slot_count
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.CAPACITY_COMMITMENTS_BY_PROJECT
          ORDER BY
            project_id
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.ASSIGNMENT_CHANGES_BY_PROJECT`
        - Prefix  
          `select info assignmentchangesbyproject`
        - Body
          ```sql
          SELECT
            change_timestamp,
            project_id,
            project_number,
            assignment_id,
            reservation_name,
            job_type,
            assignee_id,
            assignee_number,
            assignee_type,
            action,
            user_email,
            state
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.ASSIGNMENT_CHANGES_BY_PROJECT
          ORDER BY
            change_timestamp DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT`
        - Prefix  
          `select info assignmentsbyproject`
        - Body
          ```sql
          SELECT
            project_id,
            project_number,
            assignment_id,
            reservation_name,
            job_type,
            assignee_id,
            assignee_number,
            assignee_type
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT
          ORDER BY
            project_id
          ```
    - **Routine** metadata
      - `SELECT ... FROM INFORMATION_SCHEMA.ROUTINES`
        - Prefix  
          `select info routines`
        - Body
          ```sql
          SELECT
            specific_catalog,
            specific_schema,
            specific_name,
            routine_catalog,
            routine_schema,
            routine_name,
            routine_type,
            data_type,
            routine_body,
            routine_definition,
            external_language,
            is_deterministic,
            security_type,
            created,
            last_modified
          FROM
            `${1:project}.${2:dataset}`.INFORMATION_SCHEMA.ROUTINES
          ORDER BY
            specific_catalog, specific_schema, specific_name
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.ROUTINE_OPTIONS`
        - Prefix  
          `select info routineoptions`
        - Body
          ```sql
          SELECT
            specific_catalog,
            specific_schema,
            specific_name,
            option_name,
            option_type,
            option_value
          FROM
            `${1:project}.${2:dataset}`.INFORMATION_SCHEMA.ROUTINE_OPTIONS
          ORDER BY
            specific_catalog, specific_schema, specific_name, option_name
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.PARAMETERS`
        - Prefix  
          `select info parameters`
        - Body
          ```sql
          SELECT
            specific_catalog,
            specific_schema,
            specific_name,
            ordinal_position,
            parameter_mode,
            is_result,
            parameter_name,
            data_type,
            parameter_default,
            is_aggregate
          FROM
            `${1:project}.${2:dataset}`.INFORMATION_SCHEMA.PARAMETERS
          ORDER BY
            specific_catalog, specific_schema, specific_name, ordinal_position
          ```
    - **Streaming** metadata
      - `SELECT ... FROM INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_PROJECT`
        - Prefix  
          `select info streamingtimelinebyproject`
        - Body
          ```sql
          SELECT
            start_timestamp,
            project_id,
            project_number,
            dataset_id,
            table_id,
            error_code,
            total_requests,
            total_rows,
            total_input_bytes
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_PROJECT
          ORDER BY
            start_timestamp DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_FOLDER`
        - Prefix  
          `select info streamingtimelinebyfolder`
        - Body
          ```sql
          SELECT
            start_timestamp,
            project_id,
            project_number,
            dataset_id,
            table_id,
            error_code,
            total_requests,
            total_rows,
            total_input_bytes
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_FOLDER
          ORDER BY
            start_timestamp DESC
          ```
      - `SELECT ... FROM INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_ORGANIZATION`
        - Prefix  
          `select info streamingtimelinebyorganization`
        - Body
          ```sql
          SELECT
            start_timestamp,
            project_id,
            project_number,
            dataset_id,
            table_id,
            error_code,
            total_requests,
            total_rows,
            total_input_bytes
          FROM
            `region-${1:(us|eu|region_name)}`.INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_ORGANIZATION
          ORDER BY
            start_timestamp DESC
          ```

### Changed
- Changed **single line comment symbol** from `--` to `#`
- Changed **DDL** statements snippets
  - `CREATE TABLE`
    - Prefix  
      `create table`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }TABLE ${2:[IF NOT EXISTS] }`${3:project}.${4:dataset}.${5:table}`
      (
        ${6:column} ${7:type}${8: OPTIONS (description = \"comment\")}
      )
      ${9:[PARTITION BY
        _PARTITIONDATE
        |DATE(_PARTITIONTIME)
        |<date_column>
        |DATE(<timestamp_column>|<datetime_column>)
        |DATETIME_TRUNC(<datetime_column>, {DAY|HOUR|MONTH|YEAR\\})
        |TIMESTAMP_TRUNC(<timestamp_column>, {DAY|HOUR|MONTH|YEAR\\})
        |TIMESTAMP_TRUNC(_PARTITIONTIME, {DAY|HOUR|MONTH|YEAR\\})
        |DATE_TRUNC(<date_column>, {MONTH|YEAR\\})
        |RANGE_BUCKET(<int64_column>, GENERATE_ARRAY(<start>, <end>[, <interval>]))]}
      ${10:[CLUSTER BY clustering_column_list]}
      ${11:[OPTIONS (
        description = \"description\",
        expiration_timestamp = TIMESTAMP \"YYYY-MM-DD HH:MI:SS UTC\",
        partition_expiration_days = 1,
        require_partition_filter = false,
        kms_key_name = \"projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[KEYRING]/cryptoKeys/[KEY]\",
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]
      )]}
      ```
  - `CREATE VIEW`
    - Prefix  
      `create view`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }VIEW ${2:[IF NOT EXISTS] }`${4:project}.${5:dataset}.${6:view}`
      ${7:[OPTIONS (
        description = \"description\",
        expiration_timestamp = TIMESTAMP \"YYYY-MM-DD HH:MI:SS UTC\",
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]
      )]}
      AS
      SELECT
        ${8:column}
      FROM `${9:project}.${10:dataset}.${11:table}`
      ```
  - `PARTITION BY`
    - Prefix  
      `partitionby`
    - Body
      ```sql
      PARTITION BY
        ${1:_PARTITIONDATE}
        ${2:|DATE(_PARTITIONTIME)}
        ${3:|<date_column>}
        ${4:|DATE(<timestamp_column>|<datetime_column>)}
        ${5:|DATETIME_TRUNC(<datetime_column>, {DAY|HOUR|MONTH|YEAR\\})}
        ${6:|TIMESTAMP_TRUNC(<timestamp_column>, {DAY|HOUR|MONTH|YEAR\\})}
        ${7:|TIMESTAMP_TRUNC(_PARTITIONTIME, {DAY|HOUR|MONTH|YEAR\\})}
        ${8:|DATE_TRUNC(<date_column>, {MONTH|YEAR\\})}
        ${9:|RANGE_BUCKET(<int64_column>, GENERATE_ARRAY(<start>, <end>[, <interval>]))}
      ${10:[CLUSTER BY clustering_column_list]}
      ```
  - `CREATE TEMPORARY JavaScript FUNCTION`
    - Prefix  
      `create temp function javascript`
    - Body
      ```sql
      CREATE TEMP FUNCTION ${1:functionName}(${2:param_name param_type[, ...]})
      RETURNS ${3:data_type}
      LANGUAGE js
      ${4:[OPTIONS (library = [\"gs://bucket/path/file.js\"])]}
      AS \"\"\
        ${5:return \"expression\";}
      \"\"\";
      ```
  - `CREATE TEMPORARY SQL FUNCTION`
    - Prefix  
      `create temp function sql`
    - Body
      ```sql
      CREATE TEMP FUNCTION ${1:functionName}(${2:param_name param_type[, ...]})
      ${3:[RETURNS data_type]}
      AS (
        ${4:sql_expression}
      );
      ```
  - `CREATE JavaScript FUNCTION`
    - Prefix  
      `create function javascript`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }FUNCTION ${2:[IF NOT EXISTS] }`${3:project}.${4:dataset}.${5:functionName}`(${6:param_name param_type[, ...]})
      RETURNS ${7:data_type}
      LANGUAGE js
      ${8:[OPTIONS (library = [\"gs://bucket/path/file.js\"])]}
      AS \"\"\
        ${9:return \"expression\";}
      \"\"\";
      ```
  - `CREATE SQL FUNCTION`
    - Prefix  
      `create function sql`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }FUNCTION ${2:[IF NOT EXISTS] }`${3:project}.${4:dataset}.${5:functionName}`(${6:param_name param_type[, ...]})
      ${7:[RETURNS data_type]}
      AS (
        ${8:sql_expression}
      );
      ```
  - `CREATE PROCEDURE`
    - Prefix  
      `create procedure`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }PROCEDURE ${2:[IF NOT EXISTS] }`${3:project}.${4:dataset}.${5:ProcedureName}`(${6:[IN|OUT|INOUT] arg_name arg_type[, ...]})
      ${7:[OPTIONS (strict_mode = TRUE|FALSE)]}
      BEGIN
        ${8:statements}
      END;
      ```
  - `CREATE MODEL`
    - Prefix  
      `create model`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }MODEL ${2:[IF NOT EXISTS] }`${3:project}.${4:dataset}.${5:model}`
      ${6:[OPTIONS (model_option_list)]}
      AS
      ${7:query_statement}
      ```
  - `DROP TABLE`
    - Prefix  
      `drop table`
    - Body
      ```sql
      DROP TABLE ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:table}`
      ```
  - `DROP VIEW`
    - Prefix  
      `drop view`
    - Body
      ```sql
      DROP VIEW ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:view}`
      ```
  - `ALTER TABLE SET OPTIONS`
    - Prefix  
      `alter table options`
    - Body
      ```sql
      ALTER TABLE ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:table}`
      SET OPTIONS (
      ${5:\tdescription = \"description\",
        expiration_timestamp = TIMESTAMP \"YYYY-MM-DD HH:MI:SS UTC\",
        partition_expiration_days = 1,
        require_partition_filter = false,
        kms_key_name = \"projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[KEYRING]/cryptoKeys/[KEY]\",
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]}
      )
      ```
  - `ALTER VIEW SET OPTIONS`
    - Prefix  
      `alter view`
    - Body
      ```sql
      ALTER VIEW ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:view}`
      SET OPTIONS (
      ${5:\tdescription = \"description\",
        expiration_timestamp = TIMESTAMP \"YYYY-MM-DD HH:MI:SS UTC\",
        friendly_name = \"friendly_name\",
        labels = [(\"key\", \"value\")]}
      )
      ```

### Removed
- Removed **DDL** statements snippets
  - `CREATE TABLE IF NOT EXISTS`
  - `CREATE OR REPLACE TABLE`
  - `CREATE TABLE ... PARTITION BY`
  - `CREATE JavaScript FUNCTION IF NOT EXISTS`
  - `CREATE SQL FUNCTION IF NOT EXISTS`
  - `DROP TABLE IF EXISTS`
  - `DROP VIEW IF EXISTS`
  - `ALTER TABLE IF EXISTS SET OPTIONS`
  - `ALTER VIEW IF EXISTS SET OPTIONS`


### Fixed
- Fixed **regular expression syntax** with **quote character**
- Miner fixed


## [1.4.0] - 2019-10-14
### Added
- Add supports `RANGE_BUCKET` mathematical functions
  - Supports syntax highlighting
  - Add snippets
    - `RANGE_BUCKET`
        - Prefix  
          `range_bucket`
        - body
          ```sql
          RANGE_BUCKET(point, boundaries_array)
          ```
  - Document
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#range_bucket
- Add supports temporary tables
  - Supports syntax highlighting
  - Add snippets
    - `CREATE TEMPORARY TABLE`
        - Prefix  
          `create temp table`
        - body
          ```sql
          CREATE OR REPLACE TEMP TABLE table_name
          (
            column type OPTIONS (description = "comment")
          )
          ```
  - Document
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#temporary_tables
- Add supports Persistent UDF
  - Supports syntax highlighting
  - Add snippets
    - `CREATE JavaScript FUNCTION`
        - Prefix  
          `create function javascript`
        - body
          ```sql
          CREATE OR REPLACE FUNCTION `project.dataset.functionName`(param_name param_type[, ...])
          RETURNS data_type
          LANGUAGE js AS """
            return "expression";
          """;
          ```
    - `CREATE SQL FUNCTION`
        - Prefix  
          `create function sql`
        - body
          ```sql
          CREATE OR REPLACE FUNCTION `project.dataset.functionName`(param_name param_type[, ...])
          [RETURNS data_type]
          AS (
            sql_expression
          );
          ```
    - `CREATE JavaScript FUNCTION IF NOT EXISTS`
        - Prefix  
          `create function javascript if not exists`
        - body
          ```sql
          CREATE FUNCTION IF NOT EXISTS `project.dataset.functionName`(param_name param_type[, ...])
          RETURNS data_type
          LANGUAGE js AS """
            return "expression";
          """;
          ```
    - `CREATE SQL FUNCTION IF NOT EXISTS`
        - Prefix  
          `create function sql if not exists`
        - body
          ```sql
          CREATE FUNCTION IF NOT EXISTS `project.dataset.functionName`(param_name param_type[, ...])
          [RETURNS data_type]
          AS (
            sql_expression
          );
          ```
  - Document
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/user-defined-functions
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement
- Add supports scripting, and stored procedures
  - Supports syntax highlighting
  - Add snippets
    - `CREATE PROCEDURE`
        - Prefix  
          `create procedure`
        - body
          ```sql
          CREATE OR REPLACE PROCEDURE `project.dataset.ProcedureName`([IN|OUT|INOUT] arg_name arg_type[, ...])
          BEGIN
            statements
          END;
          ```
    - `CALL PROCEDURE`
        - Prefix  
          `call procedure`
        - body
          ```sql
          CALL `project.dataset.ProcedureName`(arg[, ...]);
          ```
    - `DECLARE`
        - Prefix  
          `declare`
        - body
          ```sql
          DECLARE variable_name[, ...] variable_type [DEFAULT expression];
          ```
    - `SET`
        - Prefix  
          `set`
        - body
          ```sql
          SET variable_name = expression;
          ```
    - `SET multiple`
        - Prefix  
          `set multiple`
        - body
          ```sql
          SET (variable_name_1, ...) = (expression_1, ...);
          ```
    - `SET from query`
        - Prefix  
          `set query`
        - body
          ```sql
          SET variable_name = (SELECT query);
          ```
    - `BEGIN ... END`
        - Prefix  
          `begin/end`
        - body
          ```sql
          BEGIN
            statements
          END;
          ```
    - `IF ... THEN`
        - Prefix  
          `if`
        - body
          ```sql
          IF condition THEN
            statements
          END IF;
          ```
    - `IF ... THEN ELSE`
        - Prefix  
          `if/else`
        - body
          ```sql
          IF condition THEN
            statements
          ELSE
            statements
          END IF;
          ```
    - `ELSE`
        - Prefix  
          `else`
        - body
          ```sql
          ELSE
            statements
          ```
    - `IF EXISTS query THEN`
        - Prefix  
          `if exists query`
        - body
          ```sql
          IF EXISTS (SELECT expression FROM `project.dataset.table` WHERE condition) THEN
            statements
          END IF;
          ```
    - `LOOP`
        - Prefix  
          `loop`
        - body
          ```sql
          LOOP
            statements
          END LOOP;
          ```
    - `WHILE`
        - Prefix  
          `while`
        - body
          ```sql
          WHILE expression DO
            statements
          END WHILE;
          ```
    - `BREAK`
        - Prefix  
          `break`
        - body
          ```sql
          BREAK;
          ```
    - `LEAVE`
        - Prefix  
          `leave`
        - body
          ```sql
          LEAVE;
          ```
    - `CONTINUE`
        - Prefix  
          `continue`
        - body
          ```sql
          CONTINUE;
          ```
    - `ITERATE`
        - Prefix  
          `iterate`
        - body
          ```sql
          ITERATE;
          ```
    - `RETURN`
        - Prefix  
          `return`
        - body
          ```sql
          RETURN;
          ```
  - Document
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/scripting


### Changed
- Change Temporary UDF snippets
  - Snippets
    - `CREATE TEMPORARY JavaScript FUNCTION`
        - Prefix  
          `create function javascript` -> `create temp function javascript`
        - body
          ```sql
          CREATE OR REPLACE TEMP FUNCTION functionName(param_name param_type[, ...])
          RETURNS data_type
          LANGUAGE js AS """
            return "expression";
          """;
          ```
    - `CREATE TEMPORARY SQL FUNCTION`
        - Prefix  
          `create function sql` -> `create temp function sql`
        - body
          ```sql
          CREATE OR REPLACE TEMP FUNCTION functionName(param_name param_type[, ...])
          [RETURNS data_type]
          AS (
            sql_expression
          );
          ```
  - Document
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/user-defined-functions
    - https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement


## [1.3.0] - 2019-07-14
### Added
- Add BigQuery ML supports the `DROP MODEL` DDL statement for deleting models.

### Changed
- Add description option to `CREATE TABLE` statements.
  - Example
    - Prefix  
      `create table`
    - Body
      - old
        ```sql
        CREATE TABLE `project.dataset.table`
        (
          column type
        )
        ```
      - new
        ```sql
        CREATE TABLE `project.dataset.table`
        (
          column type OPTIONS (description = "comment")
        )
        ```


## [1.2.0] - 2019-04-21
### Added
- Add supports AEAD encryption functions
  - Supported syntax highlighting
  - Added snippets
  - Document  
    https://cloud.google.com/bigquery/docs/reference/standard-sql/aead_encryption_functions
  - Functions

    |Function Name|Prefix|Body|
    |:--|:--|:--|
    |`KEYS.NEW_KEYSET`|`keysnew_keyset`|`KEYS.NEW_KEYSET(key_type)`|
    |`KEYS.ADD_KEY_FROM_RAW_BYTES`|`keysadd_key_from_raw_bytes`|`KEYS.ADD_KEY_FROM_RAW_BYTES(keyset, key_type, raw_key_bytes)`|
    |`AEAD.DECRYPT_BYTES`|`aeaddecrypt_bytes`|`AEAD.DECRYPT_BYTES(keyset, ciphertext, additional_data)`|
    |`AEAD.DECRYPT_STRING`|`aeaddecrypt_string`|`AEAD.DECRYPT_STRING(keyset, ciphertext, additional_data)`|
    |`AEAD.ENCRYPT`|`aeadencrypt`|`AEAD.ENCRYPT(keyset, plaintext, additional_data)`|
    |`KEYS.KEYSET_FROM_JSON`|`keyskeyset_from_json`|`KEYS.KEYSET_FROM_JSON(json_keyset)`|
    |`KEYS.KEYSET_TO_JSON`|`keyskeyset_to_json`|`KEYS.KEYSET_TO_JSON(keyset)`|
    |`KEYS.ROTATE_KEYSET`|`keysrotate_keyset`|`KEYS.ROTATE_KEYSET(keyset, key_type)`|

### Fixed
- Miner fixed


## [1.1.0] - 2019-03-17
### Added
- Initial release


[1.5.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.4.0...v1.5.0
[1.4.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.3.0...v1.4.0
[1.3.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.2.0...v1.3.0
[1.2.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/releases/tag/v1.1.0

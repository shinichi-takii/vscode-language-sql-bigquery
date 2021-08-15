# Change Log
All notable changes to the "sql-bigquery" extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [1.9.0] - 2021-08-16
### Added
- Added supports **parameterized types**.
  - `STRING(L)`
  - `BYTES(L)`
  - `NUMERIC(P)` / `NUMERIC(P, S)`
  - `BIGNUMERIC(P)` / `BIGNUMERIC(P, S)`
- Added supports new **data types**.
  - `INTERVAL`
- Added supports **Numeric type INT64 aliases**.
  - `SMALLINT`
  - `INTEGER`
  - `BIGINT`
  - `TINYINT`
  - `BYTEINT`
- Added all **data types** snippets.
- Added supports **table snapshot**
  - `CREATE SNAPSHOT TABLE` DDL statements.
  - `INFORMATION_SCHEMA.TABLE_SNAPSHOTS` table.
- Added supports **Table functions (TVF)** DDL statements.
  - `CREATE TABLE FUNCTION`
  - `DROP TABLE FUNCTION`
- Added supports new `ALTER COLUMN` DDL statements.
  - `ALTER COLUMN SET OPTIONS`
  - `ALTER COLUMN SET DATA TYPE`
- Added supports new **casting** functions.
  - `PARSE_BIGNUMERIC()`
  - `PARSE_NUMERIC()`
  - Added `FORMAT` parameter to `CAST()` function
- Added supports new **casting** functions.
  - `ST_GEOGFROM()`
- Added supports **DCL** statements.
  - `GRANT`
  - `REVOKE`
  - `INFORMATION_SCHEMA.OBJECT_PRIVILEGES`

### Changed
- Changed the use single line comment symbol from `#` to `--`.
  - BigQuery UI reswitched comment symbol from `#` to `--`.

### Fixed
- Minor fixed.


## [1.8.0] - 2021-05-23
### Added
- Added supports new **Geography** functions snippets.
  - `ST_STARTPOINT`
    - Prefix  
      `st_startpoint`
    - Body
      ```sql
      ST_STARTPOINT(${1:linestring_geography})
      ```
  - `ST_ENDPOINT`
    - Prefix  
      `st_endpoint`
    - Body
      ```sql
      ST_ENDPOINT(${1:linestring_geography})
      ```
  - `ST_POINTN`
    - Prefix  
      `st_pointn`
    - Body
      ```sql
      ST_POINTN(${1:linestring_geography}, ${2:index})
      ```


## [1.7.0] - 2021-05-20
### Added
- Added supports `ALTER TABLE RENAME TO` statement snippets.
  - `ALTER TABLE RENAME TO`
    - Prefix  
      `alter table rename`
    - Body
      ```sql
      ALTER TABLE ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:table}`
        RENAME TO ${5:new_table_name}
      ```

### Fixed
- Minor fixed.


## [1.6.1] - 2021-05-17
### Fixed
- Fixed `BEGIN ... END` snippets prefix
  - `BEGIN ... END`
    - Prefix  
      `begin/end` -> `begin end`


## [1.6.0] - 2021-05-16
### Added
- Added supports new **Data types** syntax.
  - `GEOGRAPHY`
  - `DECIMAL`
  - `BIGNUMERIC`
  - `BIGDECIMAL`
- Added supports new **JSON** functions.
  - `JSON_QUERY`
    - Prefix  
      `json_query`
    - Body
      ```sql
      JSON_QUERY(${1:"json_string_expr"}, ${2:"json_path"})
      ```
    - Description
      ```
      Extracts a JSON values.
      ```
  - `JSON_VALUE`
    - Prefix  
      `json_value`
    - Body
      ```sql
      JSON_VALUE(${1:"json_string_expr"}, ${2:"json_path"})
      ```
    - Description
      ```
      Extracts a scalar value.
      ```
  - `JSON_EXTRACT_ARRAY`
    - Prefix  
      `json_extract_array`
    - Body
      ```sql
      JSON_EXTRACT_ARRAY(${1:'json_string_expr'}, ${2:'json_path'})
      ```
    - Description
      ```
      Extracts an array of JSON values. (Legacy JSON function, recommend using `JSON_QUERY_ARRAY`)
      ```
  - `JSON_QUERY_ARRAY`
    - Prefix  
      `json_query_array`
    - Body
      ```sql
      JSON_QUERY_ARRAY(${1:"json_string_expr"}, ${2:"json_path"})
      ```
    - Description
      ```
      Extracts an array of JSON values.
      ```
  - `JSON_EXTRACT_STRING_ARRAY`
    - Prefix  
      `json_extract_string_array`
    - Body
      ```sql
      JSON_EXTRACT_STRING_ARRAY(${1:'json_string_expr'}, ${2:'json_path'})
      ```
    - Description
      ```
      Extracts an array of scalar values. (Legacy JSON function, recommend using `JSON_VALUE_ARRAY`)
      ```
  - `JSON_VALUE_ARRAY`
    - Prefix  
      `json_value_array`
    - Body
      ```sql
      JSON_VALUE_ARRAY(${1:"json_string_expr"}, ${2:"json_path"})
      ```
    - Description
      ```
      Extracts an array of scalar values.
      ```
- Added supports new **Scripting**.
  - `EXECUTE IMMEDIATE`
    - Prefix  
      `execute immediate`
    - Body
      ```sql
      EXECUTE IMMEDIATE
        ${1:"sql_expression @parameter_name"}
        ${2:[INTO variable]}
        ${3:[USING value AS parameter_name]};
      ```
    - Description
      ```
      Executes a dynamic SQL statement on the fly.
      ```
  - `IF ... ELSEIF ... ELSE`
    - Prefix  
      `if elseif else`
    - Body
      ```sql
      IF ${1:condition} THEN
        ${2:statements}
      ELSEIF ${3:condition} THEN
        ${4:statements}
      ELSE
        ${5:statements}
      END IF;
      ```
  - `RAISE`
    - Prefix  
      `raise`
    - Body
      ```sql
      RAISE ${1:[USING MESSAGE = "message"]};
      ```
    - Description
      ```
      Raises an error.
      ```
- Added supports new **Geography** functions.
  - `ST_GEOGFROMWKB`
    - Prefix  
      `st_geogfromwkb`
    - Body
      ```sql
      ST_GEOGFROMWKB(${1:wkb_bytes_expression|wkb_hex_string_expression})
      ```
  - `ST_GEOGPOINTFROMGEOHASH`
    - Prefix  
      `st_geogpointfromgeohash`
    - Body
      ```sql
      ST_GEOGPOINTFROMGEOHASH(${1:geohash})
      ```
  - `ST_ASBINARY`
    - Prefix  
      `st_asbinary`
    - Body
      ```sql
      ST_ASBINARY(${1:geography_expression})
      ```
  - `ST_GEOHASH`
    - Prefix  
      `st_geohash`
    - Body
      ```sql
      ST_GEOHASH(${1:geography_expression}, ${2:maxchars})
      ```
  - `ST_CENTROID_AGG`
    - Prefix  
      `st_centroid_agg`
    - Body
      ```sql
      ST_CENTROID_AGG(${1:geography})
      ```
  - `ST_CONVEXHULL`
    - Prefix  
      `st_convexhull`
    - Body
      ```sql
      ST_CONVEXHULL(${1:geography_expression})
      ```
  - `ST_DUMP`
    - Prefix  
      `st_dump`
    - Body
      ```sql
      ST_DUMP(${1:geography}${2:[, dimension]})
      ```
  - `ST_SIMPLIFY`
    - Prefix  
      `st_simplify`
    - Body
      ```sql
      ST_SIMPLIFY(${1:geography}, ${2:tolerance_meters})
      ```
  - `ST_CLUSTERDBSCAN`
    - Prefix  
      `st_clusterdbscan`
    - Body
      ```sql
      ST_CLUSTERDBSCAN(${1:geography_column}, ${2:epsilon}, ${3:minimum_geographies}) OVER (${4:...})
      ```
  - `ST_NPOINTS`
    - Prefix  
      `st_npoints`
    - Body
      ```sql
      ST_NPOINTS(${1:geography_expression})
      ```
  - `ST_X`
    - Prefix  
      `st_x`
    - Body
      ```sql
      ST_X(${1:geography_expression})
      ```
  - `ST_Y`
    - Prefix  
      `st_y`
    - Body
      ```sql
      ST_Y(${1:geography_expression})
      ```
  - `ST_GEOGFROMTEXT`
    - Prefix  
      `st_geogfromtext`
    - Body
      ```sql
      ST_GEOGFROMTEXT(${1:wkt_string}${2:[, oriented => boolean_constant_1]}${3:[, planar => boolean_constant_2]}${4:[, make_valid => boolean_constant_3]})
      ```
- Added supports **Debugging statements** syntax.
  - `ASSERT`
    - Prefix  
      `assert`
    - Body
      ```sql
      ASSERT ${1:expression}${2: [AS "description"]}
      ```
- Added supports `BQ.JOBS.CANCEL` snippets.
  - `BQ.JOBS.CANCEL`
    - Prefix  
    `call bq jobs cancel`
    - Body
      ```sql
      CALL BQ.JOBS.CANCEL(${1:"project-id.job_id"});
      ```
    - Description
      ```
      Canceling a job.
      ```
- Added `EXPORT DATA` snippets.
  - `EXPORT DATA`
    - Prefix  
      `export data`
    - Body
      ```sql
      EXPORT DATA
      OPTIONS (
        ${1:format = "AVRO"|"CSV"|"JSON"|"PARQUET",}
        ${2:compression = "GZIP"|"DEFLATE"|"SNAPPY",}
        ${3:field_delimiter = ","|"\t"|"other",}
        ${4:header = false|true,}
        ${5:overwrite = false|true,}
        ${6:uri = "gs://bucket/path/file_*.csv.gz"}
      ) AS
      query_statement
      ```
- Added supports new **DML** syntax.
  - `TRUNCATE TABLE`
    - Prefix  
      `truncate table`
    - Body
      ```sql
      TRUNCATE TABLE `${1:project}.${2:dataset}.${3:table}`
      ```
- Added supports new **DDL** syntax.
  - `ALTER COLUMN DROP NOT NULL`
    - Prefix  
      `alter column drop not null`
    - Body
      ```sql
      ALTER TABLE ${1:[IF EXISTS]} `${2:project}.${3:dataset}.${4:table}`
        ALTER COLUMN ${5:[IF EXISTS]} ${6:column_name} DROP NOT NULL
      ```
- Added supports **Federated query** syntax.
  - `EXTERNAL_QUERY`
    - Prefix  
      `external_query`
    - Body
      ```sql
      EXTERNAL_QUERY(${1:connection_id}, ${2:external_database_query}${3:[, options]})
      ```
    - Description
      ```
      Executes the query in Cloud SQL and returns results as a temporary table.
      ```
- Added supports new **Query** syntax.
  - `TABLESAMPLE`
    - Prefix  
      `"tablesample", "sampling"`
    - Body
      ```sql
      SELECT
        ${1:column}
      FROM `${2:project}.${3:dataset}.${4:table}`
        TABLESAMPLE SYSTEM (${5:value} PERCENT)
      ```
    - Description
      ```
      Table sampling lets you query random subsets of data from large BigQuery tables.
      ```
  - `FOR SYSTEM_TIME AS OF`
    - Prefix  
      `"system_time", "time travel"`
    - Body
      ```sql
      SELECT
        ${1:column}
      FROM `${2:project}.${3:dataset}.${4:table}`
        FOR SYSTEM_TIME AS OF TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL ${5:1} HOUR)
      ```
    - Description
      ```
      Time travel to access data at any point within the last 7 days.
      ```
  - `PIVOT`
    - Prefix  
      `pivot`
    - Body
      ```sql
      SELECT
        *
      FROM `${1:project}.${2:dataset}.${3:table}`
        PIVOT(
          ${4:aggregate_function(aggregate_column)}
          FOR ${5:input_column}
          IN (${6:pivot_column, ...})
        )
      ```
  - `UNPIVOT`
    - Prefix  
      `unpivot`
    - Body
      ```sql
      SELECT
        *
      FROM `${1:project}.${2:dataset}.${3:table}`
        UNPIVOT${4:[ INCLUDE NULLS|EXCLUDE NULLS ]}(
          ${5:value_column_name}
          FOR ${6:dimension_column_name}
          IN (${7:unpivot_column, ...})
        )
      ```
- Added supports new **String** functions.
  - `ASCII`
    - Prefix  
      `ascii`
    - Body
      ```sql
      ASCII(${1:value})
      ```
    - Description
      ```
      Returns the ASCII code for the first character or byte in value.
      ```
  - `CHR`
    - Prefix  
      `chr`
    - Body
      ```sql
      CHR(${1:value})
      ```
    - Description
      ```
      Takes a Unicode code point and returns the character that matches the code point.
      ```
  - `INITCAP`
    - Prefix  
      `initcap`
    - Body
      ```sql
      INITCAP(${1:value}${2:[, delimiters]})
      ```
    - Description
      ```
      Returns it with the first character in each word in uppercase and all other characters in lowercase.
      ```
  - `INSTR`
    - Prefix  
      `instr`
    - Body
      ```sql
      INSTR(${1:source_value}, ${2:search_value}${3:[, position[, occurrence]]})
      ```
    - Description
      ```
      Returns the lowest 1-based index of search_value in source_value.
      ```
  - `LEFT`
    - Prefix  
      `left`
    - Body
      ```sql
      LEFT(${1:value}, ${2:length})
      ```
    - Description
      ```
      Return the specified leftmost number of characters.
      ```
  - `OCTET_LENGTH`
    - Prefix  
      `octet_length`
    - Body
      ```sql
      OCTET_LENGTH(${1:value})
      ```
    - Description
      ```
      Alias for BYTE_LENGTH.
      ```
  - `REGEXP_INSTR`
    - Prefix  
      `regexp_instr`
    - Body
      ```sql
      REGEXP_INSTR(${1:source_value}, r\"${2:regex}\"${3:[, position[, occurrence, [occurrence_position]]]})
      ```
    - Description
      ```
      Returns the lowest 1-based index of a regular expression, regexp, in source_value.
      ```
  - `REGEXP_SUBSTR`
    - Prefix  
      `regexp_substr`
    - Body
      ```sql
      REGEXP_SUBSTR(${1:value}, r\"${2:regex}\"${3:[, position[, occurrence]]})
      ```
    - Description
      ```
      Synonym for REGEXP_EXTRACT.
      ```
  - `RIGHT`
    - Prefix  
      `right`
    - Body
      ```sql
      RIGHT(${1:value}, ${2:length})
      ```
    - Description
      ```
      Return the specified rightmost number of characters.
      ```
  - `SOUNDEX`
    - Prefix  
      `soundex`
    - Body
      ```sql
      SOUNDEX(${1:value})
      ```
    - Description
      ```
      Returns a STRING that represents the Soundex code for value.
      ```
  - `SUBSTRING`
    - Prefix  
      `substring`
    - Body
      ```sql
      SUBSTRING(${1:value}, ${2:position}${3:[, length]})",
      ```
    - Description
      ```
      Returns a substring of the supplied `value`. (Alias for SUBSTR)
      ```
  - `TRANSLATE`
    - Prefix  
      `translate`
    - Body
      ```sql
      TRANSLATE(${1:expression}, ${2:source_characters}, ${3:target_characters})
      ```
    - Description
      ```
      In `expression`, replaces each character in `source_characters` with the corresponding character in `target_characters`.
      ```
  - `UNICODE`
    - Prefix  
      `unicode`
    - Body
      ```sql
      UNICODE(${1:value})
      ```
    - Description
      ```
      Returns the Unicode code point for the first character in value.
      ```
- Added supports new **Date** functions.
  - `LAST_DAY`
    - Prefix  
      `last_day`
    - Body
      ```sql
      LAST_DAY(${1:date_expression}${2:[, date_part]})
      ```
    - Description
      ```
      description": "Returns the last day from a date expression.
      ```

### Changed
- Changed to **legacy** function.
  - `JSON_EXTRACT`
  - `JSON_EXTRACT_SCALAR`
  - `JSON_EXTRACT_ARRAY`
  - `JSON_EXTRACT_STRING_ARRAY`
- Added supports new **Scripting**.
  - `BEGIN ... END` added `EXCEPTION`
    - Prefix  
      `begin/end`
    - Body
      ```sql
      BEGIN
        ${1:statements}
      EXCEPTION WHEN ERROR THEN
        ${2:statements}
        ${3:[# Get error informations
        SELECT
          @@error.message,
          @@error.stack_trace,
          @@error.statement_text,
          @@error.formatted_stack_trace;]}
      END;
      ```
- Added supports new **DDL** syntax.
  - `CREATE VIEW`
    - Prefix  
      `create view`
    - Body
      ```sql
      CREATE ${1:[OR REPLACE] }VIEW ${2:[IF NOT EXISTS] }`${4:project}.${5:dataset}.${6:view}`
      ${7:[(
        column_name_list
      )]}
      ${8:[OPTIONS (
        description = "description",
        expiration_timestamp = TIMESTAMP "YYYY-MM-DD HH:MI:SS UTC",
        friendly_name = "friendly_name",
        labels = [("key", "value")]
      )]}
      AS
      SELECT
        ${9:column}
      FROM `${10:project}.${11:dataset}.${12:table}`
      ```
- Added supports new **Query** syntax.
  - `ORDER BY`
    - Prefix  
      `order by`
    - Body
      ```sql
      ORDER BY
        ${1:expression} ${2:[ASC|DESC]} ${3:[NULLS FIRST|NULLS LAST]}
      ```
- Added supports new **String** functions.
  - `REGEXP_EXTRACT`
    - Prefix  
      `regexp_extract`
    - Body
      ```sql
      REGEXP_EXTRACT(${1:value}, r\"${2:regex}\"${3:[, position[, occurrence]]})",
      ```
    - Description
      ```
      Returns the first substring in `value` that matches the regular expression, `regex`. Returns NULL if there is no match.
      ```

### Fixed
- Minor fixed.


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
- Minor fixed.


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
- Minor fixed.


## [1.1.0] - 2019-03-17
### Added
- Initial release


[1.9.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.8.0...v1.9.0
[1.8.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.7.0...v1.8.0
[1.7.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.6.1...v1.7.0
[1.6.1]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.6.0...v1.6.1
[1.6.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.5.0...v1.6.0
[1.5.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.4.0...v1.5.0
[1.4.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.3.0...v1.4.0
[1.3.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.2.0...v1.3.0
[1.2.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/releases/tag/v1.1.0

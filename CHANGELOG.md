# Change Log
All notable changes to the "sql-bigquery" extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


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


[1.4.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.3.0...v1.4.0
[1.3.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.2.0...v1.3.0
[1.2.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/releases/tag/v1.1.0

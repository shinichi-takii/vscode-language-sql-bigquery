# Change Log
All notable changes to the "sql-bigquery" extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


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

[1.2.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/shinichi-takii/vscode-language-sql-bigquery/releases/tag/v1.1.0

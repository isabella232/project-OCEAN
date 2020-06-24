<!-- Copyright 2020 Google LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License. -->

<!-- Example SQL to explore metadata for existing BigQuery repos using Libraries.io dataset.

	Also checkout this post: https://medium.com/google-cloud/bigquery-dataset-metadata-queries-8866fa947378
 -->


<!-- Get table schema -->

SELECT *
  FROM bigquery-public-data.libraries_io.INFORMATION_SCHEMA.TABLES


<!-- Combine queries for more detailed table schema info including lastest update date, number of rows and size -->

SELECT s.table_catalog, s.table_schema, s.table_name, s.table_type, s.is_insertable_into, s.is_typed, s.creation_time, t.last_modified_time, t.row_count, t.size_bytes, t.type
  FROM bigquery-public-data.libraries_io.INFORMATION_SCHEMA.TABLES s
  JOIN bigquery-public-data.libraries_io.__TABLES__ t 
  ON s.table_name = t.table_id 


<!-- Get column information for a table -->

SELECT *
  FROM bigquery-public-data.libraries_io.INFORMATION_SCHEMA.COLUMNS
  WHERE TABLE_NAME = "repositories"

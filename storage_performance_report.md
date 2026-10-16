# QuickFeed Storage & Performance Report

## Diagnosis

The legacy schema maintains five secondary indexes in addition to the primary key. Each INSERT must write the new row and maintain applicable indexes, increasing disk I/O, logging, and the possibility of B-tree page splits.

| Index | Decision | Reason |
|---|---|---|
| idx_user_id | Keep | Supports retrieving posts by user |
| idx_content | Drop | Prefix index on long text consumes storage; consider FULLTEXT for word search |
| idx_post_type | Drop | Low cardinality; may provide little filtering benefit |
| idx_is_visible | Drop | Boolean column with low selectivity |
| idx_created_at | Keep | Supports time-based retrieval |

## Storage comparison

Record actual measurements from information_schema.TABLES.

- Before: Data = [fill in] MB; Index = [fill in] MB
- After: Data = [fill in] MB; Index = [fill in] MB
- Index storage reduction = [calculate] MB

Removing three secondary indexes reduces index maintenance for INSERT, UPDATE, and DELETE operations. However, queries that relied on the removed indexes may become slower. Validate query plans with EXPLAIN and workload measurements.

The actual storage reduction depends on the table size, data distribution, and storage engine. No measurements should be invented.
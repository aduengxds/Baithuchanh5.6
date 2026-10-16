# AI Prompt Log — QuickFeed

## Prompt 1: Cardinality
Question: What is cardinality, and why can a Boolean index be ineffective?

Finding: Cardinality is the number of distinct values. Low-cardinality indexes often filter out few rows, so MySQL may prefer a table scan.

## Prompt 2: TEXT indexing
Question: What are the costs of indexing a long TEXT column?

Finding: A prefix index consumes storage and adds write overhead. FULLTEXT is worth considering for word-based searches.

## Prompt 3: InnoDB write performance
Question: What happens when inserting a row into a table with multiple indexes?

Finding: InnoDB writes the row and maintains applicable secondary indexes. This can cause extra page writes, logging, and page splits.

## Prompt 4: Storage measurement
Question: How can data and index sizes be compared in MB?

Finding: Query information_schema.TABLES and divide DATA_LENGTH and INDEX_LENGTH by 1024 * 1024.

## Prompt 5: Read/write trade-off
Question: Which indexes should remain on Posts?

Finding: Retain indexes that support frequent queries, such as retrieving posts by user and sorting by time. Validate decisions with EXPLAIN.
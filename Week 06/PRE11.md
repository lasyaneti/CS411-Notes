# PRE11: Storage and Indexing

## Simplified Computer Architecture 
- No instructions can be executed if the data is not in the process register or process cache (SUPER FAST 10 ns) but less memory (KB)
- Added main memory (SLOWER 10^2 ns) but more memory (GB)
- Database system runs under the OS system, data is stored in blocks

## Indexing 
- Computer-based catalog and librarian are components of index 
- Index speeds up selection of search key fields
- Search key = subset of fields of a relation
- Entries in an index (k: search key, r: record OR record ID or pointer to where search key exists)

## Terminology 
- Data file: has the data corresponding to a relation 
    - Has blocks, and every block a couple records 
- Index file: has an index 
    - Index block with search key and pointer to block of data file where key exists

![](/assets/pre11.jpg)
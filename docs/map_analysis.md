# Map Analysis Laboratory

## Core goal
Students must implement a dictionary-like `Map` structure that stores key-value pairs and supports lookup, insertion, deletion, and updates.

## Required operations
Students must implement the following behavior:

- insert a new key-value pair;
- reject duplicate keys;
- find whether a key exists;
- update an existing value;
- remove an existing key;
- retrieve a value by key;
- list keys and values;
- maintain sorted order if appropriate for the design.

## Analysis expectations
Students should discuss:

- average-case time complexity of insertion, lookup, and deletion;
- best-case and worst-case behavior;
- why duplicate-key handling matters;
- the difference between a search by key and scanning all entries;
- trade-offs between sorted vectors and hash-based maps;
- memory overhead and performance of `keys()` and `values()`.

## Big-O focus
Students should explain the Big-O of:

- `insert`
- `contains`
- `update`
- `erase`
- `at`
- `keys`
- `values`

The expected design is a clear, well-explained mapping abstraction that makes trade-offs explicit.

## Analysis:
The Map stores key-value pairs in a std::vector of KeyValuePair and keeps it sorted by key. insert first checks if the key already exists and rejects it if so, because duplicate keys would make lookups hard: at and update could not know which value to use. contains searches for the key, update changes the value of an existing key, erase removes the entry, and at returns the value or throws an error if the key is missing. keys() and values() list every entry in sorted order.

The lookup uses findIndex. It scans the vector one entry at a time. In the best case the key is the first entry, so contains, update, erase, and at is O(1) at the best case. In the worst cases they take O(n), because all entries will be checked. insert is O(n log n) because it searches for duplicates in O(n) and then re-sorts the vector. Inserting into a sorted vector could be done in O(n) by placing the new entry in the last position, instead of sorting everything again. keys() and values() are O(n) because they visit every entry.

Searching by key means looking for one specific entry, and scanning all entries means visiting every one of them. A sorted vector can use binary search to find a key in O(log n), which is much faster than a full scan. Compared with a hash-based map, a sorted vector keeps keys in order, is simple, and uses little memory, but insertion and deletion are slower because entries must shift. A hash map gives O(1) average time for insert, lookup, and deletion, but it does not keep keys in order and needs extra space to stay below a good load factor.

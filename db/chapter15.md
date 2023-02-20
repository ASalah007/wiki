# Chapter 15

## Measure of the query cost

- **seek time** (t): it is the time taken to find the required memory on desk.

- **transfere time** (tt): it is the time taken to transfere a block from desk to memory.

## Selections using file scans and indeices

1. **Linear Search** -> `ts+br*tt`: first seek the memory location with ts then transfer br blocks with tt time for each block

   1.1 **Linear Search with Equality on key** -> average case = `ts + (br/2) * tt` it is the same as linear search but i might find the record that I am looking for and then end the search.

2. **Clustering Index, equality on key** -> `(hi + 1) * (tt + ts)`, where hi is the hight of the index tree commonly the non leef nodes in the index tree are stored in the memory so hi = 1<br>
   if the records are stored in the leef nodes not just a pointer to it then the cost becomes `hi*(ts=tt)`
3. **clustering Index, equality on non-key** -> `hi*tt * (ts+b*tt)`

4. **Secondary index equality** -> same like case 2 unless multible values can be retrieved not only one -> `(hi+n) * (tt+ts)`

5. **clustering index, comparison** same as case 3

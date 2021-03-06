# Blitz
Blitz! — lightning fast primitive collections for Java

I work with sets of longs every day. SQLite primary keys and many other things are longs. So I've written these collections:
MutableLongTreeSet, ImmutableLongTreeSet, MutableLongHashSet.

This project is currently work in progress. I'll be glad to see your suggestions, so feel free to open feature requests;
API is quite experimental and is a subject to change.

## API

### MutableLongSet
(implementation: `MutableLongHashSet`)
```java
public interface PrimitiveSet<E> {
    int size();
    boolean isEmpty();
    String toString();
    boolean equals(Object other);
    int hashCode();
}
interface LongSet extends PrimitiveSet<Long> {
    boolean contains(long element);
    boolean containsAll(long[] elements);
    boolean containsAll(LongSet elements);
    boolean containsAny(long[] elements);
    boolean containsAny(LongSet elements);
    MutableLongSet copyToMutable();
    ImmutableLongSet asImmutable();
    long[] copyToArray();
    LongIterator iterator();
}
interface MutableLongTreeSet extends LongSet {
    boolean add(long element);
    boolean addAll(long[] elements);
    boolean addAll(LongSet elements);
    boolean remove(long element);
    boolean removeAll(long[] elements);
    boolean removeAll(LongSet elements);
    boolean retainAll(long[] elements);
    boolean retainAll(LongSet elements);
    @Override MutableLongIterator iterator();
    int addOrRemove(long element);
}
```

## Kotlin
This library contains operator overloads
and functional-style bulk operations for Kotlin.
```kt
// factories
mutableLongSetOf()
immutableLongSetOf()
LongArray.toImmutableLongSet()
LongArray.toMutableLongSet()

// contains() operator bindings
Long/LongArray/LongSet in LongSet

// bulk operations
LongSet.single[OrDefault]()
LongSet.filtered[Not]()
LongSet.filter[Not]To()
LongSet.forEach(), LongSet.onEach()
LongSet.mapToLongs()
LongSet.joinTo[String]()
LongSet.average(), LongSet.sum()

// operations with mutable sets
MutableLongSet += Long/LongArray/LongSet
MutableLongSet -= Long/LongArray/LongSet

// operations with immutable sets
ImmutableLongSet + Long/LongArray/LongSet: ImmutableLongSet
ImmutableLongSet - Long/LongArray/LongSet: ImmutableLongSet
```

## Performance

Insertions are <250 ns, searches are <50 ns.

![insertions](benchmarks/insertions.png)

![searches](benchmarks/searches.png)

Blitz! `MutableLongHashSet` is very compact:

![deep size](benchmarks/memory.png)

## Threading

`MutableLongHashSet`s are absolutely **not** thread-safe.

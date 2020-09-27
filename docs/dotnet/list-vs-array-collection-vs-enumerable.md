---
title: Lists vs Array vs Collections
# tags: [.net]
---

# Comparing enumerable, arrays, collections and lists

## Type Hierarchy

This is a simple hierarchy, from the most basic type to the richer ones 

- `IEnumerable` gives the ability to loop among items, forward only

- `ICollection` adds `Count`, `CopyTo`.

- `ICollection<>` adds `Add`, `Clear`, `Contains`, `Remove`.

- `IList` adds index access, `Insert`, `IndexOf`, `RemoveAt`.

- `List` adds `Find`, `Reverse`, `Sort`, `BinarySearch`, `RemoveAll`, `RemoveRange`, `AddRange`, `Insert`, `InsertRange`

## When to return what

### `List`, `IList`

You should return a list-based object when the caller is expected to scan/add/update/delete items.

If a property returns a list-based object, then all changes affect the state of the owner instance.

### `Array`
You should return an array when the caller is expected not to add/delete items, and to access
  them by index

If a property returns an Array instance, then all changes affect the state of the owner instance.

Array implements `ICollection`, but (obvously) not `ICollection<>`

### `IEnumerable`
You should return an `IEnumerable` when the caller is expected not to add/delete items, and to access its items
  one by one, in sequence.
  
If the user convert the instance to a list/array, a new instance of the proper type is 
  created, and items are copied into it, even if the instance exposed via `IEnumerable` was already
  a list/array/...


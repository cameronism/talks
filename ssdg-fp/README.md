Functional Programming
========================

Sonora Software Developers Group
---------------------------------


- mindset -- not necessarily language based
  + referential transparency (itempotent -ish)
  + higher order functions
  + purity
  + recursion
  
    


- javascript examples (maybe leave to separate meetup talk)
 

- immutability
- pattern matching
  + polymorphic types
    * case classes Scala
    * discriminated unions F#
- option types
- functional collections
  + complements immutability
- middle ground (playing nicely together)
  + trees of polymorphic objects
- destructuring
  + tuples


```csharp
public static void Increment(uint objectId, CountType type, Period period, DateTime previous, ushort? interactionId = null)
{
    lock (_Lock)
    {
        var count = Find(objectId, type, period, interactionId);
        count._Total++;
        if (previous == DateTime.MinValue)
        {
            count._Unique++;
            count._New++;
        }
        else if (!period.IsDay(previous))
        {
            count._Unique++;
        }
    }   
}

public static void Increment(uint objectId, CountType type, Period period, ushort previous, ushort? interactionId = null)
{
    lock (_Lock)
    {
        var count = Find(objectId, type, period, interactionId);
        count._Total++;
        if (previous == 0)
        {
            count._Unique++;
            count._New++;
        }
        else if (!period.IsDay(previous))
        {
            count._Unique++;
        }
    }
}
```

```fsharp
let tryParse func str = 
	let matched, value = func str
	match matched with
	| true -> Some(value)
	| false -> None



let matched, num = Int32.TryParse "123"

matched.Dump();
num.Dump();

(tryParse Int32.TryParse "123").Dump()

(tryParse Int32.TryParse "   ").Dump();

let parseInt = tryParse Int32.TryParse
let parseGuid = tryParse Guid.TryParse

(parseInt "234").Dump()
(parseGuid "asdf").Dump()

// show flatmap stuff
```

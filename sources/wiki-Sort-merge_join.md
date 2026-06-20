---
source: https://en.wikipedia.org/wiki/Sort-merge_join
fetched: 2026-06-19
---

Algorithm used in relational databases 

The **sort-merge join** (also known as merge join) is a [join algorithm](./Join_algorithm) and is used in the implementation of a [relational](./Relational_database) [database management system](./Database_management_system).

 

The basic problem of a join algorithm is to find, for each distinct value of the join attribute, the set of [tuples](./Tuple) in each relation which display that value. The key idea of the sort-merge algorithm is to first sort the relations by the join attribute, so that interleaved linear scans will encounter these sets at the same time.

 

In practice, the most expensive part of performing a sort-merge join is arranging for both inputs to the algorithm to be presented in sorted order. This can be achieved via an explicit sort operation (often an [external sort](./External_sort)), or by taking advantage of a pre-existing ordering in one or both of the join relations.[[1]](./Sort-merge_join#cite_note-1) The latter condition, called interesting order, can occur because an input to the join might be produced by an index scan of a tree-based index, another merge join, or some other plan operator that happens to produce output sorted on an appropriate key. Interesting orders need not be serendipitous: the optimizer may seek out this possibility and choose a plan that is suboptimal for a specific preceding operation if it yields an interesting order that one or more downstream nodes can exploit.

 

## Complexity

 

Let     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) and     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2)  be relations where      |  R  |  <  |  S  |    {\displaystyle |R|<|S|}  ![{\displaystyle |R|<|S|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ce4a1a7e91cfe12cda7be50302da1b4ce591dc0c).     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) fits in      P  r     {\displaystyle P_{r}}  ![{\displaystyle P_{r}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3e7f814e80c6ff1469112bd4b7430e358e86c7d6) pages memory and     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) fits in      P  s     {\displaystyle P_{s}}  ![{\displaystyle P_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fe65a99191556a55c0eea7cd971a5cb642ce7be2) pages memory. In the worst case, a **sort-merge join** will run in     O (  P  r   +  P  s   )   {\displaystyle O(P_{r}+P_{s})}  ![{\displaystyle O(P_{r}+P_{s})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f9cc39ec7d451cc35a37de6c0f35563af398a8bb) I/O operations. In the case that     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) and     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) are not ordered the worst case time cost will contain additional terms of sorting time:     O (  P  r   +  P  s   +  P  r   log ⁡ ⁡  (  P  r   ) +  P  s   log ⁡ ⁡  (  P  s   ) )   {\displaystyle O(P_{r}+P_{s}+P_{r}\log(P_{r})+P_{s}\log(P_{s}))}  ![{\displaystyle O(P_{r}+P_{s}+P_{r}\log(P_{r})+P_{s}\log(P_{s}))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/26def806b6b39f591919c26e38f041140667942a), which equals     O (  P  r   log ⁡ ⁡  (  P  r   ) +  P  s   log ⁡ ⁡  (  P  s   ) )   {\displaystyle O(P_{r}\log(P_{r})+P_{s}\log(P_{s}))}  ![{\displaystyle O(P_{r}\log(P_{r})+P_{s}\log(P_{s}))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e3c197d434c84471d72d73ff3a26e982366a919) (as [linearithmic](./Linearithmic_time) terms outweigh the linear terms, see [Big O notation – Orders of common functions](./Big_O_notation#Orders_of_common_functions)).

 

## Pseudocode

 

For simplicity, the algorithm is described in the case of an [inner join](./Join_(SQL)#Inner_join) of two relations *left* and *right*. Generalization to other join types is straightforward. The output of the algorithm will contain only rows contained in the *left* and *right* relation and duplicates form a [Cartesian product](./Cartesian_product).

 
```
function Sort-Merge Join(left: Relation, right: Relation, comparator: Comparator) {
    result = new Relation()
    
    // Ensure that at least one element is present
    if (!left.hasNext() || !right.hasNext()) {
        return result
    }
    
    // Sort left and right relation with comparator
    left.sort(comparator)
    right.sort(comparator)
    
    // Start Merge Join algorithm
    leftRow = left.next()
    rightRow = right.next()
    
    outerForeverLoop:
    while (true) {
        while (comparator.compare(leftRow, rightRow) != 0) {
            if (comparator.compare(leftRow, rightRow) < 0) {
                // Left row is less than right row
                if (left.hasNext()) {
                    // Advance to next left row
                    leftRow = left.next()
                } else {
                    break outerForeverLoop
                }
            } else {
                // Left row is greater than right row
                if (right.hasNext()) {
                    // Advance to next right row
                    rightRow  = right.next()
                } else {
                    break outerForeverLoop
                }
            }
        }
        
        // Mark position of left row and keep copy of current left row
        left.mark()
        markedLeftRow = leftRow
        
        while (true) {
            while (comparator.compare(leftRow, rightRow) == 0) {
                // Left row and right row are equal
                // Add rows to result
                result = add(leftRow, rightRow)
                
                // Advance to next left row
                leftRow = left.next()
                
                // Check if left row exists
                if (!leftRow) {
                    // Continue with inner forever loop
                    break
                }
            }
            
            if (right.hasNext()) {
                // Advance to next right row
                rightRow  = right.next()
            } else {
                break outerForeverLoop
            }
            
            if (comparator.compare(markedLeftRow, rightRow) == 0) {
                // Restore left to stored mark
                left.restoreMark()
                leftRow = markedLeftRow
            } else {
                // Check if left row exists
                if (!leftRow) {
                    break outerForeverLoop
                } else {
                    // Continue with outer forever loop
                    break
                }
            }
        }
    }
    
    return result
}

```
 

Since the comparison logic is not the central aspect of this algorithm, it is hidden behind a generic comparator and can also consist of several comparison criteria (e.g. multiple columns). The compare function should return if a row is *less(-1)*, *equal(0)* or *bigger(1)* than another row:

 
```
function compare(leftRow: RelationRow, rightRow: RelationRow): number {
	// Return -1 if leftRow is less than rightRow
	// Return 0 if leftRow is equal to rightRow
	// Return 1 if leftRow is greater than rightRow
}

```
 

Note that a relation in terms of this [pseudocode](./Pseudocode) supports some basic operations:

 
```
interface Relation {
    // Returns true if relation has a next row (otherwise false)
    hasNext(): boolean
    
    // Returns the next row of the relation (if any)
    next(): RelationRow
    
    // Sorts the relation with the given comparator
    sort(comparator: Comparator): void
    
    // Marks the current row index
    mark(): void
    
    // Restores the current row index to the marked row index
    restoreMark(): void
}

```
 

## Simple C# implementation

 

Note that this implementation assumes the join attributes are unique, i.e., there is no need to output multiple tuples for a given value of the key.

 
```
public class MergeJoin
{
    // Assume that left and right are already sorted
    public static Relation Merge(Relation left, Relation right)
    {
        Relation output = new Relation();
        while (!left.IsPastEnd && !right.IsPastEnd)
        {
            if (left.Key == right.Key)
            {
                output.Add(left.Key);
                left.Advance();
                right.Advance();
            }
            else if (left.Key < right.Key)
                left.Advance();
            else // if (left.Key > right.Key)
                right.Advance();
        }
        return output;
    }
}
 
public class Relation
{
    private const int ENDPOS = -1;
    private List<int> list;
    private int position = 0;

    public Relation()
    {
        this.list = new List<int>();
    }

    public Relation(List<int> list)
    {
        this.list = list;
    }

    public int Position => position;

    public int Key => list[position];

    public bool IsPastEnd => position == ENDPOS;

    public bool Advance()
    {
        if (position == list.Count - 1 || position == ENDPOS)
        {
            position = ENDPOS;
            return false;
        }
        position++;
        return true;
    }

    public void Add(int key)
    {
        list.Add(key);
    }

    public void Print()
    {
        foreach (int key in list)
            Console.WriteLine(key);
    }
}

```
 

## See also

 
- [Hash join](./Hash_join)
- [Nested loop join](./Nested_loop_join)

 

## References

  
1. [↑](./Sort-merge_join#cite_ref-1) ["Sort-Merge Joins"](https://www.dcs.ed.ac.uk/home/tz/phd/thesis/node20.htm). *www.dcs.ed.ac.uk*. Retrieved 2022-11-02.

 

## External links

 

[C# Implementations of Various Join Algorithms](http://www.necessaryandsufficient.net/2010/02/join-algorithms-illustrated/)
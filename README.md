darts
=====
This is a GO implementation of Double-ARray Trie System. It's a clone of the [C++ version](http://chasen.org/~taku/software/darts/) 

Darts can be used as simple hash dictionary. You can also do very fast Common Prefix Search which is essential for morphological analysis, such as word split for CJK text indexing/searching.

Reference
---------
[What is Trie](http://en.wikipedia.org/wiki/Trie)
[An Implementation of Double-Array Trie](http://linux.thai.net/~thep/datrie/datrie.html)

Usage
---------
#Input Dictionary Format
```sh
Key\tFreq
```
Each key occupies one line. The file should be utf-8 encoded

#Code example (unicode version)
```sh
package main
import(
    "darts"
    "fmt"
)

func main(){
    ok, d := darts.Import("darts.txt", "darts.lib")
    if ok {
	if d.ExactMatchSearch([]rune("考察队员",0) {
	    fmt.Println("考察队员 is in dictionary")
	}
    }
}
```
#Code example (byte version)
```sh
package main
import(
    "darts"
    "fmt"
)

func main(){
    ok, d := darts.Import("darts.txt", "darts.lib")
    if ok {
	key := []byte("考察队员")
	r := d.CommonPrefixSearch(key, 0) 
	for i := 0; i < len(r); i++ {
	    fmt.Println(string(key[:r[i].PrefixLen]))
	}
    }
}
```

Performance
-----------
Using a 100K item dictionary, a simple search on eath key takes go map 46 ms, takes byte\_key version of darts 14 ms, and for unicode\_key version of darts 9.5 ms.

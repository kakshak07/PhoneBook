# PhoneBook
Implement a phonebook using trie trees as a data structure in C language.

Tries were first described by René de la Briandais in 1959.The term trie was coined two years later by Edward Fredkin. Data structure used to implement phonebook in C language is trie trees. In computer science, a trie, also called digital tree and sometimes radix tree or prefix tree (as they can be searched by prefixes), is a kind of search tree—an ordered tree data structure that is used to store a dynamic set or associative array where the keys are usually strings. A Trie is a special data structure used to store strings that can be visualized like a graph. It consists of nodes and edges. Each node consists of at max 26 children and edges connect each parent node to its children. These 26 pointers are nothing but pointers for each of the 26 letters of the English alphabet A separate edge is maintained for every edge.

## Justification for the choice of trie trees

A trie has a number of advantages over binary search trees and other data structure. A trie can also be used to replace a hash table. Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. Values are not necessarily associated with every node. Rather, values tend only to be associated with leaves, and with some inner nodes that correspond to keys of interest. A trie tree provide an alphabetical ordering of each character of string by key. Moreover, there are no collisions of different keys in a trie tree. There is no need to provide a hash function or to change hash functions as more keys are added to a trie.

## Time Compplexity

Trie is an efficient information retrieval data structure. Using Trie, search complexities can be brought to optimal limit (key length). If we store keys
in binary search tree, a well-balanced BST will need time proportional to M * log N, where M is maximum string length and N is number of keys in tree. Using Trie, we can search the key in O(M) time. However, the penalty is on Trie storage requirements. Searching up data in a trie is faster in the worst case, O(m) time (where m is the length of a search string), compared to an imperfect hash table. An imperfect hash table can have key collisions. A key collision is the hash function mapping of different keys to the same position in a hash table. The worst-case lookup speed in an imperfect hash table is O(N) time, but far more typically is O(1), with O(m) time spent evaluating the hash.

## List of functions
Insert-: Inserting a key into Trie can be done by defining a structure with one of the member as array of pointers. Every character of input key is inserted as an individual Trie node. It is important to note that the children are an array of pointers (or references) to next level trie nodes. The key character acts as an index into the array children. If the input key is new or an extension of existing key, we need to construct non-existing nodes of the key, and mark end of word for last node. If the input key is prefix of existing key in Trie, we simply mark the last node of key as end of word. To determine the end of word a structure member is_end_of_word is defined of data type integer which will be marked as one when all the character of the input string are inserted in the trie trees. The key length determines Trie depth.
Let's say we want to insert a key-value pair ("abc") into the trie-:
1. We go to root node.
2. Get the index of the first character ('a') of "abc". That would be 0 in our alphabet system.
3. Go to 0th child of root. Because 0th child is null we first construct a TrieNode to which this 0th child would point. This
newly constructed node would be node 'a'. We mark this node as current node.
4. Now we get the index of the second character of "abc". That would be 1 and therefore we go to 1st child of current node (from step#3).
5. Here again, 1st child is null. We create a new TrieNode which would be node 'b'. We mark this node as current node.
6. Now we get the index of the third character of "abc". That would be 2 and therefore we go to 2nd child current node (from step#5).
7. Here again, 2nd child is null. We create a new TrieNode which would be node 'c'. We mark this node as current node.
8. At this step, we are done reading all the characters of the given key. Hence, we mark the current node that is node 'c' as leaf node and store value 1 at this leaf node.


Search-: Searching for a key is similar to insert operation, however we only compare the characters and move down. The search can terminate due to end of string or lack of key in trie. In the former case, if the is_end_of_word field of last node is one, then the key exists in trie. In the second case, the search terminates without examining all the characters of key, since the key is not present in trie.
Search algorithm steps
Example: Searching for non-existing key "ac".
1. Go to root node.
2. Pick the first character of key "ac" which would be 'a'. Find out its index using alphabet system in use.
3. Index returned would be 0, go to 0th child of root which is node 'a'. Mark this node as current node.
4. Pick the second character of key "ac" which would be 'c'. Its index would be 2 and therefore we go to 2nd child of current node.
5. Now at this point, we find out that 2nd child of current node is null. If you notice, from insertion algorithm of a given key, no node in the key-path from the root could be null. If it is null then that implies that this key was never inserted in the trie. And therefore, in such cases, we return Not present in phonebook.
Example: searching for an existing key "abb"
The steps are very similar to previous example. We keep on reading characters of given key and according to indices of characters, travel from root node to node 'b' which is at level-3 (if root is at level-0). At this point we would have read all the characters of the key "abb" and hence we return the value stored at this node.

# Implement Trie (Prefix Tree)

# Problem Statement
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

1. `Trie()` Initializes the trie object.
2. `void insert(String word)` Inserts the string `word` into the trie.
3. `boolean search(String word)` Returns `true` if the string word is in the trie (i.e., was inserted before), and `false` otherwise.
4. `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string word that has the prefix prefix, and `false` otherwise.
### Example
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

## Approach
Each TrieNode contains, a dictionary of characters that point to the next TrieNodes and a boolean flag to indicate if this node is end of a word.
### Time Complexity
- For insertion **O(N)**:Where N is the length of the word.
- For search **O(N)** 
- For StartWith **O(N)**
### Space Complexity
- For insertion **O(N*K)**: where k is the number of words.
- For search **O(1)** 
- For StartWith **O(1)**
## Solution Code
```C#
public class Trie {
    private class TrieNode{
        public Dictionary<char, TrieNode> children; 
        public bool isEnd;

        public TrieNode(){
            children = new Dictionary<char, TrieNode>();
            isEnd = false;
        }
    }

    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    public void Insert(string word) {
        TrieNode node = root;
        foreach(char c in word){
            if(!node.children.ContainsKey(c)){
                node.children[c] = new TrieNode();
            }
            node = node.children[c];
        }
        node.isEnd = true;  
        
    }
    
    public bool Search(string word) {
        TrieNode node = root;
        foreach(char c in word){
            if(!node.children.ContainsKey(c)){
                return false;
            }
            node = node.children[c];
        }
        return node.isEnd;
    }
    
    public bool StartsWith(string prefix) {
        TrieNode node = root;
        foreach(char c in prefix){
            if(!node.children.ContainsKey(c)){
                return false;
            }
            node = node.children[c];
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.Insert(word);
 * bool param_2 = obj.Search(word);
 * bool param_3 = obj.StartsWith(prefix);
 */
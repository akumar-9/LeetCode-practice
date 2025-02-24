# Design Add and Search Words Data Structure

# Problem Statement
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

- `WordDictionary()` Initializes the object.
- `void addWord(word)` Adds `word` to the data structure, it can be matched later.
- `bool search(word)` Returns `true` if there is any string in the data structure that matches word or fa`lse otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

### Example
Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]


## Approach
I use trie data structure. Words can be inserted using the regual insert operation. Search is the tricky part because of the dot (.). For search, start at the root and traverse character by character, if regular character is found, move to child nodes. If . is encountered, try all possible child recursively, if any path succeeds, return true. If we reach the end of the word, check if the node is marked as the end. 
### Time Complexity
- For insertion **O(N)**:Where N is the length of the word.
- For search withoud . **O(N)** 
- For search with . **O(26^N)**
### Space Complexity
- For insertion **O(N*K)**: where k is the number of words.
- For search without .**O(1)** 
- For search with . **O(N)** recursive stack
## Solution Code
```C#
public class WordDictionary {

    private TrieNode root;

    private class TrieNode{
        public Dictionary<char, TrieNode> children;
        public bool isEnd;

        public TrieNode(){
            children =  new Dictionary<char,TrieNode>();
        } 
    }

    public WordDictionary() {
        root  = new TrieNode();
    }
    
    public void AddWord(string word) {
        TrieNode cur = root;
        foreach(char c in word){
            if(!cur.children.ContainsKey(c)){
                cur.children.Add(c, new TrieNode());
            }
            cur = cur.children[c];
        }
        cur.isEnd = true;
    }
    
    public bool Search(string word) {
        return DFS(0, word, root);
    }

    private bool DFS(int index, string word, TrieNode root){
        if(index == word.Length) return root.isEnd;
        char c = word[index];

        if(c == '.'){
            foreach(TrieNode child in root.children.Values){
                if(DFS(index+1, word, child)) return true;
            }
        }
        else{
            if(root.children.ContainsKey(c)){
                return DFS(index+1, word, root.children[c]);
            }
        }
        return false;
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.AddWord(word);
 * bool param_2 = obj.Search(word);
 */
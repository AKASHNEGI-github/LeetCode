# Trie

---
| Easy | Medium | Hard |
| ---- | ------ | ---- |
| Easy | Implement Trie (Prefix Tree) | Hard |
---

### Medium

- Implement Trie (Prefix Tree)
```c++
class TrieNode {
public:
    bool isEndOfWord;
    TrieNode* children[26];

    TrieNode() 
    {
        isEndOfWord = false;
        for (int i=0; i<26; i++) 
        {
            children[i] = NULL;
        }
    }
};

class Trie {
private:
    TrieNode* root;

public:
    Trie() 
    {
        root = new TrieNode();
    }
    
    void insert(string word) 
    {
        TrieNode* current = root;
        for(int i=0; i<word.length(); i++) 
        {
            int index = word[i] - 'a';
            if(current->children[index] == NULL) 
            {
                TrieNode* newTrieNode = new TrieNode();
                current->children[index] = newTrieNode;
            }
            current = current->children[index];
        }
        current->isEndOfWord = true;
    }
    
    bool search(string word) 
    {
        TrieNode* current = root;
        for(int i=0; i<word.length(); i++) 
        {
            int index = word[i] - 'a';
            if(current->children[index] == NULL) 
            {
                return false;
            }
            current = current->children[index];
        }
        return current->isEndOfWord;
    }
    
    bool startsWith(string prefix) 
    {
        TrieNode* current = root;
        for(int i=0; i<prefix.length(); i++) 
        {
            int index = prefix[i] - 'a';
            if(current->children[index] == NULL) 
            {
                return false;
            }
            current = current->children[index];
        }
        return true;
    }
};
```

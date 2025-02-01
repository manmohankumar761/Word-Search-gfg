# Word-Search-gfg
You are given a two-dimensional mat[][] of size n*m containing English alphabets and a string word. Check if the word exists on the mat. The word can be constructed by using letters from adjacent cells, either horizontally or vertically. The same cell cannot be used more than once.

Examples :

Input: mat[][] = [['T', 'E', 'E'], ['S', 'G', 'K'], ['T', 'E', 'L']], word = "GEEK"
Output: true
Explanation:

The letter cells which are used to construct the "GEEK" are colored.
Input: mat[][] = [['T', 'E', 'U'], ['S', 'G', 'K'], ['T', 'E', 'L']], word = "GEEK"
Output: false
Explanation:

It is impossible to construct the string word from the mat using each cell only once.
Input: mat[][] = [['A', 'B', 'A'], ['B', 'A', 'B']], word = "AB"
Output: true
Explanation:

There are multiple ways to construct the word "AB".
# code
#include <vector>
#include <string>

class Solution {
public:
    static bool isWordExist(std::vector<std::vector<char>>& mat, std::string word) {
        int n = mat.size();
        int m = mat[0].size();
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (mat[i][j] == word[0]) {
                    if (search(mat, word, i, j, n, m, 0)) {
                        return true;
                    }
                }
            }
        }
        
        return false;
    }
    
private:
    static bool search(std::vector<std::vector<char>>& mat, std::string& word, int i, int j, int n, int m, int index) {
        if (index == word.length()) return true;
        
        if (i < 0 || i >= n || j < 0 || j >= m || mat[i][j] != word[index]) return false;
        
        char temp = mat[i][j];
        mat[i][j] = '#';
        
        int directions[4][2] = {{1, 0}, {0, 1}, {-1, 0}, {0, -1}};
        
        for (auto& direction : directions) {
            if (search(mat, word, i + direction[0], j + direction[1], n, m, index + 1)) {
                return true;
            }
        }
        
        mat[i][j] = temp;
        
        return false;
    }
};

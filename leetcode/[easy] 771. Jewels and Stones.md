# Jewels and Stones
[Link](https://leetcode.com/problems/jewels-and-stones/)

# Description
You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  
Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.  

The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive,   
so "a" is considered a different type of stone from "A".

# Example 1:

    Input: J = "aA", S = "aAAbbbb"
    Output: 3

# Example 2:

    Input: J = "z", S = "ZZ"
    Output: 0

# Note

S and J will consist of letters and have length at most 50.  
The characters in J are distinct.

# Bad Solution
    class Solution {
        public int numJewelsInStones(String J, String S) {
            int count = 0;
            for (char j : J.toCharArray()) {
                for (char s : S.toCharArray()) {
                    if (j == s) {
                        count++;
                    }

                }
            }
            return count;
        }
    }
    
# Solution

        class Solution {
            public int numJewelsInStones(String J, String S) {
                int count = 0;
                Set<Character> set = new HashSet();
                char[] j = J.toCharArray();
                char[] s = S.toCharArray();        
                for (char c : j) set.add(c);
                for (char c : s) count += set.contains(c) ? 1 : 0;        
                return count;
            }
        }
[Reference Link](https://leetcode.com/problems/jewels-and-stones/discuss/312591/Set-Java-solution-10-lines)
# Best Solution
        class Solution {
            public int numJewelsInStones(String J, String S) {
                boolean[] isSet = new boolean[52];
                for (char c : J.toCharArray()) {
                    isSet[getIdx(c)] = true;
                }

                int count = 0;
                for (char c : S.toCharArray()) {
                    count += isSet[getIdx(c)] ? 1 : 0;    
                }

                return count;
            }

            private int getIdx(char c) {
                if (Character.isUpperCase(c)) {
                    return 26 + c - 'A';
                }

                return c - 'a';
            }
        }
[Reference Link](https://leetcode.com/problems/jewels-and-stones/discuss/315425/Simple-Java-solution-using-Boolean-array)

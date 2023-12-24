Given a string s, reverse only all the vowels in the string and return it.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both lower and upper cases, more than once.

 

Example 1:

Input: s = "hello"
Output: "holle"

Example 2:

Input: s = "leetcode"
Output: "leotcede"

 

Constraints:

    1 <= s.length <= 3 * 105
    s consist of printable ASCII characters.


---
my solution
```csharp
public class Solution {
    public string ReverseVowels(string s) {
        var vowels= new char[]{'a','e','i','o','u'};
        var output=s.ToArray();
        for(int front=0, back = s.Length-1 ; front<back;front++,back--)
        {
            char vowelInFront = ' ';
            for(;front<=back;front++)
            {
                if(vowels.Contains(char.ToLower(s[front])))
                {
                    vowelInFront=s[front];
                    break;
                }
            }
            char vowelInBack = ' ';
            for(;back>=front;back--)
            {
                if(vowels.Contains(char.ToLower(s[back])))
                {
                    vowelInBack=s[back];
                    break;
                }
            }
            if(vowelInFront!=' '&&vowelInBack!=' ')
            {
                output[back]=vowelInFront;
                output[front]=vowelInBack;
            }
        }
        return new string(output);
    }
}
```
---
better solution
```csharp
public class Solution {
    public string ReverseVowels(string s) {
        char[] sChar = s.ToCharArray();

        int start = 0;
        int end = s.Length - 1;
        bool[] vowels = new bool[128];

        vowels[(int)'a'] = true;
        vowels[(int)'e'] = true;
        vowels[(int)'i'] = true;
        vowels[(int)'o'] = true;
        vowels[(int)'u'] = true;
        vowels[(int)'A'] = true;
        vowels[(int)'E'] = true;
        vowels[(int)'I'] = true;
        vowels[(int)'O'] = true;
        vowels[(int)'U'] = true;


        while (end >= start)
        {
            bool isStartVowel = vowels[(int)s[start]] == true;
            bool isEndVowel = vowels[(int)s[end]] == true;

            if (isStartVowel && isEndVowel)
            {
                char temp = sChar[start];
                sChar[start] = sChar[end];
                sChar[end] = temp;
                start++;
                end--;
            }
            else
            {
                if (!isStartVowel)
                {
                    start++;
                }

                if (!isEndVowel)
                {
                    end--;
                }
            }
        }

        return new String(sChar);
    }
}

```

---
layout: post
title:  "Talk about KMP"
date:   2016-07-29 +0800
categories: algorithm
---

#KMP

Recently I counted many problem to handle the certain string in a document or a large sequence. All the idea is to use brut force way to find the match string. I was told that there is great way to handle large input called KMP.

I do some search it is O(mn) in the worst case but it runs at average O(m + n). When the input source length m is large enough we can say that the algorithm is O(n).

The idea is there are two phase the first phase is to do some preprocessing over the pattern pat[] and constructs an auxiliary array lps[] of size m (same as size of pattern). Here name lps indicates longest proper prefix which is also suffix

Examples:
For the pattern “AABAACAABAA”, lps[] is [0, 1, 0, 1, 2, 0, 1, 2, 3, 4, 5]
For the pattern “ABCDE”, lps[] is [0, 0, 0, 0, 0]

This can be a little hard to understand you can watch a [video][video]

Pase 2 is Searching :
Unlike the Naive algo where we slide the pattern by one, we use a value from lps[] to decide the next sliding position. Let us see how we do that. When we compare pat[j] with txt[i] and see a mismatch, we know that characters pat[0..j-1] match with txt[i-j+1…i-1], and we also know that lps[j-1] characters of pat[0…j-1] are both proper prefix and suffix which means we do not need to match these lps[j-1] characters with txt[i-j…i-1] because we know that these characters will anyway match. See KMPSearch() in the below code for details.

 Talk is cheap:
{% highlight java %}
public int strStr(String source, String target) {
        
        int slen = source.length();
        int tlen = target.length();
        int j = 0;
        int[] lps = new int[tlen];
        char[] pat = target.toCharArray();
        computeLPSArray(pat, tlen, lps);
        int i = 0; // index of source
        while (i < slen) {
            if (pat[j] == source.charAt(i)) {
                i++;
                j++;
            }
            if (j == tlen) {
                return i - j;
            } else if (i < slen && pat[j] != source.charAt(i)) {
                if (j != 0)
                j = lps[j - 1];
                else 
                i = i + 1;
            }
        }
        return -1;
    }
    public void computeLPSArray(char[] pat, int tlen, int[] lps) {
        int len = 0; // length of previous longest prefix suffix
        int i;
        
        lps[0] = 0; // always 0
        i = 1;
        while (i < tlen) {
            if (pat[i] == pat[len]) {
                len++;
                lps[i] = len;
                i++;
                
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }
{% endhighlight %}


[video]: https://www.youtube.com/watch?v=5i7oKodCRJo
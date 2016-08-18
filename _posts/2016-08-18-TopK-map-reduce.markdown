---
layout: post
title:  "Top k item map reduce"
date:   2016-08-18 +0800
categories: algorithm
---

# Top k item

This problem is a popular interview question because it has many use cases in our life. We need to get the top k most popular items to help the user get what they want. I can help app store or shopping website like amazon to make good decision. Top k can simply implement by priority queue in java it will take O(n) space and O(nlgN) time to get the result. There is also a quick sort solution but they all fit for single machine and not large data set. When we encount large data set partition is a great way we need to first hash the in put get similar word to the same machine and then start the algorithm that fit for single machine. 

To improve we can use cache to save some data from client and use database to persistent and treeset to get top k element. The hashmap used to process some request for the change and when the changes are big enough it will flush to disk in this case we use database. There is a tread off since we will sacrifice some kind of real time to make the system faster.

Now I want to show the map reduce version to solve this problem


 Talk is cheap:
{% highlight java %}
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 * Definition of Document:
 * class Document {
 *     public int id;
 *     public String content;
 * }
 */
public class TopKFrequentWords {
    static class Pair {
        String key;
        int value;
        Pair(String key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    public static class Map {
        public void map(String _, Document value,
                        OutputCollector<String, Integer> output) {
           
            int id = value.id;
            StringBuffer sb = new StringBuffer("");
            String content = value.content;
            String[] words = content.split("\\s");
            for (String word : words) {
                if (word.length() > 0) {
                    output.collect(word, 1);
                }
            }
        }
    }

    public static class Reduce {
        private PriorityQueue<Pair> Q = null;
        private int k;
        private Comparator<Pair> pairComparator = new Comparator<Pair> (){
            public int compare(Pair left, Pair right) {
                if (left.value != right.value) {
                    return left.value - right.value;
                }
                return right.key.compareTo(left.key);
            }
        };
        public void setup(int k) {
            this.k = k;
            Q = new PriorityQueue<Pair>(k, pairComparator);
        }   

        public void reduce(String key, Iterator<Integer> values) {
            int sum = 0;
            while (values.hasNext()) {
                sum += values.next();
            }
            Pair pair = new Pair(key, sum);
            if (Q.size() < k) {
                Q.add(pair);
            } else {
                Pair peak = Q.peek();
                if (pairComparator.compare(pair, peak) > 0) {
                    Q.poll();
                    Q.offer(pair);
                }
            }
        }

        public void cleanup(OutputCollector<String, Integer> output) {
            List<Pair> pairs = new ArrayList<>();
            while (!Q.isEmpty()) {
                pairs.add(Q.poll());
            }
            int n = pairs.size();
            for (int i = n - 1; i>= 0; i--) {
                Pair pair = pairs.get(i);
                output.collect(pair.key, pair.value);
            }
        }
    }
}
{% endhighlight %}


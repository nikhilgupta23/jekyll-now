---
layout: post
title: Lexicographic Integer ArrayList Comparision
---
__Given a set of distinct integers, S, return all possible subsets.__

This question had a pretty straight forward solution. The number of subsets will always be __2<sup>n</sup>__ where n is the number of elements in the set S.
Starting from 0 and going upto 2<sup>n</sup>, the binary representation of the numbers dictated whether the element at the corresponding index of the original set is to be included in the subset currently being formed or not.

_0 to neglect_
_1 to include_

The biggest problem was this part of the question.

>Elements in a subset must be in non-descending order.
>The solution set must not contain duplicate subsets.
>Also, the subsets should be sorted in ascending ( lexicographic ) order.
>The list is not necessarily sorted.

Here is how I dealt with the problem-
1. Sort the input List before performing any operations.
2. After getting the output list of lists, using the above method, I had to pass a Comparator object with a method to compare two ArrayLists in a lexicographic manner.

``` Java
 Collections.sort(ans,new Comparator<ArrayList<Integer>> () {
      @Override
      public int compare(ArrayList<Integer> a, ArrayList<Integer> b) {
        int ai=0,bi=0;
        while(ai!=a.size() && bi!=b.size())
        {
            if(a.get(ai)!=b.get(bi))
                return a.get(ai)>b.get(bi)?1:a.get(ai)==b.get(bi)?0:-1;
            ai++;bi++;
        }
      }});
```
I think that this is an inefficient way of solving it. I will post a better solution if I find it.

The complete solution-

``` Java
public class Solution 
{
	public ArrayList<ArrayList<Integer>> subsets(ArrayList<Integer> a)
	{
	    Collections.sort(a);
	    ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
	    for(int x=0;x<Math.pow(2,a.size());x++)
	    {
	        ArrayList<Integer> toadd = new ArrayList<Integer>();
	        int count=0;
	        int r=x;
	        while(r!=0)
	        {
	            int bit=r & 1;
	            r=r>>1;
	            if(bit==1)
	                toadd.add(a.get(count));
	            count++;
	        }
	        ans.add(toadd);
	    }
	    Collections.sort(ans,new Comparator<ArrayList<Integer>> () 
	    {
	        @Override
	        public int compare(ArrayList<Integer> a, ArrayList<Integer> b) 
	        {
	          int ai=0,bi=0;
	          while(ai!=a.size() && bi!=b.size())
	          {
	              if(a.get(ai)!=b.get(bi))
	                  return a.get(ai)>b.get(bi)?1:a.get(ai)==b.get(bi)?0:-1;
	              ai++;bi++;
	          }
	          return a.size()<=b.size()?-1:1;
	        }
	   });
	   return ans;
	}	
}
```
---
__Update__

Another code snippet I found online doing the same thing. It's just more elegant.
``` Java
    Collections.sort(res, new Comparator<ArrayList<Integer>>() 
    {
        @Override
        public int compare(ArrayList<Integer> a, ArrayList<Integer> b) 
        {
            int an = a.size();
            int bn = b.size();
            for (int i = 0; i < Math.min(an, bn); i++) {
                int cmp = Integer.compare(a.get(i), b.get(i));
                if (cmp != 0)
                    return cmp;
            }
            return Integer.compare(a.size(), b.size());
        }
    });
```

# BFS-1
# Problem 1
Binary Tree Level Order Traversal (https://leetcode.com/problems/binary-tree-level-order-traversal/)

T.C=O(n)
S.C=O(h)
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ll=new ArrayList<>();
        deep(root,ll,0);
        return ll;
    }
    public static void deep(TreeNode root, List<List<Integer>> ll, int lev){
        List<Integer> l=new ArrayList<>();
        if(root==null)
            return;
        if(ll.size()==lev)
            ll.add(new ArrayList<>());
        ll.get(lev).add(root.val);
        deep(root.left,ll,lev+1);
        deep(root.right,ll,lev+1);
    }
}

# Problem 2
Course Schedule (https://leetcode.com/problems/course-schedule/)
T.C=O(n)
S.C=O(n)

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        HashMap<Integer,List<Integer>> map=new HashMap<>();
        int[] s=new int[numCourses];
        for(int[] prereq:prerequisites){
            int inward=prereq[0];
            int outward=prereq[1];
            s[inward]++;
            if(!map.containsKey(outward)){
                map.put(outward,new ArrayList<Integer>());
            }
            map.get(outward).add(inward);
        }
        Queue<Integer> qq=new LinkedList<>();
        int cnt=0;
        for(int i=0;i<numCourses;i++)
        {
            if(s[i]==0){
                qq.add(i);
                cnt++;
            }
        }
        if(cnt==numCourses)
            return true;
        if(cnt==0)
            return false;
        while(!qq.isEmpty()){
            int cur=qq.poll();
            List<Integer> ch=map.get(cur);
            if(ch!=null){
                for(int chi:ch){
                s[chi]--;
                if(s[chi]==0){
                    qq.add(chi);
                    cnt++;
                    if(cnt==numCourses)
                        return true;
                }
            }
            }
        }
        if(cnt==numCourses)
            return true;
        return false;
    }
}



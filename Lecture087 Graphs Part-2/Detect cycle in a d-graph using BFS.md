# Detect a Cycle in Directed Graph | Topological Sort | Kahn's Algorithm | BFS

## Article Link: https://takeuforward.org/data-structure/detect-a-cycle-in-directed-graph-topological-sort-kahns-algorithm-g-23/

## Using BFS
### Time Complexity:  O(V+E)
### Space Complexity: O(V)
```cpp
class Solution {
  private:
    void bfs(vector<int> adj[],vector<int>&inComingEgde,int node,vector<int>&topoSort){
       queue<int> q;
       // push all node with inComingEgde == 0 to queue
       for(int i=0;i<inComingEgde.size();i++){
           if(inComingEgde[i] == 0){
               q.push(i);
           } 
       }
       
       while(!q.empty()){
           // pop the front of queue
           auto front = q.front();
           q.pop();
           // add it to topo sort
           topoSort.push_back(front);
           // for each of its neighbour
           for(auto ne:adj[front]){
               // reduce their inComingEgde
               inComingEgde[ne]--;
               // if inComingEgde == 0 add to queue
               if(inComingEgde[ne] == 0){
                   q.push(ne);
               }
           }
           
       }
    }
  public:
    // Function to detect cycle in a directed graph.
    bool isCyclic(int V, vector<int> adj[]) {
        vector<int> inComingEgde(V,0);
	    vector<int> topoSort;
	    for(int i=0;i<V;i++){
	        for(auto ne:adj[i]){
	            inComingEgde[ne]++;
	        }
	    }
	    
        bfs(adj,inComingEgde,0,topoSort);
        // if topo sort size is not equal to V then there is a cycle in graph
        return !(topoSort.size()==V);
    }
};
```

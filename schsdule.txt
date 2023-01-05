class Solution {
public:
    bool check(int i,vector<bool>& v1,vector<bool>& v2,vector<vector<int>>& adj) {
        v1[i]=true;
        v2[i]=true;
        for (auto j:adj[i]) {
            if (v1[j]&&v2[j]) return true;
            if (!v1[j]) {
                if (check(j,v1,v2,adj)) return true;
            }
        }
        v2[i]=false;
        return false;
    }
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);
        for (auto i:prerequisites) {
            adj[i[0]].push_back(i[1]);
        }
        vector<bool> vis(numCourses,false);
        vector<bool> dfs_vis(numCourses,false);
        for (int i=0;i<numCourses;i++) {
            if (!vis[i]) {
                if (check(i,vis,dfs_vis,adj)) return false;
            }
        }
        return true;
    }
};
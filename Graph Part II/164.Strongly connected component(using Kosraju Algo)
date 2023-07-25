class Solution {
    public List<String> maxNumOfSubstrings(String S) {
	    // some nasty pre-compute in order to build the graph in O(N) time
        int[] mins = new int[26]; 
        int[] maxs = new int[26]; 
        Arrays.fill(mins, Integer.MAX_VALUE);
        Arrays.fill(maxs, -1); 
        boolean[] exists = new boolean[26]; 
        int[][] prefixSum = new int[S.length() + 1][26]; 
        for (int i = 0; i < S.length(); i ++) {
            System.arraycopy(prefixSum[i], 0, prefixSum[i + 1], 0, 26); 
            prefixSum[i + 1][S.charAt(i) - 'a'] += 1; 
            mins[S.charAt(i) - 'a'] = Math.min(mins[S.charAt(i) - 'a'], i); 
            maxs[S.charAt(i) - 'a'] = Math.max(maxs[S.charAt(i) - 'a'], i); 
            exists[S.charAt(i) - 'a'] = true; 
        }
        // build graph, using adjacency matrix
        boolean[][] graph = new boolean[26][26];
        for (int i = 0; i < 26; i ++) {
            if (exists[i]) {
                for (int j = 0; j < 26; j ++) {
                    if (prefixSum[maxs[i] + 1][j] - prefixSum[mins[i]][j] > 0) {
                        graph[i][j] = true; 
                    }
                }
            }
        }
    
        // kosaraju algorithm to find scc
        Stack stack = new Stack(); 
        boolean[] visited = new boolean[26]; 
        for (int i = 0; i < 26; i ++) {
            if (exists[i] && !visited[i]) {
                dfs(i, graph, stack, visited);
            }
        }
        int batch = 0; // 'id' of each SCC
        int[] batches = new int[26]; 
        int[] degree = new int[26];  // out-degree of each SCC
        Arrays.fill(batches, -1); 
        while (!stack.isEmpty()) {
            int v = stack.pop(); 
            if (batches[v] < 0) {
                dfs(v, graph, batches, batch, degree);
                batch ++; 
            }
        }
        
        List<String> res = new ArrayList<>(); 
        for (int i = batch - 1; i >= 0; i--) {
            if (degree[i] == 0) {
                int min = Integer.MAX_VALUE, max = -1; 
                for (int j = 0; j < 26; j ++) {
                    if (batches[j] == i) {
                        min = Math.min(mins[j], min); 
                        max = Math.max(maxs[j], max); 
                    }
                }
                res.add(S.substring(min, max + 1));
            }
        }
        
        return res; 
    }
    
    private void dfs(int v, boolean[][] graph, Stack stack, boolean[] visited) {
        if (!visited[v]) {
            visited[v] = true; 
            for (int i = 0; i < 26; i ++) {
                if (graph[v][i] && !visited[i]) {
                    dfs(i, graph, stack, visited);
                }
            }
            stack.push(v);
        }
    }
    
    private void dfs(int v, boolean[][] graph, int[] batches, int batch, int[] degree) {
        if (batches[v] < 0) {
            batches[v] = batch; 
            for (int i = 0; i < 26; i ++) {
                if (graph[i][v]) {
                    dfs(i, graph, batches, batch, degree); 
                }  
            }
        } else {
            if (batches[v] != batch) {
                degree[batches[v]] += 1;
            }
        }
    }
    
    private static final class Stack {
        int[] values = new int[26]; 
        int top = 0;
        void push(int val) {
            values[top ++] = val; 
        }
        int pop() {
            top --; 
            return values[top];
        }
        boolean isEmpty() {
            return top == 0; 
        }
        
    }
}

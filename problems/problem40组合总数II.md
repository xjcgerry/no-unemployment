````cpp
class Solution {
private:
	vector<int> candidates;
	vector<vector<int>> res;
	vector<int> cur;
public:
	void DFS(int start, int sum, int target) {
		if (sum == target) {
			res.push_back(cur);
			return;
		}
		for (int i = start; i < candidates.size() && sum + candidates[i] <= target; i++) {
			if (i > start && candidates[i] == candidates[i - 1])    //重复的数剪枝
				continue;
			cur.push_back(candidates[i]);
			DFS(i + 1, sum + candidates[i], target);
			cur.pop_back();
		}
		
	}

	vector<vector<int>> combinationSum2(vector<int> &candidates, int target) {
		sort(candidates.begin(), candidates.end());
		this->candidates = candidates;
		DFS(0, 0, target);
		return res;
	}
};
````

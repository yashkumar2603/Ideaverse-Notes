#### Sum of all elements greater than every element in vector
For every number A_i in vector, print the sum of all the elements greater than A_i, (basically if same element exists multiple times, it wont work).
[C - Sum of Numbers Greater Than Me](https://atcoder.jp/contests/abc331/tasks/abc331_c)
O(n) solution - 
```C++
void solution() {
    // write your code here
    int n;
    cin >> n;
    vector<int> v(n);
    map<int, vector<int>> mp; //auto sorts it
    for (int i = 0; i < n; i++) {
        cin >> v[i];
        mp[v[i]].push_back(i);
    }
    ll s = accumulate(v.begin(), v.end(), 0LL);
    vector<ll> ans(n);

    for (auto [x, i] : mp) {
        s -= (ll)x * i.size();
        for (auto y : i)
            ans[y] = s;
    }
    for (int i = 0; i < n; i++)
        cout << ans[i] << " ";
    cout << nl;
}
```

**For questions like this -** 
[- LeetCode](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii/)
```C++
int minSwaps(vector<int>& nums) {
        int n = nums.size();
        int one = 0;
        // Count the number of 1s
        for (int i = 0; i < n; i++) {
            if (nums[i] == 1) one++;
        }
        if (one == 0 || one == n) return 0;

        // Initialize the number of 0s in the first window
        int zero_count = 0;
        for (int i = 0; i < one; i++) {
            if (nums[i] == 0) zero_count++;
        }
        // Initialize the answer with the zero_count of the first window
        int ans = zero_count;

        // Use a sliding window to find the minimum number of 0s in any window of size 'one'
        for (int i = one; i < n + one; i++) {
            if (nums[i % n] == 0) zero_count++;
            if (nums[(i - one) % n] == 0) zero_count--;
            ans = min(ans, zero_count);
        }
        return ans;
    }
```
The sliding made is very clever, the array was also mentioned to be circular, that is why all the mod and stuff, if it wasn't circular, then the conditions would have been a bit different but how we take the count of 0s will be the same.
- 👋 Hi, I’m @harshadsakpal
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

#include <bits/stdc++.h>
using namespace std;
const int N = 20;
const int INF = 1e9;
int dp[1<<N][N], dist[N][N];
int tsp(int mask, int pos, int n) {
    if(mask == (1<<n) - 1) return dist[pos][0];
    if(dp[mask][pos] != -1) return dp[mask][pos];
    int ans = INF;
    for(int city = 0; city < n; city++) {
        if((mask & (1<<city)) == 0) {
            ans = min(ans, dist[pos][city] + tsp(mask | (1<<city), city, n));
        }
    }
    return dp[mask][pos] = ans;
}
int main() {
    int n;
    cin >> n;
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            cin >> dist[i][j];
        }
    }
    memset(dp, -1, sizeof(dp));
    cout << "The shortest path is " << tsp(1, 0, n) << endl;
    return

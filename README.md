#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

vector<unordered_set<string>> get_subscriptions(int budget, vector<string> newspapers, vector<double> prices) {
    vector<unordered_set<string>> res;
    int n = newspapers.size();
    for (int i = 0; i < (1<<n); i++) {
        double sum = 0;
        unordered_set<string> current;
        for (int j = 0; j < n; j++)
            if (i & (1<<j)) {
                sum += prices[j];
                current.insert(newspapers[j]);
            }
        if(sum <= budget && current.size() > 1) res.push_back(current);
    }
    return res;
}

int main() {
    vector<string> newspapers = {"TOI", "Hindu", "ET", "BM", "HT"};
    vector<double> prices = {26,20.5, 34, 10.5,18};
    int budget = 40;
    vector<unordered_set<string>> subscriptions = get_subscriptions(budget, newspapers, prices);
    for(auto subscription : subscriptions) {
        for (auto newp : subscription)
            cout<<newp<<" ";
        cout<<endl;
    }
    return 0;
}

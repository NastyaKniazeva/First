# First
#include <iostream>
#include <vector>
#include <string>
#include <queue>

using namespace std;

vector<int> read_till(int number)
{
	vector<int> ans;
	while (true)
	{
		int x = 0;
		cin >> x;
		if (x == 0)
			break;
		ans.push_back(x);
	}
	return ans;
}

void say_no()
{
	cout << "N" << endl;
	exit(0);
}

void print_vec(vector<int> vec)
{
	for (auto x : vec)
		cout << x << ' ';
	cout << endl;
}

int main(int argc, char *argv[]) {
	int n;
	cin >> n;
	vector<vector<int>> g(n + 1);
	for (int i = 1; i <= n; ++i)
		g[i] = read_till(0);
	vector<int> partition(n + 1, -1);
	partition[1] = 0;
	queue<int> q;
	q.push(1);
	while (!q.empty())
	{
		int cur = q.front();
		q.pop();
		for (int to : g[cur])
		{
			if (partition[to] != -1 && partition[to] == partition[cur])
				say_no();
			if (partition[to] == -1)
			{
				q.push(to);
				partition[to] = !partition[cur];
			}
		}
	}
	cout << "Y" << endl;
	vector<int> first, second;
	for (int i = 1; i <= n; ++i)
		(partition[i] ? second : first).push_back(i);
	print_vec(first);
	print_vec(second);
	return 0;
}
/*
4
2 3 0
1 3 0
1 2 4 0
3 0

4
2 0
3 0
4 0
1 0
*/

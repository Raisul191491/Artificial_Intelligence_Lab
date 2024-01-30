### N-Queen problem : 
##### Given the length (same width) of the board, show all possible solutions : 
#### Time complexity : n!
#### Space complexity : number of solutions * n ^ 2
#### C++ 
```cpp
#include <bits/stdc++.h>
typedef long long ll;
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(NULL);                    \
    cout.tie(NULL);
#define last                          \
    freopen("input.txt", "r", stdin); \
    freopen("output.txt", "w", stdout);
using namespace std;

bool isSafe(int row, int col, vector<vector<char>>& board) {
    for (int x = 0; x < row; x++) {
        if (board[x][col] == 'Q') {
            return false;
        }
    }

    for (int r = row - 1, c = col - 1; r >= 0 && c >= 0; r--, c--) {
        if (board[r][c] == 'Q') {
            return false;
        }
    }

    for (int r = row - 1, c = col + 1; r >= 0 && c < board.size(); r--, c++) {
        if (board[r][c] == 'Q') {
            return false;
        }
    }

    return true;
}

void addSolution(vector<vector<string>>& ans, vector<vector<char>>& board) {
    vector<string> temp;

    for (int i = 0; i < board.size(); i++) {
        string s = "";
        for (int j = 0; j < board[i].size(); j++) {
            s += board[i][j];
        }

        temp.push_back(s);
    }

    ans.push_back(temp);
    return;
}

void nQueen(int step, int n, vector<vector<string>>& ans,
            vector<vector<char>>& board) {
    if (step == n) {
        addSolution(ans, board);
        return;
    }

    for (int col = 0; col < n; col++) {
        if (isSafe(step, col, board)) {
            board[step][col] = 'Q';
            nQueen(step + 1, n, ans, board);
            board[step][col] = '.';
        }
    }
    return;
}

vector<vector<string>> solveNQueens(int n) {
    vector<vector<char>> board(n, vector<char>(n, '.'));
    vector<vector<string>> ans;

    nQueen(0, n, ans, board);
    return ans;
}

int main() {
    int boardLength;
    cout << "Enter board size: ";
    cin >> boardLength;
    vector<vector<string>> ans = solveNQueens(boardLength);
    cout << "Possible solutions : " << ans.size() << endl << endl;
    for (int i = 0; i < ans.size(); i++) {
        cout << "Solution : " << i + 1 << endl;
        for (int j = 0; j < ans[i].size(); j++) {
            cout << ans[i][j] << endl;
        }
        cout << endl;
    }
}
```

#### Golang
```go
package main

import "fmt"

func main() {

	boardLength := 0
	fmt.Print("Enter the board length : ")
	fmt.Scanln(&boardLength)

	ans := solveNQueens(boardLength)

	fmt.Printf("Total solutions: %d\n\n", len(ans))
	for i := range ans {
		fmt.Printf("Solution %d:\n", i+1)
		for _, line := range ans[i] {
			fmt.Println(line)
		}
		fmt.Println()
	}
}

func solveNQueens(n int) [][]string {
	b := make([][]rune, n)
	for i := range b {
		b[i] = make([]rune, n)
		for j := range b[i] {
			b[i][j] = '.'
		}
	}

	ans := [][]string{}
	nQueen(0, n, &ans, b)

	return ans
}

func nQueen(step, n int, ans *[][]string, board [][]rune) {
	if step == n {
		addAns(ans, board)
		return
	}

	for col := 0; col < n; col++ {
		if isSafe(board, step, col) {
			board[step][col] = 'Q'
			nQueen(step+1, n, ans, board)
			board[step][col] = '.'
		}
	}
}

func isSafe(b [][]rune, row, col int) bool {
	for x := 0; x < row; x++ {
		if b[x][col] == 'Q' {
			return false
		}
	}

	r := row
	c := col
	for r >= 0 && c >= 0 {
		if b[r][c] == 'Q' {
			return false
		}
		r--
		c--
	}

	for row >= 0 && col < len(b) {
		if b[row][col] == 'Q' {
			return false
		}
		row--
		col++
	}

	return true
}

func addAns(ans *[][]string, b [][]rune) {

	temp := []string{}

	for i := 0; i < len(b); i++ {
		s := ""
		for j := 0; j < len(b[i]); j++ {
			s += string(b[i][j])
		}
		temp = append(temp, s)
	}

	*ans = append(*ans, temp)
}

```
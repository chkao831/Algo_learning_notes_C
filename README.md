
# Vector
> all of its elements are of the same data type
### Initialization
```cpp
/* initialize vector of zeros */
vector<int> v(n, 0);

/* initialize vector with elements */
vector<int> v = {1, 2}; // std::initializer_list<int>

/* initialize vector of pairs */
vector<pair<int, int>> vec_pair;
vec_pair.reserve(nums.size()); // reserve the space, for later push_back

/* initialize 2d vector of ints, with default size and zeros */
vector<vector<int>> matrix_2d(
    grid.size(),
    vector<int>(grid[0].size(), 0)
);

/* initialize a graph for nodes with neighbor nodes */
vector<vector<int>> graph(n);
for (vector<int> road: roads){
    graph[road[0]].push_back(road[1]);
    graph[road[1]].push_back(road[0]);
}
```
### Methods
- Push Back
    ```cpp
    // to push back pair of ints, choose from
    vec_pair.push_back(make_pair(x, y))
    vec_pair.push_back({x, y})
    ```
- Peek Back/Pop Back (for LIFO Stack, see and pop the stack pop)
    ```cpp
    vec_pair.back(); // peek the stack top
    vec_pair.pop_back(); // pop the stack top
    ```
- Sort
    ```cpp
    // sort in ascending order by the first key of pair
    sort(vec_pair.begin(), vec_pair.end(),
        [](auto& p1, auto& p2){return (p1.first < p2.first);});
    // sort in descending order
    sort(vec_pair.begin(), vec_pair.end(),
        [](auto& p1, auto& p2){return (p1.first > p2.first);});
    sort(vec.rbegin(), vec.rend()); // also in descending order
    ```
- `std::all_of, std::any_of, std::none_of`
    ```cpp
    vector<bool> unlocked_rooms(rooms.size(), false);

    // check if all rooms are true
    return all_of(unlocked_rooms.begin(), unlocked_rooms.end(), [](bool v) { return v; });
    // check if all rooms are true
    return all_of(unlocked_rooms.begin(), unlocked_rooms.end(), [](bool v) { return !v; });
    return none_of(unlocked_rooms.begin(), unlocked_rooms.end(), [](bool v) { return v; });
    ```
- Check empty
    ```cpp
    vec_pair.empty(); //for stack while loop
    ```
- Swap
    ```cpp
    vector<int> v = {1, 2};
    swap(v[0], v[1]); // v = {2, 1}
    ```
# Pair (Tuple)
> could contain different two types
### Initialization
```cpp
pair<int, int> p = make_pair(1, 2) // or {1, 2}
```
### Methods
- Extract elements
    ```cpp
    int p1 = p.first;
    int p2 = p.second;
    ```
# Hashmap: unordered_map
> no ordering\
> implemented by hash table\
> O(1) search, insertion, deletion on average\
> not compatible with customized hashing such as pair as keys
### Initialization
```cpp
unordered_map<int, int> memo;
```
### Methods
- Key existence
    ```cpp
    if (memo.count(key) == 0) // not exist
    if (memo.find[key] == memo.end()) // equi. to not exist 
    ```
    - For **counter** initialization, where the value is of `int` type, don't need to check if key exists while incrementing. Simply increment the count, 
        ```cpp
        // no need
        if (memo.count(key)) {
            memo[key] += 1;
        } else {
            memo[key] = 1;
        }

        // instead
        memo[key] += 1;
        ```

- Check key counts
    ```cpp
    memo.size();
    ```
- Deletion
    ```cpp
    memo.erase(key);
    ```
# Map
> increasing order\
> implemented by self balancing BST\
> O(logN) search, insertion, deletion on average
### Initialization
```cpp
map<pair<int, int>, int> memo;
```
### Methods
- Access/revise key with type of pair
    ```cpp
    memo[{x, y}]
    ```
- Key existence
    ```cpp
    if (memo.count({x, y}) == 0) // not exist
    ```

# Queue
### Initialization
```cpp
queue<pair<int, int>> queue;
```

### Methods
- Check empty
    ```cpp
    if (!queue.empty()){}
    ```
- FIFO Peek and Pop (for BFS)
    ```cpp
    pair<int, int> land = queue.front(); // peek
    queue.pop() // pop
    ```

# Priority Queue
> max heap by default.
### Initialization
```cpp
priority_queue<pair<int, char>> pq; // max heap
```
### Methods
- push
    ```cpp
    for (auto& pair: map_char_freq){
        pq.push({pair.second, pair.first});
    }

    // for min heap
    pq.push({-pair.second, pair.first})
    ```
- Check empty
    ```cpp
    pq.empty();
    ```
- Peek/Pop
    ```cpp
    pq.top();
    pq.pop();
    ```
# Appendix
## Generic initialization with braces
```cpp
vector<int> func(...){
    return {-1}; // return a vector with an element -1

queue<vector<int>> q;
q.push({0, 0, -1});
```
## Usage of `auto`
```cpp
vector<vector<int>>& redEdges;
for (auto& redEdge: redEdges) {}
for (vector<int>& redEdge: redEdges) {} // equivalent 

vector<vector<pair<int, int>>> adj(n);
for (auto& [neighbor, color]: adj[node]) {}
// is equivalent to
for (pair<int, int>& p: adj[node]){
    int neighbor = p.first;
    int color = p.second;
}
```
## `min()` and `max()`
```cpp
int min=INT_MAX;
int max=INT_MIN;
 
// takes in two items. For three+ items, do double+ operations.
min(a, b); max(a, b);
```
## Returning while performing an assignment
```cpp
// return a value, while assigning this value to the key in the map
return memo[{x,y}] = matrix[x][y] + min(left, min(middle, right));
```
## String and Character
```cpp
string s = "abc";
char c = 'a';

isalpha(c); // true
isdigit(c); // false
char lower_c = tolower(c);
char upper_c = toupper(c);
```
## Built-in Primitive Data Type
### Integers
|  | bytes | typical range |
|---|---|---|
| short int | 2 | -32768 ~ 32767 |
| unsigned short int | 2 | 0 ~ 65535 |
| int | 4 | -2147483648 ~ 2147483647 |
| unsigned int | 4 | 0 ~ 4294967295 |
| long int | 4 |  |
| unsigned long int | 4 |  |
| long long int | 8 |  |
| unsigned long long int | 8 |  |

### Floating-Point
|  | bytes | typical range |
|---|---|---|
| float | 4 | -3.4E-38 ~ 3.4E38 |
| double | 8 | -1.7E308 ~ 1.7E308 |
| long double | 8 |  |

### bool
Boolean variables are set to either `true` or `false`. Has 1 byte.
### char
Actually an integer data type that uses 1 byte of memory. Commonly used method for encoding each character to a unique number is ASCII.

## Division Calculation
In C++, division calculation is possible using the division operator denoted by `/`. We can divide integers and floating point numbers using the `/` operator. 
```cpp
// the remainder is discarded if dividend is not exactly divisible
int a; int b;
int c = a/b;
//In order to use the double version, at least one of the ints must be explicitly casted to a double.
double c = a/(double)b;

float = float / float
```
```cpp
// The ceil() function in C++ returns the smallest possible integer value which is greater than or equal to the given argument.

#include <cmath>
cout << ceil(15.08); // output = 16
```

## Read in file/stream
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;


int main() {
    string line;

    ifstream myFile;
    myFile.open("test.txt");

    // istream& getline (istream& is, string& str, char delim);
    while (getline(myFile, line)) {
        cout << line << endl;
    }
    
    // string name;
    // int score;
    // while (myFile >> name >> score) {
    //    cout << name << " " << score << "\n";
    //    names.push_back(name);
    //    scores.push_back(score);
    //}
    
    myFile.close();
    return 0;
}
```
```cpp
#include <iostream>
#include <sstream>
#include <string>
#include <vector>
using namespace std;

int main() {
    string str = "1,2,3,4,5,6";
    vector<int> vect;

    stringstream ss(str);

    for (int i; ss >> i;) {
        vect.push_back(i);    
        if (ss.peek() == ',')
            ss.ignore();
    }
}
```

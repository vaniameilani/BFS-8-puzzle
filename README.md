# BFS-8-puzzle

BFS adalah salah satu metode algoritma pencarian dimana dalam pencariannya secara melebar, yaitu dari root akan memeriksa ke node ke sebelah kiri, kemudian memeriksa ke node sebelahnya / node sebelah kanan. 
Pencarian akan turun ke tingkat node setelahnya apabila pencarian nilai node sebelah kanan telah selesai. 
Urutan pencariannya :
root - node kiri - node kanan. 

Untuk kali, program permasalahan yang akan dibahas adalah 8-puzzle.
Berikut adalah penjelasan dari program 8-puzzle dengan menggunakan BFS  :
1. Mendeklarasikan Initial state 
```
for(int i = 0; i < n; ++i)
    {
        cin >> x;
        start_state->state.push_back(x);
    }
 ```
2. Mendeklarasikan end state secara global 
```
vector<int> final_state = {1, 2, 3, 4, 5, 6, 7, 8, 0};
```
3. Fungsi untuk membuat sebuah node baru 
```
node* createNewState(node* state, int x, int y)
{
    node* new_state = new node();
    new_state->state = state->state;
    swap(new_state->state[x], new_state->state[y]);
    
    return new_state;
}
```
4. Fungsi dalam pencarian secara BFS
```
void BFS(node* start_state)
{
    visit[start_state->state] = 1;
    
    int pos, row, col;
    
    node *curr = new node(), *child = new node();
    queue<node*> q;    
    q.push(start_state);
    
    while(!q.empty())
    {
        curr = q.front();
        q.pop();
        
        if(curr->state == final_state)
        {
            printPath(curr);
            return;
        }
        
        for(int i = 0; i < n; ++i)
        {
            if(curr->state[i] == 0)
            {
                pos = i;
                break;
            }
        }
        row = pos / 3;
        col = pos % 3;

        if(col != 0)
        {
            child = createNewState(curr, pos, pos-1);
            
            if(visit[child->state] == 0)
            {
                visit[child->state] = 1;
                child->parent = curr;
                q.push(child);
            }
        }

        if(col != 2)
        {
            child = createNewState(curr, pos, pos+1);
            
            if(visit[child->state] == 0)
            {
                visit[child->state] = 1;
                child->parent = curr;
                q.push(child);
            }
        }

        if(row != 0)
        {
            child = createNewState(curr, pos, pos-3);
            
            if(visit[child->state] == 0)
            {
                visit[child->state] = 1;
                child->parent = curr;
                q.push(child);
            }
        }

        if(row != 2)
        {
            child = createNewState(curr, pos, pos+3);
            
            if(visit[child->state] == 0)
            {
                visit[child->state] = 1;
                child->parent = curr;
                q.push(child);
            }
        }
    }
}
```
5. Fungsi untuk print path moving
```
void printPath(node* state)
{
    vector<node*> path;
    while(state)
    {
        path.push_back(state);
        state = state->parent;
    }
    
    cout << "Moves Required: " << path.size()-1 << endl;
    for(int i = path.size()-1; i >= 0; --i)
        printState(path[i]->state);
}
```

6. Fungsi untuk print state
```
void printState(vector<int> state)
{
    for(int i = 0; i < 9; )
    {
        for(int j = 0; j < 3; ++j, ++i)
            cout << state[i] << " ";
        cout << endl;
    }
    cout << endl;
}

```

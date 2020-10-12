## BASICS

### 1.Find the maximum element in a binary tree.
> a. Use any one traversal technique and keep updating the maximum value on each node.
> b. recursive :-
```
int findMax(struct node* root)
{
if(!root)
return 0;
return max(max(findMax(root->left),findMax(root->right)),root->data);
}
```
### 2.Search an element in a binary tree.
> a. Use any one traversal technique and keep updating the maximum value on each node.
> b. recursive :-
```
bool search(node* root,int val)
{
    if(!root)
    return false;
    if(root->data==val)
    return true;
    return search(root->left,val)||search(root->right,val);
}
```
### 3.Find the size of binary tree.
> a. Use any one traversal technique and keep updating the maximum value on each node.
> b. recursive :-
```
int size(node* root)
{
    if(!root)
    return 0;
    return size(root->left)+size(root->right)+1;
}
```
### 4.Print the level order data in reverse order.
                        1
                       / \ 
                      2   3
                     / \  /\
                    4   5 6 7

                    print: 4 5 6 7 2 3 1
```
void reverse_level(node* root)
{
    queue<node* >q;
    stack<node* >s;
    if(!root)
    return ;
    q.push(root);
    whil(!q.empty())
    {
        temp=q.front();
        q.pop();
        s.push(temp);
        if(temp->right);
        q.push(temp->right);
        if(temp->left)
        q.push(temp->left);
    }
    //print s
}
```
### 5.Write the algo for deleting a tree.
```
void delete_tree(node* root)
{
    if(!root)
    return ;
    delete_tree(root->left);
    delete_tree(root->right);
    free(root);
}
```
### 6.Find the height of binary tree.
```
int height(node* root)
{
    if(!root)
    return 0;
    return max(height(root->left),height(root->right))+1;
}
```
Can be done iteratively using level order by adding a delimiter NULL after each level.

### 7.check if two trees are structurally identical.
```
bool is_identical(node* root1,node* root2)
{
    if(!root1&&!root2)
    return true;
    if(!root1||!root2)
    return false;
    if(root1->val!=root2->val)
    return false;
    return is_identical(root1->right,root2->right)&&is_identical(root1->left,root2->left);
}
```
### 8.Find the diameter of binary tree.
```
int diameter(node* root)
{
    if(!root)
    return 0;
    int l_height=height(root->left);
    int r_height=height(root->right);
    int l_d=diameter(root->left);
    int r_d=diameter(root->right);
    return max(max(l_d,r_d),l_height+r_height+1);
}
```
Complexity: O(N*N).
Optimization:O(N)
```

int height(node* root,int *ans)
{
   if(!root)
   return 0;
   int l=height(root->left);
   int r=height(root->right);
   ans=max(ans,l+r+1);
   return max(l,r)+1;
}


int diameter(node* root)
{
    int ans=INT_MIN;
    int h=height(root,&ans);
    return ans;
}
```
### 9.Print the path from root to the given node.
```
bool print path(node* root,int x,vector<int>&arr)
{
    if(!root)
    return false;
    arr.push(root->data);
    if(root->data==x)
    return true;
    if(path(root->left,x,arr)||path(root->right,x,arr))
    return true;
    arr.pop_back();
    return false;
}
```

### 10.Print all root-to-leaf paths.
```
void path_recur(node* root,int path[],int len)
{
    if(!root)
    return ;
    path[len++]=root->data;
    if(!root->left&&!root->right)
    print_arr(path,len);
    else
    {
        path_recur(root->left,path,len);
        path_len(root->right,path,len);
    }
}
void print_arr(int path[],int len)
{
    for(int i=0;i<len;i++)
    cout<<path[i]<<" ";
}
```
### 11.check the existence of path with given sum.
```
bool check(node* root,int sum,int temp)
{
    if(!temp)
    return true;
    if(!root||temp<0)
    return false;
    return check(root->left,sum,temp-root->data)||check(root->right,sum,temp-root->data);
}
```
### 12.Check the existence of path with given sum(root to leaf path).
```
bool hasPathSum(Node *node, int sum) {
    if(sum<0||(!sum&&node)||(sum&&!node))
    return false;
    if(!node&&!sum)
    return true;
    return hasPathSum(node->left,sum-node->data)||hasPathSum(node->right,sum-node->data);
    //return false;
}
```
### 13.Find sum of all nodes in a binary tree.
```
int sum(node* root)
{
    if(!root)
    return 0;
    return root->val+sum(root->left)+sum(root->right);
}
```
### 14.Convert the given binary tree to its mirror .
A. Recursive:
```
Node* mir(Node* root)
{
    if(root)
    {
    mir(root->left);
    mir(root->right);
    swap(root->left,root->right);
    }
    return root;
}
void mirror(Node* node) 
{
     node=mir(node);
}
```
B. Iterative:
```
void mirror(Node* root) 
{ 
    if (root == NULL) 
        return; 
  
    queue<Node*> q; 
    q.push(root); 
    while (!q.empty()) 
    { 
        Node* curr = q.front(); 
        q.pop(); 
        swap(curr->left, curr->right); 
        if (curr->left) 
            q.push(curr->left); 
        if (curr->right) 
            q.push(curr->right); 
    } 
} 
```
### 15.Check if two trees are mirror images of each other.
```
bool is_mirror(node* root1,node* root2)
{
    if(!root1&&!root2)
    return true;
    if(!root1||!root2)
    return false;
    if(root1->data!=root2->data)
    return false;
    return is_mirror(root1->left,root2->right)&&is_mirror(root1->right,root2->left);
}
```
Iterative:
Use two queues -
```
q1.push(root1);  
q2.push(root2);
    while(!q1.empty() and !q2.empty()){
        t1 =  q1.front(); 
        q1.pop();     
        t2 =  q2.front(); 
        q2.pop(); 
        if (t1 == NULL and t2 == NULL)continue; 
        if((!t1) || (!t2)) return false;
        if(t1->data != t2->data)return false;
        q1.push(t1->left); 
        q2.push(t2->right); 
        q1.push(t1->right);
        q2.push(t2->left);  
    }
    return true; 
```
### 16.Chech if the tree is the mirror of itself.
A. Recursive:
```
bool symetric(node* root)
{
    return is_mirror(root,root);
}
```
B. Iterative:
```
bool isSymmetric(struct Node* root) 
{ 
    if(root == NULL) 
        return true; 
    if(!root->left && !root->right) 
        return true; 
    queue <Node*> q; 
    q.push(root); 
    q.push(root); 
    Node* leftNode, *rightNode; 
      
    while(!q.empty()){ 
          
        leftNode = q.front(); 
        q.pop(); 
          
        rightNode = q.front(); 
        q.pop(); 
        if(leftNode->key != rightNode->key){ 
        return false; 
        } 
        if(leftNode->left && rightNode->right){ 
            q.push(leftNode->left); 
            q.push(rightNode->right); 
        } 
        else if (leftNode->left || rightNode->right) 
        return false; 
        if(leftNode->right && rightNode->left){ 
            q.push(leftNode->right); 
            q.push(rightNode->left); 
        } 
        else if(leftNode->right || rightNode->left) 
        return false; 
    } 
      
    return true; 
} 
```
### 17.Find the LCA of two nodes in a Binary Tree.
```
node* LCA(node* root,node* a,node* b)
{
    if(!root)
    return NULL;
    if(root==a||root==b)
    return root;
    left=LCA(root->left,a,b);
    right=LCA(root->right,a,b);
    if(left&&right)
    return root;
    return left?left:right;
}
```
### 18.Construct the binary tree from the given inorder and preorder traversal.
```

## BASICS
### 1.Find an element in binary search tree.
```
node* find(node* root,int val)
{
    if(!root)
    return root;
    if(root->data==val)
    return root;
    if(root->data>val)
    return find(root->left,val);
    return find(root->right,val);
}
```
### 2.Find the minimum and maximum elements in BST.
Minimum:
```
node* minimum(node* root)
{
    if(!root)
    return root;
    if(!root->left)
    return root;
    return minimum(root->left);
}
```
Maximum:
```
node* maximum(node* root)
{
    if(!root)
    return root;
    if(!root->right)
    return root;
    return maximum(root->right);
}
```
Can be done iteratively in constant space.
### 3.Find the LCA of two nodes.
```
Node* LCA(Node* root,int a,int b)
{
    if(!root)
    return root;
    if(root->data==a||root->data==b)
    return root;
    if((root->data>a&&root->data<b)||(root->data<a&&root->data>b))
    return root;
    if((root->data<a&&root->data<b))
    return LCA(root->right,a,b);
    return LCA(root->left,a,b);
}
```
### 4.Find the shortest path between two nodes in a BST.
**Dist(n1, n2) = Dist(root, n1) + Dist(root, n2) - 2*Dist(root, lca)**
```
int distanceFromRoot(struct Node* root, int x) 
{ 
    if (root->key == x) 
        return 0; 
    else if (root->key > x) 
        return 1 + distanceFromRoot(root->left, x); 
    return 1 + distanceFromRoot(root->right, x); 
} 
int distanceBetween2(struct Node* root, int a, int b) 
{ 
    if (!root) 
        return 0; 
    if (root->key > a && root->key > b) 
        return distanceBetween2(root->left, a, b); 
    if (root->key < a && root->key < b)  
        return distanceBetween2(root->right, a, b); 
    if (root->key >= a && root->key <= b) 
        return distanceFromRoot(root, a) +  
               distanceFromRoot(root, b); 
}  
int findDistWrapper(Node *root, int a, int b) 
{ 
   if (a > b) 
     swap(a, b); 
   return distanceBetween2(root, a, b);    
} 
```
Similarly, can be done for binary tree also.
### 5.Give an algorithm for counting the number of BSTs possible with n nodes.
```
int numTrees(int n) {
        int dp[n+1];
        memset(dp,0,sizeof(dp));
        dp[0]=1,dp[1]=1;
        for(int i=2;i<=n;i++)
        {
            for(int j=1;j<=i;j++)
                dp[i]=dp[i]+dp[j-1]*dp[i-j];
        }
        return dp[n];
    }
```
Total number of possible Binary Search Trees with n different keys (countBST(n)) = Catalan number Cn = (2n)! / ((n + 1)! * n!)

### 6.Check whether the given tree is BST.
A.For each node, check if max value in left subtree is smaller than the node and min value in right subtree greater than the node.Complexity:O(n*n).
```
int isBST(struct node* node)  
{  
  if (node == NULL)  
    return 1;  
  if (node->left!=NULL && maxValue(node->left) > node->data)  
    return 0;  
  if (node->right!=NULL && minValue(node->right) < node->data)  
    return 0;  
  if (!isBST(node->left) || !isBST(node->right))  
    return 0;  
  return 1;  
}  
```
B.A better solution looks at each node only once. The trick is to write a utility helper function isBSTUtil(struct node* node, int min, int max) that traverses down the tree keeping track of the narrowing min and max allowed values as it goes, looking at each node only once. The initial values for min and max should be INT_MIN and INT_MAX — they narrow from there.
```
bool is_bst(Node* root,int min,int max)
{
    if(!root)
    return true;
    if(root->data<min||root->data>max)
    return false;
    return is_bst(root->left,min,root->data-1)&&is_bst(root->right,root->data+1,max);
}
bool isBST(Node* root) {
    // Your code here
    if(!root)
    return true;
    return is_bst(root,-1,10000000);
}
```
C. Check if the inorder traversal of the tree gives a sorted array.
```
bool isBSTUtil(struct Node* root, Node *&prev) 
{ 
    if (root) 
    { 
        if (!isBSTUtil(root->left, prev)) 
          return false;  
        if (prev != NULL && root->data <= prev->data) 
          return false; 
   
        prev = root; 
   
        return isBSTUtil(root->right, prev); 
    } 
   
    return true; 
} 
  
bool isBST(Node *root) 
{ 
   Node *prev = NULL; 
   return isBSTUtil(root, prev); 
} 
```
### 7.Convert BST to DLL.
A.Using global or static variable:
```
void bst_to_dll(node* root,node **head)
{
    if(!root)
    return ;
    static node* prev=NULL;
    bst_to_dll(root->left,head);
    if(!prev)
    head=root;
    else
    {
        root->left=prev;
        prev->right=root;
    }
    prev=root;
    bst_to_dll(root->right,head);
}
node* convert(node* root)
{
    node* head=NULL;
    bst_to_dll(root,&head);
    return head;
}
```
B. Without using global or static variable:
```
void BToDLL(Node* root, Node*& head) 
{  
    if (root == NULL) 
        return; 
    BToDLL(root->right, head); 
    root->right = head; 
    if (head != NULL) 
        head->left = root; 
    head = root; 
    BToDLL(root->left, head); 
} 
```
### 8.Given a sorted doubly linked list, convert it to balanced BST.





### 9.Find the kth smallest element in the binary tree.
```
node* kth_smallest(node* root,int *c,int k)
{
    if(!root)
    return root;
    node* left=kth_smallest(root->left,c,k);
    if(left)
    return left;
    if(++c==k)
    return root;
    return kth_smallest(root->right,c,k);

}
```
### 10.Find the kth largest element in the binary tree.
```
Node* kth_lar(Node* root,int &k)
{
    if(!root)
    return root;
    Node* right=kth_lar(root->right,k);
    if(right)
    return right;
    if(--k==0)
    return root;
    return kth_lar(root->left,k);
}
int kthLargest(Node *root, int k)
{
    Node* temp=kth_lar(root,k);
    return temp->data;
}
```
### 11.Given a BST and two numbers k1 and k2, print all the elements of the bst in the range k1 and k2.
```
void range(node* root,int k1,int k2)
{
    if(!root)
    return ;
    if(root->data>=k1)
    range(root->left,k1,k2);
    if(root->data>=k1&&root->data<=k2)
    cout<<root->data<<" ";
    if(root->data<=k2)
    range(root->right,k1,k2);
}
```
### 12.Convert a given tree to its Sum Tree.
```
int toSumTree(node *Node)  
{  
    if(Node == NULL)  
    return 0;   
    int old_val = Node->data; 
    Node->data = toSumTree(Node->left) + toSumTree(Node->right);  
    return Node->data + old_val;  
}  
```
### 13.Check if a given Binary Tree is SumTree.
```
int isSumTree(struct node* node) 
{ 
    int ls; 
    int rs; 
    if(node == NULL || isLeaf(node)) 
        return 1; 
  
    if( isSumTree(node->left) && isSumTree(node->right)) 
    { 
        if(node->left == NULL) 
            ls = 0; 
        else if(isLeaf(node->left)) 
            ls = node->left->data; 
        else
            ls = 2*(node->left->data); 
        if(node->right == NULL) 
            rs = 0; 
        else if(isLeaf(node->right)) 
            rs = node->right->data; 
        else
            rs = 2*(node->right->data); 
        return(node->data == ls + rs); 
    } 
  
    return 0; 
} 
```
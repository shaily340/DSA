## FREQUENTLY ASKED!!
### 1.Modify a binary tree to get preorder traversal using right pointers only.
```
Node* modifytree(Node* root) 
{ 
    struct Node* right = root->right; 
    struct Node* rightMost = root; 
  
    // if the left tree exists 
    if (root->left) { 
  
        // get the right-most of the 
        // original left subtree 
        rightMost = modifytree(root->left); 
  
        // set root right to left subtree 
        root->right = root->left; 
        root->left = NULL; 
    } 
  
    // if the right subtree does 
    // not exists we are done! 
    if (!right)  
        return rightMost; 
  
    // set right pointer of right-most 
    // of the original left subtree 
    rightMost->right = right; 
  
    // modify the rightsubtree 
    rightMost = modifytree(right); 
    return rightMost; 
} 
```
### 2.Print the boundary traversal of the given binary tree.
```
void printfront(Node* root,vector<int>&ans)
{
    if(!root||(!root->left&&!root->right))
    return ;
    ans.push_back(root->data);
    if(root->left)
    printfront(root->left,ans);
    else
    printfront(root->right,ans);
}
void printback(Node* root,vector<int>&ans)
{
    if(!root||(!root->left&&!root->right))
    return ;
    if(root->right)
    printback(root->right,ans);
    else
    printback(root->left,ans);
    ans.push_back(root->data);
}
void printleaves(Node* root,vector<int>&ans)
{
    if(!root)
    return ;
    if(!root->left&&!root->right)
    ans.push_back(root->data);
    printleaves(root->left,ans);
    printleaves(root->right,ans);
}
vector <int> printBoundary(Node *root)
{
     //Your code here
     vector<int>ans;
     if(!root||(!root->left&&!root->right))
     return {root->data};
    ans.push_back(root->data);
     printfront(root->left,ans);
     printleaves(root->left,ans);
     printleaves(root->right,ans);
     printback(root->right,ans);
     return ans;
     
}
```
This method works for complete binary trees.
### 3.Convert binary tree to doubly linked list.
```
void convert(node* root,node* head)
{
    if(!root)
    return ;
    static node* prev=NULL;
    convert(root->left,head);
    if(prev==NULL)
    head=root;
    else
    {
        root->left=prev;
        prev->right=root;
    }
    prev=root;
    convert(root->right,head);
}
```
### 4.Check if a binary tree is a subtree of another tree.
A. Brute force:O(n*n)-
```
bool is_subtree(node* root1,node* root2)
{
    
}
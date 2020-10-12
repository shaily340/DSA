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
bool areIdentical(node * root1, node *root2)  
{  
    if (root1 == NULL && root2 == NULL)  
        return true;  
  
    if (root1 == NULL || root2 == NULL)  
        return false;  
    return (root1->data == root2->data &&  
            areIdentical(root1->left, root2->left) &&  
            areIdentical(root1->right, root2->right) );  
}  
bool isSubtree(node *T, node *S)  
{  
    if (S == NULL)  
        return true;  
  
    if (T == NULL)  
        return false;  
    if (areIdentical(T, S))  
        return true;  
    return isSubtree(T->left, S) ||  
        isSubtree(T->right, S);  
}  
```
B.Optimization:The idea is based on the fact that inorder and preorder/postorder uniquely identify a binary tree. Tree S is a subtree of T if both inorder and preorder traversals of S arew substrings of inorder and preorder traversals of T respectively.
```
void preorder(TreeNode* root, std::string& str) {
if(!root) {
str.push_back('$');
return;
}
str.push_back(root->val);
preorder(root->left, str);
preorder(root->right, str);
}
class Solution {
public:
    bool isSubtree(TreeNode* s, TreeNode* t) {
        string main_tree;
preorder(s, main_tree);
string sub_tree;
preorder(t, sub_tree);
return main_tree.find(sub_tree) != std::string::npos;//check inorder also
    }
```
### 5.How to store a binary tree in a file and then read back?
**Serialize and deserialize a binary tree**
#### If given Tree is Binary Search Tree?
>If the given Binary Tree is Binary Search Tree, we can store it by either storing preorder or postorder traversal. In case of Binary Search Trees, only preorder or postorder traversal is sufficient to store structure information.

#### If given Binary Tree is Complete Tree?
>A Binary Tree is complete if all levels are completely filled except possibly the last level and all nodes of last level are as left as possible (Binary Heaps are complete Binary Tree). For a complete Binary Tree, level order traversal is sufficient to store the tree. We know that the first node is root, next two nodes are nodes of next level, next four nodes are nodes of 2nd level and so on.

#### If given Binary Tree is Full Tree?
>A full Binary is a Binary Tree where every node has either 0 or 2 children. It is easy to serialize such trees as every internal node has 2 children. We can simply store preorder traversal and store a bit with every node to indicate whether the node is an internal node or a leaf node.

#### How to store a general Binary Tree?
>A simple solution is to store both Inorder and Preorder traversals. This solution requires requires space twice the size of Binary Tree.
We can save space by storing Preorder traversal and a marker for NULL pointers.
```
void serialize(Node *root, FILE *fp) 
{ 
    // If current node is NULL, store marker 
    if (root == NULL) 
    { 
        fprintf(fp, "%d ", MARKER); 
        return; 
    } 
  
    // Else, store current node and recur for its children 
    fprintf(fp, "%d ", root->key); 
    serialize(root->left, fp); 
    serialize(root->right, fp); 
} 
  
// This function constructs a tree from a file pointed by 'fp' 
void deSerialize(Node *&root, FILE *fp) 
{ 
    // Read next item from file. If theere are no more items or next 
    // item is marker, then return 
    int val; 
    if ( !fscanf(fp, "%d ", &val) || val == MARKER) 
       return; 
  
    // Else create node with this item and recur for children 
    root = newNode(val); 
    deSerialize(root->left, fp); 
    deSerialize(root->right, fp); 
} 
```
### 6.Views of Binary Tree.
**A.Left View**
```
void left(Node* root,int level,int *max_level)
{
    if(!root)
    return ;
    if(level>*max_level)
    {cout<<root->data<<" ";
        *max_level=level;
    }
    left(root->left,level+1,max_level);
    left(root->right,level+1,max_level);
}
void leftView(Node *root)
{
   int level=1,max_level=0;
   left(root,level,&max_level);
}
```
**Top View:**
```
void fillMap(Node* root,int d,int l,map<int,pair<int,int>> &m){ 
    if(root==NULL) return; 
  
    if(m.count(d)==0){ 
        m[d] = make_pair(root->data,l); 
    }else if(m[d].second>l){ 
        m[d] = make_pair(root->data,l); 
    } 
  
    fillMap(root->left,d-1,l+1,m); 
    fillMap(root->right,d+1,l+1,m); 
} 
void topView(struct Node *root){  
    map<int,pair<int,int>> m; 
  
    fillMap(root,0,0,m); 
  
    for(auto it=m.begin();it!=m.end();it++){ 
        cout << it->second.first << " "; 
    } 
} 
```
**Bottom View:**
```
void fillMap(Node* root,int d,int l,map<int,pair<int,int>> &m){ 
    if(root==NULL) return; 
  
    if(m.count(d)==0){ 
        m[d] = make_pair(root->data,l); 
    }else if(m[d].second<=l){ 
        m[d] = make_pair(root->data,l); 
    } 
  
    fillMap(root->left,d-1,l+1,m); 
    fillMap(root->right,d+1,l+1,m); 
} 
vector <int> bottomView(Node *root) 
{
    map<int,pair<int,int>> m; 
  
    fillMap(root,0,0,m); 
  vector<int>ans;
    for(auto it=m.begin();it!=m.end();it++){ 
        ans.push_back(it->second.first); 
    } 
    return ans;
} 
```
**Right View:**
```
void rightViewUtil(struct Node *root,  
                   int level, int *max_level) 
{ 
    if (root == NULL) return; 
    if (*max_level < level) 
    { 
        cout << root->data << "\t"; 
        *max_level = level; 
    } 
    rightViewUtil(root->right, level + 1, max_level); 
    rightViewUtil(root->left, level + 1, max_level); 
} 
void rightView(struct Node *root) 
{ 
    int max_level = 0; 
    rightViewUtil(root, 1, &max_level); 
} 
```
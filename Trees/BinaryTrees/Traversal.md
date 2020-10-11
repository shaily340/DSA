## TREE TRAVELSAL 

### Depth First Traversals:
                  10
                 /  \
                20   30
               /  \    \
              40   60    80
            /              \
           100             90


### 1.PREORDER :

```
 Algorithm
  Preorder(tree)
   1. Visit the root.
   2. Traverse the left subtree, i.e., call Preorder (left-subtree)
   3. Traverse the right subtree, i.e., call Preorder(right-subtree)
```
                  
> Recursive:
```
void preorder(node* root)
{
    if(root)
    {
        cout<<root->val<<" ";
        preorder(root->left);
        preorder(root->right);
    }
}
```
>Iterative:

```
void preorder(node* root)
{
    stack<node*> s;
    while(1)
    {
        while(root)
        {
            cout<<root->val<<" ";
            s.push(root);
            root=root->left;
        }
        if(s.empty())
        break;
        root=s.top();
        s.pop();
        root=root->right;
    }
}
```
________

### 2.INORDER:

```
Algorithm 
Inorder(tree)
   1. Traverse the left subtree, i.e., call Inorder(left-subtree)
   2. Visit the root.
   3. Traverse the right subtree, i.e., call Inorder(right-subtree)
```
>Recursive:

```
void inorder(node* root)
{
    if(root)
    {
        inorder(root->left);
        cout<<root->val<<" ";
        inorder(root->right);
    }
}
```

>Iterative:

```
void inorder(node* root)
{
    stack<node* >s;
    while(1)
    {
        while(root)
        {
            s.push(root);
            root=root->left;
        }
        if(s.empty())
        break;
        root=s.top();
        s.pop();
        cout<<root->val<<" ";
        root=root->right;
    }
}
```
________
### 3.POSTORDER

```
Algorithm 
Postorder(tree)
   1. Traverse the left subtree, i.e., call Postorder(left-subtree)
   2. Traverse the right subtree, i.e., call Postorder(right-subtree)
   3. Visit the root.
```

>Recursive :

```
void postorder(node* root)
{
    if(root)
    {
        inorder(root->left);
        inorder(root->right);
        cout<<root->val<<" ";
    }
}
```

>Iterative:

```
vector <int> postOrder(Node* root)
{
  // Your code here
  stack<Node* >s;
  vector<int>ans;
  if(!root)
  return {};
  s.push(root);
  Node* temp;
  while(!s.empty())
  {
      temp=s.top();
      s.pop();
      ans.push_back(temp->data);
      if(temp->left)
      s.push(temp->left);
      if(temp->right)
      s.push(temp->right);
  }
  reverse(ans.begin(),ans.end());
  return ans;
}
```
___________
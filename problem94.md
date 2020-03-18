# 94. 二叉树的中序遍历
* 前序遍历：访问完根子树后，遍历左子树前，要将右子树压入栈。
* 后序遍历：每到一个结点A，就立即访问它，然后将左子树压入栈，再遍历右子树。遍历完，结果序列逆序即可
* 后序遍历：每到一个结点，因为根的访问在中间，将A入栈，然后遍历左子树，接着访问A，最后遍历右子树。
## 前序遍历
每到一个结点A就立即访问它。因为每棵子树都先访问其根结点。对结点的左右子树来说，也一定是先访问根。在A的两颗子树中，遍历完左子树后，再遍历右子树。  
因此，在访问完根子树后，遍历左子树前，要将右子树压入栈。
```cpp
vector<int> preorderR(TreeNode* root){
  stack<TreeNode*> S;
  vector<int> v;
  TreeNode* rt = root;
  while(rt || S.size()){
    while(rt){
      S.push(rt->right);
      v.push_back(rt->val);
      rt = rt->left;
    }
    rt = S.top();
    S.pop();
  }
  return v;
}
````
## 后序遍历
1. 每到一个结点A，就立即访问它，然后将左子树压入栈，再遍历右子树。遍历完整棵树后，结果序列逆序即可
````cpp
vector<int> postorderR(TreeNode* root){
  stack<TreeNode*> S;
  vector<int> v;
  TreeNode* rt = root;
  while(rt || S.size()){
    while(rt){
      S.push(rt->left);
      v.push_back(rt->val);
      rt = rt->right;
    }
    rt = S.top();
    S.pop();
  }
  reverse(v.begin(), v.end());
  return v;
}
````
2. 按照左子树-右子树-根的方式。  
每到一个结点A，因为根要最后返回，将其入栈。然后遍历左子树，遍历右子树，最后返回A。  
为了区分是从左子树返回还是从右子树返回。给A结点附加一个标记T。T为true表示从右子树返回，要访问A了；T为false表示A的左子树遍历完，还要遍历右子树。
````cpp
vector<int> postorderR(TreeNode* root) {
  stack<TreeNode*> S;
  unorder_map<TreeNode*, int> done;
  vector<int> v;
  TreeNode* rt = root;
  while(rt || S.size()) {
    while(rt) {
      S.push(rt);
      rt = rt->left;
    }
    while(S.size() && done[S.top()]){
      v.push_back(S.top()->val);
      S.pop();
    }
    if(S.size()){
      rt = S.top()->right;
      done[S.top()] = 1;
    }
  }
  return v;
}
````
## 中序遍历
每到一个结点，因为根的访问在中间，将A入栈，然后遍历左子树，接着访问A，最后遍历右子树。
````cpp
vector<int> inorderR(TreeNode* root) {
  stack<TreeNode*> S;
  vector<int> v;
  TreeNode* rt = root;
  while(rt || S.size()) {
    while(rt) {
      S.push(rt);
      rt = rt->left;
    }
    rt = S.top();
    S.pop();
    v.push_back(rt->val);
    rt = rt->right;
  }
  return rt;
}
  ````

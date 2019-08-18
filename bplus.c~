#include<stdio.h>
#include<stdlib.h>

int rootdiv=0,rootadd=0;

struct node
{
  int key[4];
  struct node *p[5];
  int leaf;
 
};
typedef struct node *node;

node insert_in_parent(node n,int k1,node n1,node root);
node insert_in_leaf(node l,int k,node root);
node insert(int k,node root);
int counting(node x);
node parent(node n,int value,node root);
//node erase(node l);
//node copy_node_key_pointer(node l);
node find(int v,node root);
node getnode();
void print(node root,int n);
void verify(node root);

node getnode()
{
  int i;
  node x;
  x=(node)malloc(sizeof(struct node));
  if(x==NULL)
  {
   printf("out of memory\n");
  }
  else
  for(i=0;i<5;i++)
  {
    x->p[i]=NULL;
  }
  x->leaf=0;
  return x;
}

node find(int v,node root)
{
  int i,count=0,counter=0;
  node prev,cur;
  prev=NULL;
  cur=root;
  if(cur->leaf==0)
  {
    return cur;
  }
label1:
  while(cur->leaf!=0)
  {
     prev=cur;
     cur=cur->p[0];
  }
    if(v<cur->key[0])
       {
          return cur;
       }
     else 
       {
         for(i=0;i<3;i++)
         {
            count+=1;
            if(v>cur->key[i]&&v<cur->key[i+1])
            {
               return cur;
            }
            if(v>cur->key[i]&&cur->key[i]!=0)
            {
               counter+=1;
            }
         }
         if(count==3)
         {
           if(counter==3)
           {
           counter=0;
           return cur;
           }
           count=0;
           counter=0;
           cur=cur->p[4];
           goto label1;
         }
        
       } 
}

node copy_node_key_pointer(node l)
{
 node t;
 int i;
 for(i=0;i<4;i++)
 {
   t->key[i]=l->key[i];
   t->p[i]=l->p[i];
 }
  
}
node erase(node l)
{
  int i;
  for(i=0;i<4;i++)
  {
   if(i>3)
    {
    l->p[i]=NULL;
    }
    l->key[i]=0;
  }
  l->p[5]=NULL;
 return l;
}

node parent(node n,int value,node root)
{
 int k=0,j,i;
 node cur,temp;
 cur =root;
label1:
if(n==root)
{
  return root;
}
 while(k!=1)
 {
   for(i=0;i<5;i++)
   {
    for(j=0;j<4;j++)
    {
      if(cur->p[i]->key[j]==value)
      {
        k=1;
        return cur;
      }
    }
   }
 }

 temp=cur;
 cur=temp->p[0];goto label1;
 cur=temp->p[1];goto label1;
 cur=temp->p[2];goto label1;
 cur=temp->p[3];goto label1;
 cur=temp->p[4];goto label1;
  

}

int counting(node x)
{
  int i,counta=0;
  for(i=0;i<5;i++)
  {
    if(x->p[i]!=NULL)
    {
      counta+=1;
    } 
  }
  return counta;
}
node insert(int k,node root)
{
  int i,count=0,k1;
  node l;
  if(root==NULL)
  {
    l=getnode();
    root=l;
  }
  else
  {
    l=find(k,root);
   
  }
  for(i=0;i<4;i++)
  {
    if(l->key[i]!=0)  //if leaf node has less than 4 values
    {
      count=count+1;
    }
  }
  if(count<4)
  {
   root=insert_in_leaf(l,k,root);
  }
  else  //if leaf node has 4 values then split it
  {
   int a[4];
   node *ap[5];
   node l1;
   l1=getnode();
   //copy_node_key_pointer(l);
   root=insert_in_leaf(l,k,root);
   //a[4]=k;
   l1->p[4]=l->p[4];
   l->p[4]=l1;
   
  
   //l=erase(l);
   
   for(i=0;i<3;i++)
   {
     l1->p[i]=l->p[i+2];
     l1->key[i]=l->key[i+2];
   }
   for(i=2;i<4;i++)
   { 
     l->p[i]=NULL;
     l->key[i]=0;       
   }
   
   k1=l1->key[0];
  
   root=insert_in_parent(l,k1,l1,root);
    if(rootdiv!=1)
   {
     l->leaf=0;
    l1->leaf=0;
   } 
  
 }  
return root;
}

node insert_in_leaf(node l,int k,node root)
{
  int k1,index=0,i;
  node t;
   if(k<l->key[0])
   {
     for(i=0;i<4;i++)
     {
       l->key[i+1]=l->key[i];
       l->key[i]=k;
     }
   }
 
   else
   {
     k1=l->key[0];
     if(k1<k)
     {
       for(i=0;i<4;i++)
       {
         if(k>l->key[i]&&l->key[i]!=0)
         {
           index=i+1;
         }
       }
     }
   //if(root->p[0]!=NULL&&index==4&&rootadd==1)
     //{
      //t->p[0]=root->p[0];
     //}
    l->key[index]=k;
  }
if(root==NULL)
{
  root=l;
}
 //if(root->p[0]!=NULL&&index==4&&rootadd=1)
   // {
   // root->p[0]=t->p[0];
    //}
rootadd=0;
return root;
}

node insert_in_parent(node n,int k1,node n1,node root)
{
  node r,p,p1,temp;
  int pnum,index=0,i,k11,a[4],ppoint=0;
  root->leaf=1;
  if(n==root)
  {
    r=getnode();
    r->p[0]=n;
    r->p[1]=n1;
    r->key[0]=k1;
    r->leaf=1;
    root=r;
    rootadd=1;
    return root;
  }
  else
  {
    p=parent(n,n->key[0],root);
    pnum=counting(p);
      if(pnum<5)
       { 
       for(i=0;i<4;i++)
        {
          if(p->key[i]!=0)
          {
            ppoint+=1;
          }
        }
          p->key[ppoint]=k1;
          for(i=0;i<5;i++)
          {
          if(p->p[i]==n)
            {
             p->p[i+1]=n1;
           }}
       }
       else
       {
          //temp=copy_node_key_pointer(p);
          if(root->key[3]!=0)
          {
            rootadd=1;
          }
         
          root=insert_in_leaf(p,k1,root);
          p1=getnode();
        
          p1->p[4]=p->p[4];
          p->p[4]=p1;
         

          for(i=0;i<2;i++)
          {
            p1->p[i]=p->p[i+3];
            p1->key[i]=p->key[i+3];
          }
          p1->p[2]=n1;
          k11=p->key[2];
          for(i=3;i<4;i++)
          {
            p->p[i]=NULL;
            p->key[i]=0;
          }
        //  for(i=0;i<=2;i++)
         // {
           // p->p[i]=temp->p[i];
           // p->key[i]=temp->key[i];
          //}
          rootdiv=1;
           root=insert_in_parent(p,k11,p1,root);
           
       }
       
 }
 return root;
}
void print(node root,int n)
{
 int i;
 node cur,prev;
 cur=root;
 prev=NULL;
 while(cur->key[0]!=1)
 {
   prev=cur;
   cur=cur->p[0];
 }
// printf("%d",prev->key[0]);

flag:
for(i=0;i<4;i++)
{
  if(cur->key[i]==0&&cur->p[4]!=NULL)
 {
   cur=cur->p[4]; goto flag;
 }
else if(cur->key[i]!=0)
 {
 printf("%d ",cur->key[i]);
 } 
else if(cur->p[4]==NULL)
 {
  printf("\n");
  exit(0);
 }
}
}
void verify(node root)
{
  node cur;
  int value,i,j,k=0,l,m,v1,v2;
  
label5:
 if(root->p[0]!=NULL&&root->leaf!=0)
 {
  value=root->key[0];
  cur=root->p[0];
  for(i=1;i<4;i++)
  { 
    if(cur->key[i]>value)
    {
     printf("Item is greater then parent\n");
     exit(0);
    }
  }

  label3:
  {
   if(k==3) goto label4;
   v1=root->key[k];
   v2=root->key[k+1];
   cur=root->p[k+1];
   for(j=0;j<4;j++)
   {
    if((cur->key[j]<v1&&cur->key[j]!=0)||(cur->key[j]>v2&&v2!=0))
    {
      printf("greater or smaller condition is not satisfied\n");
      exit(0);
    }
   }
   k+=1;
   if(root->p[k+2]!=NULL)
   {
    goto label3;
   }
  }

 label4:
 {
  if(cur->p[4]!=NULL)
  {
   value=cur->key[3];
   cur=cur->p[4];
   for(l=1;l<4;l++)
   { 
     if(cur->key[l]<value)
     {
      printf("Item is lesser then parent\n");
      exit(0);
     }
   }
  }
 }
  
 for(m=0;m<4;m++)
 {
 if(root->p[m]!=NULL)
   {
     root=root->p[m];
   }
  goto label5;
 }
 }
}
void main()
{
  node root;
  int i,a[13]={1,2,3,4,5,6,7,8,9,10,11,12,13},n=13;
  for(i=0;i<n;i++)
  {
   if(i==0)
   {
     root=NULL;
   }
   root=insert(a[i],root); 
   verify(root);
  }
print(root,n);
}

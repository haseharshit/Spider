<details><summary>
	First 4 problems </summary>
<p>

<details><summary>
 Task 1 (A) - </summary>
<p>
Toffee Problem 
Ronny is fond of toffies. He has N rupees, and the shop has M toffies. Each toffee has a price, 𝑖𝑡ℎ toffee has price of 𝐴𝑖 rupees. 
Find the maximum no. of toffees Ronny can buy. If he can't buy anything, print 0.
	</p>
	</details>
	<p> Approach </p>
We will solve this by using greedy approach.
We need to maximize number of toffees ronny can buy(regardless the price of toffees). 
Buying a toffee of $999 or $1 will increase the count by 1 only.
So, we will sort the toffees with there rate (in non dec order), and buy as much as Ronny Can from the amount he have.
We will use inbuilt sort( O(nlogn) complexity) . (Since we N<10^5).
Therefore there will not be any TLE.
If N would have been larger (say 10^8). Then we could have used Countsort ( since Ai <10^7) 
Code:

```
 int main() {
     int n, k;
     cin>>n>>k;
     int a[n];
     for(int i=0; i<n; i++)  cin>>a[i];
     sort(a, a+n);
     int i=0;
     while(i<n && k>=a[i]){
         k-=a[i];
         i++;

     }
     cout<<i<<endl;
     return 0;
 }
```













<details><summary>
	Task 2</summary>
	<p>
Button Factory 
Alice and Bob are in a factory and have a button each that does nothing. They are looking over a machine and get bored so they start playing with the buttons.
Alice presses the button P seconds after the machine starts and releases it after Q seconds. Bob presses the button R seconds after the machine starts and releases it after S seconds.
You have to determine for how many seconds both Alice and Bob had pressed the button together.
	</p>
	</details>

Alice [a,b],
Bob[ c,d]
Now we want intersection of Alice and Bob, 
L(lower bound) =max(a,c) 
U(upper bound) =min(b,d)
Intersection will exist if (L<U)  
since according to question, if alice [1,2], and bob[2,3], then anser is 0. 
therefor no equal sign
If intersection Exists, output U-L
Else output, 0
Code:

```
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */  
    int a, b, c, d;
    cin>>a>>b>>c>>d;
    int l=max(a, c), u=min(b, d);
    if(l<u)
        cout<<u-l<<endl;
    else
        cout<<0<<endl;
    return 0;
}

```


<details><summary>
	Task 3(Lazy Lads)</summary>
	<p>
Paras was procrastinating to take personal interviews for Algos inductions. He tried to avoid the task as much as he can. Eventually, Simran and Yasser got angry and decided to punish him.
They locked him in a big dungeon which had q rooms with N j boxes inside j th room ( 1 <= j <= q ). They told him to stack those boxes in the shape of rows starting from 1 st row. The i th row was supposed to have exactly i boxes. But Yasser forgot to count the number of boxes. As a remedy Simran told Paras he can leave the last row incomplete (but it could be complete as well).
Paras, somehow sneaked his laptop inside, decided to take your personal interview there. He counted the number of boxes and asked you how many number of complete rows will he be able to build from those boxes in each room.
	</p>
	</details>
<p> Approach </p>

if n rows would have been completely filled. Number of boxes required for that would be x= n*(n+1)/2. But we have given number of boxes( i.e x,) and we have to find number complete rows
	n*(n+1)/2 <=x  (n should be natural number.)
	n^2+n-2x<=0 ( since x>=1, therefore one root would be +ve and one would be negative)

	we want +ve n, and that would be (-1+sqrt(1+8*x))/2 (     Floor value implicit typecast to int)

now since x is given with constraints 2^31-1, therefore 8*x part may result in overflow (since upper bound of int is 2^31-1). To overcome that, we have used Long long int.



Code:
```
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int n;
    cin>>n;
    ll a[n];
    for(int i=0; i<n; i++)  cin>>a[i];
    //int limit=2147483648;
    
    for(int i=0; i<n; i++){
        int k=(sqrt(1+8*a[i])-1)/2;
        cout<<k<<endl;
    }
    return 0;
}

```




<details><summary>
	Task 4</summary>
	<p>
Harsh is interested in prime numbers. He used to play Primeman game. According to the rules of Primeman, every even integer greater than 2 can be expressed as the sum of two primes. Harsh finds this game interesting and he decides to design a game of his own and call it ‘HarshPrime’. Since Harsh is a philomath, HarshPrime rules states that at least x prime numbers from 2 to n inclusively can be expressed as the sum of three integer numbers: two neighbouring prime numbers and 1. For example, 31 = 1 + 13 + 17.
Two prime numbers are called neighbouring if there are no other prime numbers between them. Harsh is busy with his project so you have to help him, and find out if he is right or wrong.
	</p>
	</details>

Approach:
finding the prime using Sieve of Eratosthenes.and pushing prime numbers in a vector .
This question can be reframed as if sum two prime number +1 is also a prime.
We will check this by iterating over that vector.
Also, at the end we want to find number number of Harshprime within 2, n (lower bound is fixed). Therefore we will maintain a count which will give us the number of Harshprime.
To Reduce SpaceComplexity, Can use prime[1001] array itself instead of considering another array of same size(ans).
 
For given value of n (if >12)
We will look for the non zero value at  kth index ( k<=n)
And if k >=x Yes
else No
![alt text](/t4.png?raw=true "Title")

Code:
```
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int prime[1001]={0}, ans[1001]={0};
    vector<int>p;
    for(int i=2; i<1001; i++){
        if(prime[i]==0){
            p.push_back(i);
            for(int j=i+i; j<1001; j+=i)
                prime[j]=1;
        }
    }
    int k=0, n=p.size();
    for(int i=1; i<n; i++){
        int x=p[i]+p[i-1]+1;
        if(x>1000)
            break;
        if(prime[x]==0){
            k++;
            ans[x]=k;
        }
    }
    int a, b;
    cin>>a>>b;
    if(a<13){
        if(b)
            cout<<"NO\n";
        else
            cout<<"YES\n";
    }
    else{
        while(a>10 && ans[a]==0){
            a--;
        }
        if(ans[a]>=b){
            cout<<"YES\n";
        }
        else
            cout<<"NO\n";
    }
    return 0;
}
```
	
</p>
</details>
	

<details><summary>
	Last 4 problems </summary>
	
<p>
	<details><summary>
Weird Letter - </summary>
<p>
Simran received a letter from his friend Yasser. However, Yasser's keyboard is broken, so pressing a key on it once may cause the corresponding symbol to appear more than once.

For example, as a result of typing the word "greetings", the following words could be printed: "grreetingssss", "greeetings”, “ggrreettiiinggs", but the following could not be printed: "greeting", "geeting".

Note, that when you press a key, the corresponding symbol must appear (possibly, more than once). The keyboard is broken in a random manner, it means that pressing the same key you can get the different number of letters in the result.

For each word in the letter, Simran has guessed what word Yasser actually wanted to write, but she is not sure about it, so she asks you to help her. Give her an assurance whether she has interpreted the message correctly or not.

You are given a list of pairs of words. For each pair, determine if the second word could be printed by typing the first one on Yasser's keyboard.
	</p>
	</details>
	<p> Approach </p>
Here, I am iterating through booth string and if I find character same, then I will count the occurence of that character for both string..
(say c1 and c2. Thereafter, I will compare if c1>c2 (return false)else continue). And if character is not same. return false.
At the end, if any of the iterator haven't reach at the end. Return FALSE;
else TRUE;
CODE:
```
	int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int t;
    cin>>t;
    while(t--){
        string s1, s2;
        cin>>s1>>s2;
        int i=0, n1=s1.length(),j=0, n2=s2.length(), ans=1;
        char ch;
        while(i<n1 && j<n2){
            if(s1[i]==s2[j]){
                ch=s1[i];
                int c1=0,c2=0;
                while(i<n1 && s1[i]==ch){
                    c1++;
                    i++;
                }
                while(j<n2 && s2[j]==ch){
                    c2++;
                    j++;
                }
            //    cout<<i<<" "<<j<<endl;
                if(c1>c2){
                    ans=0;
                    break;
                }
                    
            }
            else
            {
                ans=0;
                break;
            }
        }
        if(j!=n2 || i!=n1)
            ans=0;
        cout<< (ans?"YES\n":"NO\n");
        
    }
    return 0;
}
```


<details><summary>
Simran the Prankster- </summary>
<p>
Simran asked Paras to do a very weird task. She gave him a list of numbers and asked him to use a calculator to apply arithmetic operations on the numbers to obtain some value X. Simran knows how tedious it would be to keep trying all the combinations so she might play a prank with Paras and give him such a X that can't be obtained using the list and the 4 arithmetic operations. Paras knows Simran might do this and he does not want to keep trying out all the possible combinations and end up finding out that he was pranked. So Paras would only do the task if it is possible to obtain X.

Given an array of n integers and an integer X, without changing the order of the elements in the array insert arithmetic operations between the elements and find out if it is possible to obtain X.

E.g.: n = 3, nums[3] = {1, 2, 3}, X = 5. Since 1 * 2 + 3 = 5, hence the answer is YES.

Keep in mind Paras would use a calculator so the operators would be directly computed from left to right and won't follow BODMAS (1 + 2 * 3 will evaluate to 9 not 7).
	</p>
	</details>
	<p> Approach </p>
Since, n<13 => number of operations=12, I have tried using recursion with time complexity( 4^n), but since n is pretty small. Therefore NO TLE.
Things that I took care: Floating point error ( deviding by 0). Taking datatype Double instead of int. etc

CODE:
```
	bool helper(double a[], int i, int n,double k, double res){
    //cout<<k<<" "<<res<<endl;
    if(i==n)
        return k==res;
    if(a[i]==0)
        return helper(a, i+1, n, k*a[i], res) ||  helper(a, i+1, n, k-a[i], res) || helper(a, i+1, n, k+a[i], res);
    return helper(a, i+1, n, k*a[i], res) || helper(a, i+1, n, k/a[i], res) || helper(a, i+1, n, k-a[i], res) || helper(a, i+1, n, k+a[i], res);
}
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int t;
    cin>>t;
    while(t--){
        int n;
        double res;
        cin>>n>>res;
        double a[n];
        if(n==0){
            cout<<"NO\n";
            continue;
        }
        if(n==1){
            cin>>n;
            if(n==res)
                cout<<"YES\n";
            else
                cout<<"NO\n";
            continue;
        }
        for(int i=0; i<n; i++)
            cin>>a[i];
        
        if(helper(a, 1, n, a[0], res))
            cout<<"YES\n";
        else
            cout<<"NO\n";
    }
    return 0;
}
```
	
<details><summary>
Catch The Psycopath!- </summary>
<p>
Treecity is a very unique place. The man who established the city loved binary trees and had the city designed like a binary tree. The city starts at the mayor's residence and each house has at-most 2 houses directly connected to it by 2 roads, 1 going left and 1 going right.

Everything was very peaceful in Treecity until a psycopath named Ed came along. Ed has been continuously committing very serious crimes and the police department is unable to catch him. He decides to play a game with them. He sends a note to the police stating that he is going to abduct exactly m kids from Treecity starting from the mayor's residence and ending at one of the houses that are the last on that route.

You decide to catch him this time and lock him up for good.

You are given an integer m and the number of children living in each house in Treecity. Find all the possible routes Ed could take to complete his psycopathic mission and stop him!
	</p>
	</details>
	<p> Approach </p>
I have created a binary tree with two data fields, node->val and node->sum(Which stores the sum from top till this node). And made a tree. Inorder Function takes Node as and argument, and if that node->sum==TARGEt && that node is LEAF NODE. It will print its ansistory.(Stored in vector).
CODE:
```
	class node{
    public:
    node *left, *right;
    int val,sum;
    node(int x){
        left=NULL;
        right=NULL;
        val=x;
        sum=x;
    }
};
//void insert()
void printInorder( node* nod, int target, vector<int> curr)
{
    if(nod==NULL)
        return;
    if (nod->left == NULL && nod->right==NULL){
        if(nod->sum==target){
            curr.push_back(nod->val);
            for(auto i : curr){
                cout << i << " ";
            }
            cout << "\n";
            return;
        }
    }
  //  vector< vector<int>> l,r;
    curr.push_back(nod->val);
    if(nod->sum > target)
        return;
    if(nod->left){
        printInorder(nod->left, target, curr);
    }
    if(nod->right){
        printInorder(nod->right,target, curr);
    }
}
 
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int n,x;
    cin>>n;
    if(n==0)
        return 0;
    cin>>x;
    class node * root= new node(x);
    class node *temp=root;
    queue < node*> q;
    q.push(temp);
    n--;
    while(n){
       // cout<<"n="<<n<<endl;
        node *k=q.front();
       // cout<<"Baap, "<<k->val<<endl;
        q.pop();
        cin>>x;
        if(x!=-1){
            n--;
            node *n1= new node(x);
            n1->sum+=k->sum;
            k->left=n1;
            q.push(n1);
        }
        if(n!=0){
            cin>>x;
            if(x!=-1){
                n--;
                node *n1= new node(x);
                n1->sum+=k->sum;
                k->right=n1;
                q.push(n1);
            }
        }
        
    }
    cin>>x;
    while(x==-1)
        cin>>x;
    printInorder(root, x, {});
    // for (int i = 0; i < ans.size(); i++){
    //     for (int j = ans[i].size()-1; j >= 0; j--)
    //     {
    //         cout << ans[i][j] << " ";
    //     }
    //     cout << "\n";
    // }
        return 0;
}

```
	
<details><summary>
Fractalato!- </summary>
<p>
Manish decided to work on his dream of owning a potato chips company. With his team he developed a Fractalato Chip (fractal + potato), which was a miracle. The chip looks like an equilateral triangle pointed upwards. After one second, this triangular piece broke down in 4 triangular pieces, 3 pointed upward and 1 downward. After another second, each triangular piece broke down into 3 pieces pointed in the same direction as the parent piece and one in opposite direction of the parent pieces. The image describes the breaking process.

image

Suddenly Mansih got curious and wondered about the pieces. Help Manish find the number of pieces that are pointed upward at the end of n seconds.
	</p>
	</details>
	<p> Approach </p>
for n=1, it is 3 ( sum till 2^1), for n=2, ans is 10 (sum till 2^2 i.e 4). But the interesting part is the modulo, we have to keep MODING OPERANDS so that overflow will not occur.
	
CODE:
```
ll binpow( long long b) {
    ll a=2;
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a % mod;
        a = a * a % mod;
        b >>= 1;
    }
    return res;
}
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    ll n;
    cin>>n;
   // ll  ans=0;
    //ll t=1,x=1;
    //ans = (2^n)*(2^n+1)/2 using mod algo.
    ll ans=binpow(n);
    ans=(ans*(ans+1)/2)%mod;
    cout<<ans<<endl;
    return 0;
}
```
	
	
	
</p>
</summary>
	

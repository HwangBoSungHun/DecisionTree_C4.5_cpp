# Decision Tree(C4.5)
인공지능 동아리 ‘ICU’에서 Decision tree(C4.5)를 바닥부터 짜보는 활동함(2017. 10 ~ 2018. 01)

## Code 설명  
__main.cpp__  
data set을 받아들여 실행하는 부분.  

__csvTovector.cpp__  
~~~
vector<vector<float> > ConvertToVector(char file1[], char file2[])  
~~~
csv파일을 읽고 vector<vector<float>>의 형태로 return 한다.  

__C45.cpp__  
~~~
typedef struct Node  
{  
    vector<vector<float>> vWine;  
    int nAttr; //몇번째 attribute인지 저장.  
    float fAttribute_value;
    int nNumOfRed; //red wine의 갯수 저장.
    int nNumOfWhite; //white wine의 갯수 저장.
    float fProbablityOfRed; //red일 확률 저장.
    float fProbablityOfWhite; //white일 확률 저장.
    
    int nOutcome; //red 갯수가 많으면 1, white 갯수가 많으면 2 저장. 이것을 			통해 test이 들어왔을 때 red인지 white인지 결정.
    
    struct Node *pLeft;
    struct Node *pRight;
}Node;
Node* c45(vector<vector<float>> vWine) //실제 c4.5 구현.
void initNode(Node* pNode) //node 초기화
~~~
__IGCalculator.cpp__
typedef struct IG_Info
{
    float fAttr_value;
    double dIG_value;
}IG_Info;

//한가지에 대해서만 엔트로피를 구할 때 사용하는 function.
double Entropy1(float arr[], int nSize) 
//두가지 요소 간에 엔트로피를 구할 때 사용하는 function.
double Entropy2(vector<float> const& arr1, float arr2[], int nSize)

//information gain을 구하는 function.
double IG(double dEnt1, double dEnt2)

//(Sorting 하지 않음) 한 attribute에 대한 column이 들어왔을 때, 그 column을 기준으로 모든 value의 IG을 구해서 IG이 가장 큰 것의 정보를 저장.
IG_Info MaxIG_Info(float fRorW[], float fAttr[], int nSize)



__traversal.cpp__
//preorder traversal 이용해서 tree 확인.
void preorder_traversal(Node* pRoot);

//data set으로 들어간 wine을 분석하여 red 와인인지 white 와인인지 예측하고, 실제 값(실제로 red 와인인지 white인지)과 비교하여 accuracy를 return 함.
int accuracyCalc(Node* pRoot, vector<vector<float> > vWine);


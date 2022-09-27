## 순차검색 알고리즘(sequential search)
- 문제: 크기가 n인 배열s에 x가 있는가?
- 알고리즘: x와 같은 원소를 찾을 때까지 s에 있는 모든 원소를 차례대로 검사, 만일 x와 같은 원소를 찾으면 그 위치 반환
```
void seqsearch(int n, const keytype x, index& location){
    location = 1;
    while(location <= n && S[location] != x) #로케이션이 배열의 크기보다 작으면, x를 찾지 못했다면 반복
        location++
    if (location > n) #현 위치가 범위보다 커지면 x를 찾지못함. 0반환
    location = 0;
}
```
- 최악의 경우:n #배열의 마지막 아이템이거나, x가 배열에 없는 경우
- 평균의 경우 (#배열의 아이템이 모두 다르다고 가정):
        - x가 배열 s안에 있는 경우만 고려: n+1/2 
        - x가 배열 s안에 없는 경우 고려: n(1-p/2)+p/2
- 최선의 경우 : 1


- while 문을 수행할 때마다 검색 대상의 크기가 1/2씩 감소하기 떄문에 최악의 경우라도 logn + 1개 검사

### 순차검색 vs 이분검색
- 이분검색이 훨씬 크기가 작아짐

## 배열에 있는 원소 덧셈
- 문제: 크기가 n인 배열s에 있는 모든 수를 더하여라
```
number sum(int n, const number s[]){
    index i;
    number result;
    result = 0;
    for(i=1;i<=n;i++)
        result = result + s[i]
    return result
}
```
- 배열에 있는 원소의 덧셈
    - 단위연산 덧셈: 총 수행 횟수 T(n) = 2n
    - 단위연산 지정문: 총 수행 횟수 T(n) = 2n + 2

## 교환정렬
- 문제: 비내림차순으로 n개의 키를 정렬
```
void exchangesort(int n, keytype s[]){
    index i,j;
    for(i=1;i<=n-1;i++){
        for(j=i+1;j<=n;j++){
            if(s[j]<s[i]){
                exchange s[i] and s[j]
            }
        }
    }
}
```
- 단위연산: 조건문
    - T(n) = n(n-1)/2
- 단위연산: 교환하는 연산
    - 최악의 경우
        - 항상 조건문이 참이 되는 경우
        - 입력배열이 거꾸로 정렬된 경우: n(n-1)/2
    - 최선의 경우
        - 항상 조건문이 거짓이 되는 경우
        - 배열이 이미 정렬된 경우: c(상수)
        
## Divide&Conquer
- T(n):
    - g(n)
    - f(n) + 2T(n/2)
```
procedure D&C(p,q)
int n,A(1:n);
int m,q,p; #1<=p<=q<=n
if small(p,q) then return(G(p,q))
else{
    m:divide(p,q)
    return conbine(D&C(p,m),D&C(m+1,q))
}
```

## 이분 검색 알고리즘 (Binary search)
- 문제: 크기가 n인 <b>정렬된</b> 배열s에 x가 있는가?
- recursive 알고리즘
- O(logn)
```
index binsearch(index low, index high){
    index low,high,mid;
    low = 1; high = n;
    location = 0;
    while(low<=high&&location==0){
        mid = (low+high)/2
        if(x==s[mid])
            location = mid
        else if (x<s[mid])
            return binsearch(low,mid-1)
        else 
            return binsearch(mid+1, high)
    }
}
```

- iterative 알고리즘
- O(logn)
```
void binsearch(int n, const keytype s[], keytype x, index& location){
    index low,high,mid;
    low = 1; high = n;
    location = 0;
    while(low<=high&&location==0){
        mid = (low+high)/2
        if(x==s[mid])
            location = mid
        else if (x<s[mid])
            high = mid - 1
        else 
            low = mid + 1
    }
}
```
# 정렬 알고리즘
    - 평균적으로 O(n^2) 시간 소요 알고리즘
        - 선택정렬
        - 버블정렬
        - 삽입정렬
    - 평균적으로 O(nlogn) 시간 소요 알고리즘
        - 합병정렬
        - 퀵정렬
        - 힙정렬

## 합병정렬
- 문제: n개의 정수를 비내림차순으로 정렬
- 전략: 
    1. 배열 반으로 나누기
    2. 배열 정렬
    3. 베열 conbine하기
```
void merge(int h, int m, const keytype U[], keytype V[], const keytype S[]){
    index = 1,j=1,k=1
    while(i<=h && j<=m){
        if(U[i]<V[j]>){
            S[k] = U[i];
            i++
            }
        else{
            S[k] = V[j]
            j++
            }
        }
        k++
    }
    if(i>h)
        copy V[j] through V[m] to S[k] through S[h+m]
    else
        copy U[i] through U[h] to S[k] through S[h+m]
}

void mergesort(int n, keytype S[]){
    const int h = n/2, m = n-h
    keytypeU[1..h], V[1..m];

    if(n>1){
        copy S[1] through S[h] to U[1] through U[h]
        copy S[h+1] through S[n] to V[1] through V[m]
        mergesort(h,U);
        mergesort(m,V);
        merge(h,m,U,V,S);
    }
}
```
- 최악의 경우
    - U[i ]와 V[j ]의 비교연산
        - 합병하는 시간 복잡도: O(n)
    - merge에서 발생하는 비교연산
        - O(logn)
    - 공간 복잡도
        - 2n

## 퀵정렬
- n개의 정수를 비내림차순으로 정렬
```
void quicksort(index p, index q){
    if(p<q){
        j=q+1
        quicksort(p,j-1)
        quicksort(j+1,q)
    }
}

procedure partition(p,j)

```
- 최악의 경우: O(n^2)
- 평균의 경우: O(nlogn)

### mergesort vs quicksort
- mergesort:
    - 반씩 균등하게 나눔
    - 독립적으로 분배
    - 끝에 merge
- quicksort
    - 딱 중간으로 못 나눌 수 있음
    - 독립적으로 분배
    - merge안해도 됨
    
## selection
- 문제: k번째 작은 원소를 찾는 문제
- 알고리즘
    1. 숫자 데이터들을 오름차순 정렬 후 k번째 원소 찾기 -> O(n)
    2. n 개의 데이터들 중에서 가장 작은 최소의 숫자를 k번을 찾음 -> O(kn)
    3. partition algorithm
```
procedure select(A,n,k){
    #A(n+1) = 무한
    p = 1
    q = n+1
    A(n+1) = +무한

    Loop
        j = q;
        partition(p,j);
        clse
            k=j: return A(j);
            k<j:q=j;
            k>j:j+1;
    repeat
}
```
- 최악의 경우 O(n^2)
- 보통: O(n)

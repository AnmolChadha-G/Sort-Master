#include<stdio.h>
#include<stdlib.h>
struct list{
    float data;
    struct list *next;
};
    void bubblesort(int *a,int n)
{
    for(int i=0;i<n;i++)
    {
        for(int j=1;j<n-i;j++)
        {
            if(a[j]<a[j-1])
            {
                int temp=a[j];
                a[j]=a[j-1];
                a[j-1]=temp;
            }
        }
        for(int i=0;i<n;i++)
    	{
        	printf("%d ",a[i]);
    	}
    	printf("\n");
    }
}
    void bubblesort2(float *a,int n)
{
    for(int i=0;i<n;i++)
    {
        for(int j=1;j<n-i;j++)
        {
            if(a[j]<a[j-1])
            {
                float temp=a[j];
                a[j]=a[j-1];
                a[j-1]=temp;
            }
        }
    }
}
struct list* newnode(float val)
{
    struct list *temp=(struct list*)malloc(sizeof(struct list));
    temp->data=val;
    temp->next=NULL;
    return temp;
}
void insert(struct list* *head,float val)
{
    struct list *temp=newnode(val);
    if(*(head)==NULL)
    {
        *(head)=temp;
    }
    else
    {
        temp->next=*(head);
        *(head)=temp;
    }
}
void printlist(struct list *head)
{
    struct list *temp=head;
    while(temp!=NULL)
    {
        printf("%f ",temp->data);
        temp=temp->next;
    }
}
void sort(struct list* *head)
{
    struct list *temp=*head;
    int n=0;
    while(temp->next!=NULL)
    {
        n+=1; 
        temp=temp->next;
    }
    temp=*head;
    float a[n];
    for(int i=0;i<n;i++)
    {
        a[i]=temp->data;
        temp=temp->next;
    }
    bubblesort2(a,n);
    temp=*head;
    for(int i=0;i<n;i++)
    {
        temp->data=a[i];
        temp=temp->next;
    }
    
}
void countsort(int *a,int n,int j)
{
    int c[10];
    for(int i=0;i<10;i++)
    {
        c[i]=0;
    }
    for(int i=0;i<n;i++)
    {
        c[(a[i]/j)%10]+=1;
    }
    for(int i=1;i<10;i++)
    {
        c[i]=c[i]+c[i-1];
    }
    int b[n];
    for(int i=n-1;i>=0;i--)
    {
        b[c[(a[i]/j)%10]-1]=a[i];
        c[(a[i]/j)%10]--;

    }
    for(int i=0;i<n;i++)
    {
        a[i]=b[i];
    }
}
void radixsort(int *a,int n)
{
    int p=a[0];
    for(int i=0;i<n;i++)
    {
        if(p<a[i])
        {
            p=a[i];
        }
    }
    for(int i=1;p/i>0;i*=10)
    {
        countsort(a,n,i);
        for(int i=0;i<n;i++)
    	{
        	printf("%d ",a[i]);
    	}
    	printf("\n");
    }
}
void maxheapify(int *a,int n,int i)
{
    int l=2*i+1;
    int r=2*i+2;
    int largest=i;
    if(l<n&&a[largest]<a[l])
    {
        largest=l;
    }
    if(r<n&&a[largest]<a[r])
    {
        largest=r;
    }
    if(largest!=i)
    {
        int temp;
        temp=a[largest];
        a[largest]=a[i];
        a[i]=temp;
        maxheapify(a,n,largest);
    }

}
void heapsort(int *a,int n)
{
    while(n>1){
        int temp;
        temp=a[0];
        a[0]=a[n-1];
        a[n-1]=temp;
        n--;
        maxheapify(a,n,0);
        for(int i=0;i<n;i++)
    	{
        	printf("%d ",a[i]);
    	}
    	printf("\n");
    }
}
void countingsort(int *a,int n)
{
     int k;
    k=a[0];
    for(int i=0;i<n;i++){
        if(a[i]>k){
            k=a[i];
        }
    }
    
    int c[k+1];
    for(int i=0;i<k+1;i++)
    {
        c[i]=0;
    }
    for(int i=0;i<n;i++)
    {
        c[a[i]]+=1;
    }
    for(int i=1;i<k+1;i++)
    {
        c[i]=c[i]+c[i-1];
    }
    int b[n];
    for(int i=n-1;i>=0;i--)
    {
        b[c[a[i]]]=a[i];
    }
    for(int i=1;i<=n;i++)
    {
        printf("%d ",b[i]);
    }

}
void selectionsort(int *a,int n)
{
	int i;
	int j;
	for(i=0;i<n-1;i++)
	{
		  int p=i;
		  for(j=i+1;j<n;j++)
			  {
			  if(a[p]>a[j])
			  {
			  	p=j;
			  }
		  }
		  int temp;
		  temp=a[i];
		  a[i]=a[p];
		  a[p]=temp;
		  for(int i=0;i<n;i++)
		 {
			printf("%d ",a[i]);
		 }
		 printf("\n");
	 }
 }
void merge(int *a,int n,int p,int q,int r){
    int n1=q-p+1;
    int n2=r-q;
    int l[n1];
    int s[n2];
    int k=0;
    for(int i=0;i<n1;i++)
    {
        l[i]=a[i+p];
    
    }
    for(int i=0;i<n2;i++){
        s[i]=a[q+i+1];
    }
    int i=0;
    int j=0;
    k=p;
    while(i<n1&&j<n2)
    {
        if(l[i]<s[j]){
            a[k]=l[i];
            i++;
            k++;
        }
        else
        {
            a[k]=s[j];
            j++;
            k++;
        }
    }
    while(i<n1){
        a[k]=l[i];
        i++;
        k++;

    }
    while(j<n2)
    {
        a[k]=s[j];
        j++;
        k++;
    }

}
void mergesort(int *a,int n,int p,int r){
    int q;
    if(p<r){
    	for(int i=0;i<n;i++)
    	{
        	printf("%d ",a[i]);
    	}
    	printf("\n");
        q=p+((r-p)/2);
        mergesort(a,n,p,q);
        mergesort(a,n,q+1,r);
        merge(a,n,p,q,r);
    }
}
int partition1(int *a,int n,int p,int r)
{
    int x=a[r];
    int i=p-1;
    int j=p;
    for(j=p;j<r-1;j++)
    {
        if(a[j]<=x)
        {
            i++;
            int temp;
            temp=a[i];
            a[i]=a[j];
            a[j]=temp;
        }
    }
    i++;
    int temp;
    temp=a[i];
    a[i]=a[r];
    a[r]=temp;
    return i;
}
void quicksort1(int *a,int n,int p,int r)
{
    if(p<r){
        int q=partition1(a,n,p,r);
        quicksort1(a,n,p,q-1);
        quicksort1(a,n,q+1,r);
    }
}
int partition2(int *a,int n,int p,int r)
{
    int x=a[p];
    int i=r+1;
    int j=r;
    for(j=r;j>p;j--){
        if(a[j]>=x)
        {
            i--;
            int temp=a[i];
            a[i]=a[j];
            a[j]=temp;
        }
    }
    i--;
    int temp=a[p];
    a[p]=a[i];
    a[i]=temp;
    return i;
}
int partition(int *a,int n,int p,int r)
{
	int i,j,x,temp;
	i=-1;
	x=a[r];
	for(j=0;j<=r-1;j++)
	{
		if(a[j]<=x)
		{
		 i++;
		 temp=a[j];
		 a[j]=a[i];
		 a[i]=temp; 
		}
	}
	i++;
	temp=a[r];
	a[r]=a[i];
	a[i]=temp;
	return i;
}
void quicksort(int *a,int n,int p,int r)
{
	int q,i;
	if(p<r)
	{
		for(i=0;i<n;i++)
		{
			printf("%d ",a[i]);
		}
		printf("\n");
		q=partition(a,n,p,r);
		quicksort(a,n,p,q-1);
		quicksort(a,n,q+1,r);
	}
}
void quicksort2(int *a,int n,int p,int r)
{
    int q;
    if(p<r)
    {
    	for(int i=0;i<n;i++)
    	{
        	printf("%d ",a[i]);
    	}
    	printf("\n");
        q=partition2(a,n,p,r);
        quicksort2(a,n,p,q-1);
        quicksort2(a,n,q+1,r);
    }
}
void quicksort_random(int *a,int n,int p,int r,int j)
{
    int q;
    if(p<r)
    {
    	for(int i=0;i<n;i++)
    	{
        	printf("%d ",a[i]);
    	}
    	printf("\n");
        q=partition2(a,n,p,r);
        quicksort_random(a,n,p,q-1,j);
        quicksort_random(a,n,q+1,r,j);
    }
}
void insertionsort(int *a,int n)
{
	int i;
	int j;
	for(j=0;j<n;j++)
	{
		int key=a[j];
		i=j-1;
		while(i>=0&&a[i]>key)
		{
			a[i+1]=a[i];
			i--;
		}

		a[i+1]=key;
		for(int i=0;i<n;i++)
		{
			printf("%d ",a[i]);
		}
			printf("\n");
	}
}

int main()
{
		FILE *fp;
	fp=fopen("file.txt","r");
	int n;
	fscanf(fp,"%d",&n);
	int *a;
	a=(int*)malloc(n*sizeof(int));
	for(int i=0;i<n;i++)
	{
	fscanf(fp,"%d",&a[i]);
	}
	fclose(fp);
    printf("choose the sorting algorithm-:\n");
    printf("1-bubble sort\n2-selection sort\n3-insertion sort\n4-merge sort\n5-quick sort_last_pivot\n6-quick sort_first_pivot\n7-radix sort\n8-bucket sort\n9-counting sort\n10-heap sort\n11-quicksort_random\n");
    int choice;
    scanf("%d",&choice);
    switch(choice){
        case 1: {
            bubblesort(a,n);
            break;
        }
        case 2: {
            selectionsort(a,n);
            break;
        }
        case 3: {
            insertionsort(a,n);
            break;
        }
        case 4: {
            mergesort(a,n,0,n-1);
            break;
        }
        case 5: {
            quicksort(a,n,0,n-1);
            break;
        }
        case 6: {
            quicksort2(a,n,0,n-1);
            break;
        }
        case 7: {
            radixsort(a,n);
            break;
        }
        case 8: {
            struct list *head[10];
            for(int i=0;i<10;i++)
            {
                head[i]=NULL;
            }
            int n=5;
            //here we use bucket sort to sort the decimal numbers using linkist as we are not using file.txt hence direct input given
            float a[5]={0.28,0.21,0.36,0.11,0.54};
            for(int i=0;i<n;i++)
            {
                float m;
                m=a[i];
                int p=m*10;
                insert(&head[p],m);

            }
            for(int i=0;i<10;i++)
            {   
            if(*head!=NULL&&(*head)->next!=NULL)
            {
                 sort(&head[i]);
            }
                printlist(head[i]);
            }
            return 0;
        }
        case 9: {
            countingsort(a,n);
            return 0;
        }
        case 10: {
            for(int i=n/2;i>=0;i--)
        {
            maxheapify(a,n,i);
        }
            heapsort(a,n);
            break;
        }
        case 11: {
            printf("enter the index to be pivoted");
            int j;
            scanf("%d",&j);
            if(j>=9)
            {
				printf("index out of limit\n");
			}
			int temp;
			temp=a[0];
			a[0]=a[j];
			a[j]=temp;
        	quicksort_random(a,n,0,n-1,j);
        }
        
    }
    for(int i=0;i<n;i++)
    {
        printf("%d ",a[i]);
    }
    return 0;
}

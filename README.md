# binary-tree
this is a binary tree which can insert a new node, delete a node, search a node, search in postorder and inorder via Linked List in C

#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>

struct node{
	int data;
	node* left;
	node* right;
}; // for storing nodes.

typedef node Node;
typedef node* nodePtr;

void Insert(nodePtr startPtr);
void Search(nodePtr startPtr);
void Delete(nodePtr startPtr);
void Inorder(nodePtr startPtr);
void Postorder(nodePtr startPtr);

int main(void){
	int opt=0;
	nodePtr startPtr=NULL;

	do{
		printf("1.) Insert   2.) Search   3.) Delete   4.) Inorder   5.) Postorder   -1.)\nOption:");
		scanf("%d", &opt);
		if(opt!=-1){
			if(opt==1){
				Insert(startPtr);
			}
			else if(opt==2){
				Search(startPtr);
			}
			else if(opt==3){
				Delete(startPtr);
			}
			else if(opt==4){
				Inorder(startPtr);
			}
			else if(opt==5){
				Postorder(startPtr);
			}
			else{
				printf("Wrong input!\n");
			}
		}// end if(opt!=-1)
	}while(opt!=-1);

	system("pause");
	return 0;
}

void Insert(Node* startPtr){
	nodePtr currentPtr=NULL;
	nodePtr root=NULL;
	nodePtr previousPtr=NULL; // 接上一個地址currentPtr.
	int num;

	do{
		// 給使用者輸入數字，-1結束程式
		printf("Please enter a number(-1 to end the function):");
		scanf("%d", &num);

		// 每新增一個節點，先把值存入，之後比大小，再決定放右邊或左邊。
		if(num!=-1){
			nodePtr newNode=(nodePtr)malloc(sizeof(Node));
			newNode->data=num; // 每新增一個節點，先把值存入

			// 判斷是否為第一個，是則存入root，否則比大小。
			if(startPtr==NULL){
				startPtr=newNode;
				startPtr->left=NULL;
				startPtr->right=NULL;
				// 確認根(root)是否有地址。
				printf("%p\n", startPtr);
			}
			// 比大小，再決定放右邊(大的)或左邊(小的)。
			else{
				// 用currentPtr去接startPtr(root)，以while迴圈尋找可插入的點，這樣startPtr(root)才不會變動。
				currentPtr=startPtr; //  每一次都從root去找。
				while(currentPtr!=NULL){
					// 輸入的值<比對到的值，且未到最後一個節點，往左並繼續往下比較。
					if(newNode->data<currentPtr->data){
						previousPtr=currentPtr;
						currentPtr=currentPtr->left;
					}
					// 輸入的值>比對到的值，且未到最後一個節點，往右並繼續往下比較。
					else if(newNode->data>currentPtr->data){
						previousPtr=currentPtr;
						currentPtr=currentPtr->right;
					}
					// 輸入的值=比對到的值，提醒使用者。
					else if(newNode->data==currentPtr->data){
						printf("值重複出現!\n");
						break;
					}
				}// end while.
				// 找到最後一個節點，決定要放左邊還右邊。
				if(currentPtr==NULL){
					// 輸入的值<比對到的值，放入比對到的值之左下方。
					// 因為此時currentPtr以至結尾，故用previousPtr去比大小。
					if(newNode->data<previousPtr->data){
						previousPtr->left=newNode;
						previousPtr->right=NULL;
					}
					// 輸入的值>比對到的值，放入比對到的值之右下方。
					else if(newNode->data>previousPtr->data){
						previousPtr->right=newNode;
						previousPtr->left=NULL;
					}
					newNode->left=NULL;
					newNode->right=NULL;
				} // end if(currentPtr==NULL)
			} // end else.
		} // end if(num!=-1
	}while(num!=-1);
}
void Search(Node* startPtr){

}
void Delete(Node* startPtr){

}
void Inorder(Node* startPtr){

}
void Postorder(Node* startPtr){
	    if (startPtr) {
        Postorder(startPtr->left);
        Postorder(startPtr->right);
        printf("%d\n", startPtr->data);
    }

}


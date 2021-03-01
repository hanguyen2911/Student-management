#include<stdio.h>
#include<string.h>
#include<stdlib.h>

typedef struct {
    char name[40];
    char MaSV[10];
    int KyTucXa;
    char GioiTinh;
    int age;
    float ALG2, CSDL, ENGLISH, TBC;
}SinhVien;

typedef struct {
    char tenLop[30];
    char giaoVien[20];
    int sySo;
    SinhVien SinhVien[50];
}Class;

//nhap lop
void nhapLop(Class * p,int count){
    printf("\n\t Nhap ten lop thu %d :", count);
    fflush(stdin);
    gets((p+count)->tenLop);
    printf("\n\t Nhap ten giao vien chu nhiem lop %s: ",(p+count)->tenLop );
    fflush(stdin);
    gets((p+count)->giaoVien);
       ((p+count)->sySo)=0;
}

//xem lop
void xemLop(Class * p, int count){
    int i;
   	for(i=1;i<=count;i++){
    	printf("\n\t Ten lop thu %d la: %s",i , (p+i)->tenLop);
    	printf("\n\t Giao vien chu nhiem lop %s: %s\n",(p+i)->tenLop,(p+i)->giaoVien);
	}  
}

//so sanh lop can tim voi lop da nhap
int kiemTra(Class * p, int count) {
	int i;
	char s[10];
	 	printf("\n\t Danh sach cac lop la: ");
	for (i = 1; i <= count; i++) {
	 	printf("\n\t  Lop thu %d: %s",i ,(p+i)->tenLop);}
       	printf("\n\t Ban can tim lop: ");
       	fflush(stdin);
        gets(s);
	for (i = 1; i <= count; i++) {   
		if (0 == stricmp(s,(p+i)->tenLop))
	return i;
	}
	return -1;
}

//nhap thong tin sinh vien
void nhapSV(Class * p,int count){
	char h,k;
	int n;
        tieptheo:
		n=kiemTra(p,count);
	if(n>=0){
		printf("\n\t ----- Nhap thong tin sinh vien lop %s -----\n",(p+n)->tenLop);
        tiep:
        printf("\n\t\tHo va ten sinh vien thu %d: ",((p+n)->sySo)+1);
    	fflush(stdin);
   		gets((p+n)->SinhVien[((p+n)->sySo)].name);
   		printf("\n\t\tMa sinh vien %s ", (p+n)->SinhVien[((p+n)->sySo)].name);
    	scanf(" %s",&(p+n)->SinhVien[((p+n)->sySo)].MaSV);
   		fflush(stdin);
    do{
    	printf("\n\t\tGioi Tinh M(nam) or F(nu) cua %s: ",(p+n)->SinhVien[((p+n)->sySo)].name);
        fflush(stdin);
    	scanf("%c",&(p+n)->SinhVien[((p+n)->sySo)].GioiTinh);
    }while((p+n)->SinhVien[((p+n)->sySo)].GioiTinh != 'M' && (p+n)->SinhVien[((p+n)->sySo)].GioiTinh != 'F'&& (p+n)->SinhVien[((p+n)->sySo)].GioiTinh != 'F');
    do{
    	printf("\n\t\tTuoi cua %s: ",(p+n)->SinhVien[((p+n)->sySo)].name);
    	scanf("%d%*c",&(p+n)->SinhVien[((p+n)->sySo)].age);
    }while((p+n)->SinhVien[((p+n)->sySo)].age<=10);
  	do{
    	printf("\n\t\tDiem mon ALG2: ");
   		scanf("%f",&(p+n)->SinhVien[((p+n)->sySo)].ALG2);
  	}while((p+n)->SinhVien[((p+n)->sySo)].ALG2<0 || (p+n)->SinhVien[((p+n)->sySo)].ALG2>10); 
  	do{
   		printf("\n\t\tDiem mon CSDL: ");
    	scanf("%f",&(p+n)->SinhVien[((p+n)->sySo)].CSDL);
    }while((p+n)->SinhVien[((p+n)->sySo)].CSDL<0 || (p+n)->SinhVien[((p+n)->sySo)].CSDL>10); 
    do{
    	printf("\n\t\tDiem mon ENGLISH: ");
    	scanf("%f",&(p+n)->SinhVien[((p+n)->sySo)].ENGLISH);
  	}while((p+n)->SinhVien[((p+n)->sySo)].ENGLISH<0 || (p+n)->SinhVien[((p+n)->sySo)].ENGLISH>10); 
    	printf("\n\t\tSo ky Tu Xa cua %s: ",(p+n)->SinhVien[((p+n)->sySo)].name);
   	    scanf("%d",&(p+n)->SinhVien[((p+n)->sySo)].KyTucXa);
          ((p+n)->sySo)++; 
    do{
     	printf("\n\tBan co muon nhap sinh vien tiep theo Y(co) or N(khong)");
	   	fflush(stdin);
        scanf(" %c",&h);
    }while(h!= 'y' && h!= 'n' && h!= 'Y' && h!= 'N');
        if( h == 'y' || h == 'Y'){
         goto tiep; 
       }
    do{
	    printf("\n\tTim ten lop tiep theo Y(co) or N(khong): ");
	    fflush(stdin);
        scanf(" %c",&k);
    }while(k!= 'y' && k!= 'n' && k!= 'Y' && k!= 'N');
        if( k == 'y' || k == 'Y'){
        goto tieptheo;
    	}
   }
    else{
       printf("\n\t Rat tiec! Khong co trong danh sach ban da nhap");}
}

//xep loai diem trung binh
void xeploai(Class *p, int n, int j){
    if((p+n)->SinhVien[j].TBC < 4){
        printf("\n\t Xep loai: KEM ",(p+n)->SinhVien[j].name); }
	else if((p+n)->SinhVien[j].TBC >= 4 && (p+n)->SinhVien[j].TBC < 5){
  		printf("\n\t Xep loai: YEU ",(p+n)->SinhVien[j].name); }
	else if((p+n)->SinhVien[j].TBC >= 5 && (p+n)->SinhVien[j].TBC < 6.5){
   		printf("\n\t Xep loai: TRUNG BINH ",(p+n)->SinhVien[j].name); }
	else if((p+n)->SinhVien[j].TBC >= 6.5 && (p+n)->SinhVien[j].TBC <8){
  	 	printf("\n\t Xep loai: KHA ",(p+n)->SinhVien[j].name); }
	else if((p+n)->SinhVien[j].TBC >= 8 && (p+n)->SinhVien[j].TBC <9){
   		printf("\n\t Xep loai: GIOI ", (p+n)->SinhVien[j].name);  }
	else{   
   		printf("\n\t Xep loai: SUAT SAC ",(p+n)->SinhVien[j].name);  ;
    }
}

//xem thong tin sinh vien
void xemSV(Class * p,  int count){
    int j,n;
	char h;
      tieptheo:
	    n=kiemTra(p,count);
	if(n>=0){
		    printf("\n\t +-------+---------------------+-----------+-----------+-----------+-----------+-----------+------+-----------+");
		    printf("\n\t | %-6s| %-20s| %-10s| %-10s| %-10s| %-10s| %-10s| %-5s| %-10s|","MSV", "Ho va ten", "Gioi tinh", "Tuoi", "ALG2", "CSDL", "ENGLISH", "DTB", "Ky Tuc Xa");
		    printf("\n\t |-------+---------------------+-----------+-----------+-----------+-----------+-----------+------+-----------|");
		for(j=0;j<((p+n)->sySo);j++){
			   (p+n)->SinhVien[j].TBC= ((p+n)->SinhVien[j].ALG2 + (p+n)->SinhVien[j].CSDL + (p+n)->SinhVien[j].ENGLISH)/3;
        	printf("\n\t | %-6s| %-20s| %-10s| %-10d| %-10.2f| %-10.2f| %-10.2f| %-5.2f| %-10d|",(p+n)->SinhVien[j].MaSV,(p+n)->SinhVien[j].name,(p+n)->SinhVien[j].GioiTinh =='M'?"Nam":"Nu", (p+n)->SinhVien[j].age,(p+n)->SinhVien[j].ALG2,(p+n)->SinhVien[j].CSDL,(p+n)->SinhVien[j].ENGLISH,(p+n)->SinhVien[j].TBC,(p+n)->SinhVien[j].KyTucXa);
        	}
        	printf("\n\t +-------+---------------------+-----------+-----------+-----------+-----------+-----------+------+-----------+");
		}
    else {
        printf("\n\t Rat tiec! Khong co trong danh sach ban da nhap");}
    do{
    	
	    printf("\n\t Tim lop tiep theo Y(co) or N(khong): ");
	    fflush(stdin);
        scanf(" %c",&h);
    }while(h!= 'y' && h!= 'n' && h!= 'Y' && h!= 'N');
    if( h == 'y' || h == 'Y'){
        goto tieptheo;
     }
}
    
//nhap ky tuc xa tim thong tin sinh vien
 void timKTX(Class *p, int count){
    	int i, j, ktx, dem=0;
	    printf("\n\t Nhap ten ky tuc xa: ");
	    scanf(" %d",&ktx);
        for(i = 1; i <= count; i++){
         for(j = 0; j<(p+i)->sySo; j++){
            if((p+i)->SinhVien[j].KyTucXa == ktx){
            	printf("\n\t -------------------------------------------");
                printf("\n\t Sinh vien: %s\n\t Tuoi: %d\n\t Gioi tinh: %s\n\t Lop: %s",(p+i)->SinhVien[j].name,(p+i)->SinhVien[j].age,(p+i)->SinhVien[j].GioiTinh =='M'?"Nam":"Nu",(p+i)->tenLop);
                dem++;
				}
			}
		}
		dem!=0?printf("\n\n\t ->Co %d sinh vien co ki tuc xa %d",dem, ktx):printf("\n\n\t Rat tiec! Khong co trong danh sach ban da nhap");
 }
 
//nhap khoang diem tim thong tin sinh vien
void timDiem(Class *p, int count){
	int a,b,i,j,dem=0;
	printf("\n\t Tim sinh vien co diem Trung Binh tu a den b");
	printf("\n\t Nhap a: ");
	scanf("%d",&a);
	printf("\n\t Nhap b: ");
	scanf("%d",&b);
        for(i = 1; i <= count; i++){
         for(j = 0; j<(p+i)->sySo; j++){
         	 if((p+i)->SinhVien[j].TBC >= a && (p+i)->SinhVien[j].TBC <= b){
         	 	printf("\n\t -------------------------------------------");
				printf("\n\t Ten: %s\n\t Tuoi: %d\n\t Gioi tinh: %s\n\t Lop: %s",(p+i)->SinhVien[j].name,(p+i)->SinhVien[j].age,(p+i)->SinhVien[j].GioiTinh =='M'?"Nam":"Nu",(p+i)->tenLop);
	 			xeploai(p,i,j);
	 		  	dem++;
         	}
	    }
	}
	    dem!=0?printf("\n\n\t ->Co %d sinh vien co diem Trung Binh tu %d den %d",dem,a,b):printf("\n\n\t Rat tiec! Khong co trong danh sach ban da nhap");
}

void main(){
	Class p[20];
	char  c;
    int n,  count=0, e;
    printf("\t\t\t\t  ***************************************************");
    printf("\n\t\t\t\t  *****      Chuong Trinh Quan Ly Sinh Vien     *****");
    printf("\n\t\t\t\t  ***************************************************");
    printf("\n\t\t\t\t =========================MENU======================== \n");
do{
	printf("\n\t   Xin vui long chon:");
	printf("\n\t ===========================================");
    printf("\n\t|  1. Nhap lop");
    printf("\n\t|  2. Nhap sinh vien");
    printf("\n\t|  3. Xem thong tin lop");
    printf("\n\t|  4. Xem sinh vien theo lop");
    printf("\n\t|  5. Tim kiem sinh vien theo diem trung binh");
    printf("\n\t|  6. Tim kiem sinh vien theo phong ky tuc xa");
    printf("\n\t|  7. Thoat chuong trinh");
    printf("\n\t ===========================================");
    char c;	
	do{
		fflush(stdin);
		printf("\n\t   =>Lua chon cua ban la: ");
		scanf("%d%c", &n, &c);
	}while( n!=1 && n!=2 && n!=3 && n!=4 && n!=5 && n!=6 && n!=7 || c != '\n');

    switch(n){
case 1:{
    char t;
    tieptuc:
    count++;
      nhapLop(p,count);
    do{
       printf("\n\t Ban co muon them lop tiep theo Y(co) or N(khong): ");
       scanf(" %c",&t);
    }while(t!= 'y' && t!= 'n' && t!= 'Y' && t!= 'N');
     if( t == 'y' || t == 'Y'){
       goto tieptuc;
     }
     break;
}
case 2:{ 
    nhapSV(p,count);
    break;
}
case 3:{
    xemLop(p,count);
    getch();
break;
}
case 4:{
    xemSV(p,count);
    getch();
break;
}
case 5:{
    timDiem(p,count);
    getch();
break;
}
case 6:{
	timKTX(p,count);
	getch();
break;
}
}
system("cls");
}while(n!=7);
printf("\n ==============================================Chuong Trinh ket thuc=====================================================");
}




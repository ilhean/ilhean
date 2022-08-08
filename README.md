#include<stdlib.h>//contiene atoi
#include<conio.h>
#include<windows.h>
#include<stdbool.h>
#include<stdio.h>//contiene atoi
#include<time.h>//contiene tiempo

struct fecha{
	
	
	unsigned int facismo;
	unsigned int dia;
	unsigned int mes;
	unsigned int ano;
	
};

struct tiempo{
	
	int hora;
	int min;
	int seg;
	
};

typedef struct entrada{
		
   struct tiempo t;
   struct fecha  f;
	
}entrada[2];


/*--------------------------------*/

void general(entrada*);
void menu();
void amd(entrada*);//amd año mes dias
bool dias(entrada*,int);
int validar(char[]);

/*---------------------------------*/

int main(){
	
	float reinicio = 0;
	entrada a;
	
	while (reinicio != 1 ){
		
		general(&a);
		fflush(stdin);
		printf("\n\n\n\n\t\tPara finalizar presione 1 / otra tecla para reiniciar: ");
		scanf("%10f",&reinicio);		
		
		if(reinicio == 1) exit(-1);
		
	}

	

	return 0;
}

void menu(){
	
	time_t reloj = time(NULL);//TOMA TIEMPO ACTUAL DEL SISTEMA
	struct tm *r;//PUNTERO A ESTRUCTURA TIME.H
	r = localtime(&reloj);
	char *semana[7] = {"Domingo","Lunes","Martes","Miercoles","Jueves","Viernes","Sabado"};//matriz de cadenas para dias semana
	char *mes[12] = {"Enero","Febrero","Marzo","Abril","Mayo","Junio","Julio","Agosto","Septiembre","Octubre","Noviembre","Diciembre"};//MESES DEL AÑO
			
	printf("%s %d %s %d",semana[r->tm_wday],r->tm_mday,mes[r->tm_mday],1900+r->tm_year);
	
	if(r->tm_hour>=12)//PM 	
	printf("|%02d:%02d pm",r->tm_hour,r->tm_min);
	else//AM
	printf("|%02d:%02d am",r->tm_hour,r->tm_min);
	
	printf("\n\n\n\n\n\t\t  CALCULADORA DIFERENCIAS ENTRE DOS FECHAS");
	printf("\n\n\t\t 1.  CALCULADORA");
	printf("\n\n\t\t 2.  COMO USAR LA CALCULADORA");
	printf("\n\n\t\t INGRESE UN DIGITO: ");

}

void general(entrada *tp){
	
	int i,v,m; // v retorna validar, m datos del menu	
	char cadena[10];
	char *cont[5] = {"inicial", "final"};
	bool bo;
	int prueba;
	  do{
		
		fflush(stdin);	
		system("cls");	
		cadena[0]=0;			
		menu();
		scanf("%20[^\n]",cadena);
		v = validar(cadena);
		m = atoi(cadena); 
		
	  }while(v==0 || m<1 || m>2);
	
	
		switch(m){
			
			case 1: 
			
			for(i=0;i<2;i++){
				

				do{
									
					fflush(stdin);				
					system("cls");		
					cadena[0] = 0; //limpia la cadena de validar y al ingresar "enter" retorna 0				
					tp[1]->f.ano = 100000; //Inicio el año final en 10000 para evitar errores con el if
					printf("\n\n\t\tIngrese el a%co %s: ",164, cont[i]);
					scanf("%20[^\n]",cadena);
					v = validar(cadena); 
					tp[i]->f.ano = atoi(cadena);
					
					if(v!=0){//si hay una letra reinicia bucle o si año es 0
						
						if(tp[0]->f.ano > tp[1]->f.ano){
							
							printf("\n\n\t\tTIENE que ser mayor al a%co de inicio",164);
							getch();
							
						}	
							
						
						if(tp[i]->f.ano < 1900){
							
							printf("\n\n\t\tNO puede ser menor a 1900");
							getch();
							
						}
							
					}	
						
			   }while(v==0  || tp[0]->f.ano > tp[1]->f.ano || tp[i]->f.ano < 1900);
				
					
				do{
			
					fflush(stdin);	
					system("cls");
					cadena[0] = 0; //limpia la cadena de validar y al ingresar "enter" retorna 0
					printf("\n\n\t\tIngrese el mes %s: ", cont[i]);
					scanf("%20[^\n]",cadena);
					v = validar(cadena); 
					tp[i]->f.mes = atoi(cadena);
				
					if(v!=0){//si hay una letra reinicia bucle o si es 0
						
						if(tp[i]->f.mes > 12){
							
							printf("\n\n\t\tNO puede ser mayor a 12");
							getch();
							
						}	
						
					}
					
					
						
				}while(v==0 || tp[i]->f.mes > 12);
				
				do{
			
					fflush(stdin);
					system("cls");					
					cadena[0] = 0; //limpia la cadena de validar	
					printf("\n\n\t\tIngrese el dia %s: ", cont[i]);
					scanf("%20[^\n]",cadena);
					v = validar(cadena); 
					tp[i]->f.dia = atoi(cadena);
				
					if(v!=0){//si hay una letra reinicia bucle o si dia es 0
						
						if(tp[i]->f.dia < 1 || tp[i]->f.dia > 31){
							
							printf("\n\n\t\tNO puede ser menor 0 o mayor a 31");
							getch();
							
						}	
						
					}
								
				}while(v==0 || tp[i]->f.dia < 1 || tp[i]->f.dia > 31  || dias(tp,i) == false);
				
				//dias(tp,i) esta pasando como un puntero *tp a la funcion booleana que mediante la los valores
				//proporcionados evalua si es correcto 
				//i es el si es la primera o la segunda fecha
				
			}
				
				amd(tp); // funcion que calcula las diferencias
							
			break;
			
			case 2:
			
				system("cls");
				
				printf("\n\n\t\t\t\tGuia del codigo");	
				printf("\n\n\n\n\t1..Se encontrara error al ingresar la segunda fecha menor a la primera.");
				printf("\n\t2..El codigo fue realizado con la libreria time.h");
				printf("\n\t3..NO pueden ser ingresados dias y meses mayores a dos digitos");
				printf("\n\t4..NO puede ser ingresados a%cos mayores a cuatro digitos",164);
				printf("\n\t5..El a%co minimo es de 1900",164);
				printf("\n\t6..El codigo mostrara segundos, minutos, horas");
				printf("\n\t7..El codigo mostrara a%cos meses semanas y dias",164);
				
			break;	
		}
			
}



void amd(entrada *tp){

	int a,b,i,aux;
	struct tm tm1; 		
	struct tm tm2;
	double diferencia;
	
//la estructura toma los valores de la estructura de la libreria time.h	

	tm1.tm_year = tp[0]->f.ano - 1900; //los años son iguales al año - 1900;
	tm2.tm_year = tp[1]->f.ano - 1900;
	tm1.tm_mon  = tp[0]->f.mes - 1; //Los meses van de 0 a 11
	tm2.tm_mon  = tp[1]->f.mes - 1;
	tm1.tm_mday = tp[0]->f.dia;
	tm2.tm_mday = tp[1]->f.dia;
	
	/*horas minutos y segundos*/
    //se igualan a 0 para reiniciar todo a una misma hora	

    tm1.tm_hour = 0;
	tm2.tm_hour = 0;
	tm1.tm_min = 0;
	tm2.tm_min = 0;
	tm1.tm_sec = 0;
	tm2.tm_sec = 0;


//mktime combierte variables de tipo entero a variables de time_t
	
	a = mktime(&tm1);	
	b = mktime(&tm2); 
	
//difftime toma dos tiempo y los saca la diferencia entre ambos	
//b esta primero que a porque difftime al tomar el año inicial como menor al primero devuelve datos
//en negativo al poner b primero que a o el año final primero que el inicial evita ese problema

	diferencia = difftime(b,a);

//	diferencia = diferencia / 3600  * 24 divido entre los segundos que tiene una hora para saber cuantas horas
//hay en la diferencia de difftime y luego lo multiplico por 24 para determinar cuantos dias son en total
	
	///(3600*24)
	
	system("cls");
	printf("\n\n\n\t\t\t\tRESULTADOS\n\n");
	printf("\n\n\t\tEntre %d/%d/%d y %d/%d/%d han pasado",tp[0]->f.dia,tp[0]->f.mes, tp[0]->f.ano ,tp[1]->f.dia,tp[1]->f.mes,tp[1]->f.ano);
	printf("\n\n\t\tSegundos: %.0f",diferencia);
	printf("\n\t\tMinutos: %.0f",diferencia/60);
	printf("\n\t\tHoras: %.0f",diferencia/3600);
	printf("\n\t\tDias: %.0f",diferencia/(3600*24));		
	printf("\n\t\tSemanas: %.0f",diferencia/(3600*24*7));
	printf("\n\t\tMeses: %.0f",diferencia/(3600*24*30.44));

	aux = diferencia/(3600*24*365); //toma el año en entero
	
	if((diferencia/(3600*24*365)) - aux != 0){
			
		printf("\n\t\tA%cos: %d ",164,aux);	
		aux = aux * 365;		
		printf("con %.0f dias", diferencia/(3600*24) - aux);
		
	}
	
	else
	printf("\n\t\tA%cos: %.0f",164,diferencia/(3600*24*365));	
	
}


//toma un puntero de struct entrada y evalua si mediante su indreccion s
bool dias(entrada *tp, int n){
	
	int mesd[13] = {0,31,28,31,30,31,30,31,31,30,31,30,31};// Meses del año no bisiesto	
	char *mes[12] = {"Enero","Febrero","Marzo","Abril","Mayo","Junio","Julio","Agosto","Septiembre","Octubre","Noviembre","Diciembre"};//MESES DEL AÑO

	
		if(tp[n]->f.dia <= mesd[tp[n]->f.mes])//si la estructura [1 o 2] es menor o igual al dia del mes ingresado
		return true;					
			//retorna true
		
		else{
			
			printf("\n\n\t\tEL mes de %s que ha ingresado tiene un maximo de %d dias",mes[tp[n]->f.mes-1],mesd[tp[n]->f.mes]);
			getch();
			return false;
			//return false
		}	
}

int validar(char validar[100]){
			
		int i;
							
			for(i=0;i<strlen(validar);i++){
				
				
				if(strlen(validar)>4){
					
					printf("\n\n\t\tEl numero es muy grande\n\n\n");	
					getch();	
					return 0;	
					break;
				}
				
					if(isdigit(validar[i])){
				//si i es igual a la longitud de la cadena retorna 1 
				//esto fuerza a que se lea la cadena entera															
					if(i==strlen(validar)){		 			
						return 1;
					}						
				}		
				
				
				
				else{
					//si isdigit no es un numero retorna 0 y se repite
					printf("\n\n\t\tIngrese solo numeros\n\n");
					getch();
					return 0;
					
				}
											
			}
	}

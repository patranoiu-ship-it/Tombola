# Tombola

esercizio tombola:

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(int argc, char** argv) {
	
	srand(time(NULL));
	
	  int cart1[3][5] = {0};//dichiarazione di una cartella composta da 15 numeri
    int cart2[3][5] = {0};//dichiarazione di una cartella composta da 15 numeri
    
    //generazione cartella 1
    for(int i=0; i<3; i++)
    {
    	int decine[10]={0};
    	for(int j=0; j<5; j++)
    	{
    		int numero, decina, valido;
    		do
			{
    			valido=1;
    			numero=rand()%90+1;
    			if(numero==90)
    			{
    		    decina=8;
				}
    			else
    			{
    			decina=numero/10;
    		    }
    			if(decine[decina]==1)
    			{
    		    valido=0;
    		    }
    		    for(int z=0; z<3; z++)
    		    {
    		    	for(int k=0; k<5; k++)
    		    	{
    		    		if(cart1[z][k]==numero)
    		    		valido=0;
					}
				}
			}while(valido==0);
			cart1[i][j]=numero;
			decine[decina]=1;
		}
	}
	
	//generazione cartella 2
	for(int i=0; i<3; i++)
    {
    	int decine[10]={0};
    	for(int j=0; j<5; j++)
    	{
    		int numero, decina, valido;
    		do
			{
    			valido=1;
    			numero=rand()%90+1;
    			if(numero==90)
    			{
    		    decina=8;
				}
    			else
    			{
    			decina=numero/10;
    		    }
    			if(decine[decina]==1)
    			{
    		    valido=0;
    		    }
    		    for(int z=0; z<3; z++)
    		    {
    		    	for(int k=0; k<5; k++)
    		    	{
    		    		if(cart2[z][k]==numero)
    		    		valido=0;
					}
				}
			}while(valido==0);
			cart2[i][j]=numero;
			decine[decina]=1;
		}
	}
	
	//stampa le cartelle
	cout<<"Cartella giocatore 1:"<<endl;
	for(int i=0; i<3; i++)
	{
		for(int j=0; j<5; j++)
		{
			if(cart1[i][j] < 10)
			{
				cout<<" "<<cart1[i][j]<<" ";
			}else
			{
				cout<<cart1[i][j]<<" ";
			}
		}
		cout<<endl;
	}
	
	cout<<"Cartella giocatore 2:"<<endl;
	for(int i=0; i<3; i++)
	{
		for(int j=0; j<5; j++)
		{
			if(cart2[i][j] < 10)
			{
				cout<<" "<<cart2[i][j]<<" ";
			}else
			{
				cout<<cart2[i][j]<<" ";
			}
		}
		cout<<endl;
	}
	cout<<"Premi invio per iniziare l'estrazione dei numeri";
	cin.get();
	
	
	return 0;
}


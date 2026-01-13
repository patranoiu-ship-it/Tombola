tombola

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;


int main(int argc, char** argv) {

    srand(time(NULL));

    int cart1[3][9] = {0};
    int cart2[3][9] = {0};
    int estratti[91] = {0};
  

    //Generazione cartella 1 
    for(int i = 0; i < 3; i++) {
  
        int inseriti = 0;

        while(inseriti < 5) {

            int numero, colonna, valido = 1;

            numero = rand() % 90 + 1;

            if(numero == 90)
            {
            	colonna = 8;
			}
            else
            {
            	colonna = numero / 10;
			}
                
            // colonna già occupata nella riga
            if(cart1[i][colonna] != 0)
                valido = 0;

            // numero già presente nella cartella
            for(int z = 0; z < 3; z++)
                for(int k = 0; k < 9; k++)
                    if(cart1[z][k] == numero)
                        valido = 0;

            if(valido == 1) {
                cart1[i][colonna] = numero;
                inseriti++;
            }
        }
    }

    //Generazione cartella 2 
    for(int i = 0; i < 3; i++) {

        int inseriti = 0;

        while(inseriti < 5) {

            int numero, colonna, valido = 1;

            numero = rand() % 90 + 1;

            if(numero == 90)
                colonna = 8;
            else
                colonna = numero / 10;

            if(cart2[i][colonna] != 0)
                valido = 0;

            for(int z = 0; z < 3; z++)
                for(int k = 0; k < 9; k++)
                    if(cart2[z][k] == numero)
                        valido = 0;

            if(valido == 1) {
                cart2[i][colonna] = numero;
                inseriti++;
            }
        }
    }

    //stampaggio cartelle
    cout << "Cartella giocatore 1"<<endl;
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 9; j++) {
            if(cart1[i][j] == 0)
                cout << "   ";
            else if(cart1[i][j] < 10)
                cout << " " << cart1[i][j] << " ";
            else
                cout << cart1[i][j] << " ";
        }
        cout << endl;
    }
    cout<<endl;

    cout << "Cartella giocatore 2"<<endl;
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 9; j++) {
            if(cart2[i][j] == 0)
                cout << "   ";
            else if(cart2[i][j] < 10)
                cout << " " << cart2[i][j] << " ";
            else
                cout << cart2[i][j] << " ";
        }
        cout << endl;
    }

    cout << "Premi INVIO per iniziare l'estrazione";
    cin.get();

    //Estrazione numeri
    while(1) {

        int numero, v1 = 1, v2 = 1;

        do {
            numero = rand() % 90 + 1;
        } while(estratti[numero] == 1);
system("cls"); 
        estratti[numero] = 1;
        cout << "Il numero estratto e': " << numero << endl;

        // controllo tombola
        for(int i = 0; i < 3; i++){  
            for(int j = 0; j < 9; j++){
                if(cart1[i][j] != 0 && estratti[cart1[i][j]] == 0)
                    v1 = 0;
           }
        }

        for(int i = 0; i < 3; i++){
            for(int j = 0; j < 9; j++){
                if(cart2[i][j] != 0 && estratti[cart2[i][j]] == 0)
                    v2 = 0;
            }
        }
        cout<<endl;

        // stampa aggiornata
        cout << "Giocatore 1"<<endl;
        for(int i = 0; i < 3; i++) {   
            for(int j = 0; j < 9; j++) {
                if(cart1[i][j] == 0)
                    cout << "   ";
                else if(estratti[cart1[i][j]] == 1)
                    cout << " X ";
                else if(cart1[i][j] < 10)
                    cout << " " << cart1[i][j] << " ";
                else
                    cout << cart1[i][j] << " ";
            }
            cout << endl;
        }
        cout<<endl;

        cout << "Giocatore 2"<<endl;
        for(int i = 0; i < 3; i++) { 
            for(int j = 0; j < 9; j++) {
                if(cart2[i][j] == 0)
                    cout << "   ";
                else if(estratti[cart2[i][j]] == 1)
                    cout << " X ";
                else if(cart2[i][j] < 10)
                    cout << " " << cart2[i][j] << " ";
                else
                    cout << cart2[i][j] << " ";
            }     
            cout << endl;
        }

        if(v1 == 1) {
            cout << "tombola, vince il giocatore 1"<<endl;
            break;
        }
        if(v2 == 1) {
            cout << "tombola, vince il giocatore 2"<<endl;
            break;
        }

        cout << "\nPremi INVIO per estrarre il prossimo numero";
        cin.get();
    }
  
    return 0;
}

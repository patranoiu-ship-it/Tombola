esercizio tombola
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(int argc, char** argv) {

    srand(time(NULL));

    int cart1[3][9] = {0};
    int cart2[3][9] = {0};
    int estratti[91] = {0};

    
    // Generazione cartella 1
    
    for(int i = 0; i < 3; i++) {
        int inseriti = 0;

        while(inseriti < 5) {
            int numero, colonna, valido = 1;

            numero = rand() % 90 + 1;

            if(numero == 90)
                colonna = 8;
            else
                colonna = numero / 10;

            if(cart1[i][colonna] != 0)
                valido = 0;

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

    
    // Generazione cartella 2
    
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

    // Estrazione numeri
    
    while(1) {

        int numero, v1 = 1, v2 = 1;

        do {
            numero = rand() % 90 + 1;
        } while(estratti[numero] == 1);

        estratti[numero] = 1;

        system("cls");

        // Tabellone tombola

        cout << "TABELLONE TOMBOLA\n";
        for(int n = 1; n <= 90; n++) {

            if(estratti[n] == 1)
                cout << "\033[32m";
            else
                cout << "\033[0m";

            if(n < 10)
                cout << " " << n << " ";
            else
                cout << n << " ";

            if(n % 10 == 0)
                cout << endl;
        }
        cout << "\033[0m\n";

        cout << "\nNumero estratto: \033[32m" << numero << "\033[0m\n\n";

        // Cartella giocatore 1

        cout << "Cartella giocatore 1\n";
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < 9; j++) {
                if(cart1[i][j] == 0)
                    cout << "   ";
                else if(estratti[cart1[i][j]] == 1)
                    cout << "\033[32m X \033[0m";
                else if(cart1[i][j] < 10)
                    cout << " " << cart1[i][j] << " ";
                else
                    cout << cart1[i][j] << " ";
            }
            cout << endl;
        }

        // Cartella giocatore 2 

        cout << "\nCartella giocatore 2\n";
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < 9; j++) {
                if(cart2[i][j] == 0)
                    cout << "   ";
                else if(estratti[cart2[i][j]] == 1)
                    cout << "\033[32m X \033[0m";
                else if(cart2[i][j] < 10)
                    cout << " " << cart2[i][j] << " ";
                else
                    cout << cart2[i][j] << " ";
            }
            cout << endl;
        }

        // Controllo tombola

        for(int i = 0; i < 3; i++)
            for(int j = 0; j < 9; j++)
                if(cart1[i][j] != 0 && estratti[cart1[i][j]] == 0)
                    v1 = 0;

        for(int i = 0; i < 3; i++)
            for(int j = 0; j < 9; j++)
                if(cart2[i][j] != 0 && estratti[cart2[i][j]] == 0)
                    v2 = 0;

        if(v1 == 1) {
            cout << "\nTOMBOLA! Vince il giocatore 1\n";
            break;
        }
        if(v2 == 1) {
            cout << "\nTOMBOLA! Vince il giocatore 2\n";
            break;
        }

        system("pause");
    }

    return 0;
}

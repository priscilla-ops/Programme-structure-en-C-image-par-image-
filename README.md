# Programme-structure-en-C
#include <stdio.h>
#include <string.h>

#define MAX 100

/*================= STRUCTURE =================*/

typedef struct {

    char nom[50];
    char date_naissance[15];
    char adresse[100];
    char niveau[10];
    float moyenne;

} Eleve;

/*================= TABLEAU =================*/

Eleve classe[MAX];
int n = 0;

/*================= AJOUT =================*/

void ajouter() {

    if (n >= MAX) {

        printf("Liste pleine !\n");
        return;
    }

    printf("\nNom : ");
    scanf(" %[^\n]", classe[n].nom);

    printf("Date de naissance (JJ/MM/AAAA) : ");
    scanf(" %[^\n]", classe[n].date_naissance);

    printf("Adresse : ");
    scanf(" %[^\n]", classe[n].adresse);

    printf("Niveau : ");
    scanf(" %[^\n]", classe[n].niveau);

    printf("Moyenne : ");
    scanf("%f", &classe[n].moyenne);

    n++;

    printf("Eleve ajoute avec succes.\n");
}

/*================= AFFICHAGE =================*/

void afficher() {

    if (n == 0) {

        printf("Aucun eleve.\n");
        return;
    }

    for (int i = 0; i < n; i++) {

        printf("\n=====================\n");

        printf("Eleve %d\n", i + 1);

        printf("Nom : %s\n",
               classe[i].nom);

        printf("Date naissance : %s\n",
               classe[i].date_naissance);

        printf("Adresse : %s\n",
               classe[i].adresse);

        printf("Niveau : %s\n",
               classe[i].niveau);

        printf("Moyenne : %.2f\n",
               classe[i].moyenne);
    }
}

/*================= RECHERCHE EXACTE =================*/

void rechercher() {

    char nom[50];
    int trouve = 0;

    printf("Nom a rechercher : ");
    scanf(" %[^\n]", nom);

    for (int i = 0; i < n; i++) {

        if (strcmp(classe[i].nom, nom) == 0) {

            printf("\nEleve trouve :\n");

            printf("Nom : %s\n",
                   classe[i].nom);

            printf("Date naissance : %s\n",
                   classe[i].date_naissance);

            printf("Adresse : %s\n",
                   classe[i].adresse);

            printf("Niveau : %s\n",
                   classe[i].niveau);

            printf("Moyenne : %.2f\n",
                   classe[i].moyenne);

            trouve = 1;
        }
    }

    if (trouve == 0) {

        printf("Eleve introuvable.\n");
    }
}

/*================= BARRE DE RECHERCHE =================*/

void barreRecherche() {

    char mot[50];

    while (1) {

        printf("\nRecherche (0 pour quitter) : ");
        scanf(" %[^\n]", mot);

        if (strcmp(mot, "0") == 0) {

            break;
        }

        int trouve = 0;

        printf("\n===== RESULTATS =====\n");

        for (int i = 0; i < n; i++) {

            if (strstr(classe[i].nom, mot) != NULL ||
                strstr(classe[i].adresse, mot) != NULL ||
                strstr(classe[i].niveau, mot) != NULL) {

                printf("\nNom : %s\n",
                       classe[i].nom);

                printf("Niveau : %s\n",
                       classe[i].niveau);

                printf("Adresse : %s\n",
                       classe[i].adresse);

                printf("Moyenne : %.2f\n",
                       classe[i].moyenne);

                trouve = 1;
            }
        }

        if (trouve == 0) {

            printf("Aucun resultat.\n");
        }
    }
}

/*================= MODIFICATION =================*/

void modifier() {

    char nom[50];

    printf("Nom de l'eleve a modifier : ");
    scanf(" %[^\n]", nom);

    for (int i = 0; i < n; i++) {

        if (strcmp(classe[i].nom, nom) == 0) {

            printf("Nouvelle adresse : ");
            scanf(" %[^\n]", classe[i].adresse);

            printf("Nouveau niveau : ");
            scanf(" %[^\n]", classe[i].niveau);

            printf("Nouvelle moyenne : ");
            scanf("%f", &classe[i].moyenne);

            printf("Modification reussie.\n");

            return;
        }
    }

    printf("Eleve introuvable.\n");
}

/*================= TRI PAR NOM =================*/

void trierNom() {

    Eleve temp;

    for (int i = 0; i < n - 1; i++) {

        for (int j = i + 1; j < n; j++) {

            if (strcmp(classe[i].nom,
                       classe[j].nom) > 0) {

                temp = classe[i];
                classe[i] = classe[j];
                classe[j] = temp;
            }
        }
    }

    printf("Tri par nom termine.\n");
}

/*================= COMPARAISON DATE =================*/

int comparerDate(char d1[], char d2[]) {

    int j1, m1, a1;
    int j2, m2, a2;

    sscanf(d1, "%d/%d/%d",
           &j1, &m1, &a1);

    sscanf(d2, "%d/%d/%d",
           &j2, &m2, &a2);

    if (a1 != a2)
        return a1 - a2;

    if (m1 != m2)
        return m1 - m2;

    return j1 - j2;
}

/*================= TRI PAR DATE =================*/

void trierDate() {

    Eleve temp;

    for (int i = 0; i < n - 1; i++) {

        for (int j = i + 1; j < n; j++) {

            if (comparerDate(
                classe[i].date_naissance,
                classe[j].date_naissance) > 0) {

                temp = classe[i];
                classe[i] = classe[j];
                classe[j] = temp;
            }
        }
    }

    printf("Tri par date termine.\n");
}

/*================= TRI PAR MOYENNE =================*/

void trierMoyenne() {

    Eleve temp;

    for (int i = 0; i < n - 1; i++) {

        for (int j = i + 1; j < n; j++) {

            if (classe[i].moyenne <
                classe[j].moyenne) {

                temp = classe[i];
                classe[i] = classe[j];
                classe[j] = temp;
            }
        }
    }

    printf("Tri par moyenne termine.\n");
}

/*================= SUPPRESSION =================*/

void supprimerNonAdmis() {

    float seuil;

    printf("Moyenne minimale : ");
    scanf("%f", &seuil);

    int i = 0;

    while (i < n) {

        if (classe[i].moyenne < seuil) {

            for (int j = i; j < n - 1; j++) {

                classe[j] = classe[j + 1];
            }

            n--;
        }

        else {

            i++;
        }
    }

    printf("Suppression terminee.\n");
}

/*================= SAUVEGARDE =================*/

void sauvegarder() {

    FILE *f;

    f = fopen("eleves.txt", "w");

    if (f == NULL) {

        printf("Erreur fichier.\n");
        return;
    }

    for (int i = 0; i < n; i++) {

        fprintf(f,
                "%s;%s;%s;%s;%.2f\n",

                classe[i].nom,
                classe[i].date_naissance,
                classe[i].adresse,
                classe[i].niveau,
                classe[i].moyenne);
    }

    fclose(f);

    printf("Sauvegarde reussie.\n");
}

/*================= CHARGEMENT =================*/

void charger() {

    FILE *f;

    f = fopen("eleves.txt", "r");

    if (f == NULL) {

        return;
    }

    n = 0;

    while (fscanf(f,
           " %49[^;];%14[^;];%99[^;];%9[^;];%f\n",

           classe[n].nom,
           classe[n].date_naissance,
           classe[n].adresse,
           classe[n].niveau,
           &classe[n].moyenne) != EOF) {

        n++;
    }

    fclose(f);
}

/*================= MENU =================*/

int main() {

    int choix;

    charger();

    do {

        printf("\n");
        printf("=================================\n");
        printf("GESTION DES INSCRIPTIONS\n");
        printf("=================================\n");

        printf("1. Ajouter un eleve\n");
        printf("2. Afficher les eleves\n");
        printf("3. Rechercher un eleve\n");
        printf("4. Barre de recherche\n");
        printf("5. Modifier un eleve\n");
        printf("6. Trier par nom\n");
        printf("7. Trier par date\n");
        printf("8. Trier par moyenne\n");
        printf("9. Supprimer non admis\n");
        printf("10. Sauvegarder\n");
        printf("11. Quitter\n");

        printf("Choix : ");
        scanf("%d", &choix);

        switch (choix) {

            case 1:
                ajouter();
                break;

            case 2:
                afficher();
                break;

            case 3:
                rechercher();
                break;

            case 4:
                barreRecherche();
                break;

            case 5:
                modifier();
                break;

            case 6:
                trierNom();
                break;

            case 7:
                trierDate();
                break;

            case 8:
                trierMoyenne();
                break;

            case 9:
                supprimerNonAdmis();
                break;

            case 10:
                sauvegarder();
                break;

            case 11:
                printf("Fin du programme.\n");
                break;

            default:
                printf("Choix invalide.\n");
        }

    } while (choix != 11);

    return 0;
}

#include <SoftwareSerial.h>

SoftwareSerial bluetooth(10, 11); 
int moteurDroiteAvant = 3; 
int moteurDroiteArriere = 5;
int moteurGaucheAvant = 6; 
int moteurGaucheArriere = 9; 

void setup() {
  bluetooth.begin(9600);
  pinMode(moteurDroiteAvant, OUTPUT);
  pinMode(moteurDroiteArriere, OUTPUT);
  pinMode(moteurGaucheAvant, OUTPUT);
  pinMode(moteurGaucheArriere, OUTPUT);
}

void loop() {
  if (bluetooth.available() > 0) { 
    char commande = bluetooth.read(); 

    switch (commande) { 
      case 'A': // avance
        avancer();
        break;
      case 'R': // recule
        reculer();
        break;
      case 'G': // tourne à gauche
        tournerGauche();
        break;
      case 'D': // tourne à droite
        tournerDroite();
        break;
      case 'S': // arrêt
        stop();
        break;
    }
  }
}

void avancer() {
  digitalWrite(moteurDroiteAvant, HIGH);
  digitalWrite(moteurDroiteArriere, LOW);
  digitalWrite(moteurGaucheAvant, HIGH);
  digitalWrite(moteurGaucheArriere, LOW);
}

void reculer() {
  digitalWrite(moteurDroiteAvant, LOW);
  digitalWrite(moteurDroiteArriere, HIGH);
  digitalWrite(moteurGaucheAvant, LOW);
  digitalWrite(moteurGaucheArriere, HIGH);
}

void tournerGauche() {
  digitalWrite(moteurDroiteAvant, HIGH);
  digitalWrite(moteurDroiteArriere, LOW);
  digitalWrite(moteurGaucheAvant, LOW);
  digitalWrite(moteurGaucheArriere, HIGH);
}

void tournerDroite() {
  digitalWrite(moteurDroiteAvant, LOW);
  digitalWrite(moteurDroiteArriere, HIGH);
  digitalWrite(moteurGaucheAvant, HIGH);
  digitalWrite(moteurGaucheArriere, LOW);
}

void stop() {
  digitalWrite(moteurDroiteAvant, LOW);
  digitalWrite(moteurDroiteArriere, LOW);
  digitalWrite(moteurGaucheAvant, LOW);
  digitalWrite(moteurGaucheArriere, LOW);
}



# aruino-sd-bottone
il bottone va attaccato al pin 5, mentre i pin del lettore sd sono fissi prova a cercarli su intenet. devi anche vedere quali schede vanno perché mi ricordo che non tutte funzionano



#include <SD.h>
File myFile;
int stato = 0;
double tempo = 0;


void setup() {
  pinMode(5, INPUT);

  
  if (SD.begin(10))
  {
    Serial.println("SD card is present & ready");
  } 
  else
  {
    Serial.println("SD card missing or failure");
    while(1); //
  }
  //rimuove il file se è presente
  if (SD.exists("csv.txt")) 
  {
    Serial.println("Removing simple.txt");
    SD.remove("csv.txt");
    Serial.println("Done");
  } 

  //scrive un nuovo file e cosa fa
   myFile = SD.open("csv.txt", FILE_WRITE);  
   if (myFile) 
    {
    Serial.println("Writing headers to csv.txt");
    myFile.println("Time, button status");
    myFile.close(); 
    
    }
  else 
  // se non riesce
    Serial.println("Error opening csv.txt");  
  Serial.println("Enter w for write, r for read or s for split csv");

}

void loop() {
  // guarda se il bottone è premuto o no
  stato = digitalRead(5);
  //tiene il tempo, facendolo aumentare di 0.02 ogni loop aumenta di 1 ogni secondo
  tempo = tempo +0.02;
  
   myFile = SD.open("csv.txt", FILE_WRITE);     
    // if the file opened okay, write to it:
    if (myFile) 
    {
          

      myFile.println(stato);
      myFile.println(tempo);
   
      
      myFile.println("...............................................");
     

      myFile.close();
  
    } 

}

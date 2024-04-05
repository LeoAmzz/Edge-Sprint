# Edge-Sprint



# Descrição:
O projeto apresenta uma solução inovadora para tornar os exames de sangue pediátricos mais reconfortantes, envolvendo o uso de óculos de realidade virtual e um sistema baseado em Arduino. Enquanto as crianças exploram um mundo imaginário dentro da realidade virtual, o Arduino monitora seus sinais vitais (nesse projeto simulamos um sensor de sinais vitais atraves de um potenciometro) e ativa estímulos calmantes, como luzes suaves e música tranquilizadora, caso detecte sinais de ansiedade. Essa abordagem visa proporcionar uma experiência mais positiva e menos estressante para as crianças durante os procedimentos médicos, promovendo um ambiente hospitalar mais acolhedor e reconfortante.

# Link Wokwi:
https://wokwi.com/projects/394192185544489985

# Código

#define NOTE_B0  31
#define NOTE_C1  33
#define NOTE_CS1 35
#define NOTE_D1  37
#define NOTE_DS1 39
#define NOTE_E1  41
#define NOTE_F1  44
#define NOTE_FS1 46
#define NOTE_G1  49
#define NOTE_GS1 52
#define NOTE_A1  55
#define NOTE_AS1 58
#define NOTE_B1  62
#define NOTE_C2  65
#define NOTE_CS2 69
#define NOTE_D2  73
#define NOTE_DS2 78
#define NOTE_E2  82
#define NOTE_F2  87
#define NOTE_FS2 93
#define NOTE_G2  98
#define NOTE_GS2 104
#define NOTE_A2  110
#define NOTE_AS2 117
#define NOTE_B2  123
#define NOTE_C3  131
#define NOTE_CS3 139
#define NOTE_D3  147
#define NOTE_DS3 156
#define NOTE_E3  165
#define NOTE_F3  175
#define NOTE_FS3 185
#define NOTE_G3  196
#define NOTE_GS3 208
#define NOTE_A3  220
#define NOTE_AS3 233
#define NOTE_B3  247
#define NOTE_C4  262
#define NOTE_CS4 277
#define NOTE_D4  294
#define NOTE_DS4 311
#define NOTE_E4  330
#define NOTE_F4  349
#define NOTE_FS4 370
#define NOTE_G4  392
#define NOTE_GS4 415
#define NOTE_A4  440
#define NOTE_AS4 466
#define NOTE_B4  494
#define NOTE_C5  523
#define NOTE_CS5 554
#define NOTE_D5  587
#define NOTE_DS5 622
#define NOTE_E5  659
#define NOTE_F5  698
#define NOTE_FS5 740
#define NOTE_G5  784
#define NOTE_GS5 831
#define NOTE_A5  880
#define NOTE_AS5 932
#define NOTE_B5  988
#define NOTE_C6  1047
#define NOTE_CS6 1109
#define NOTE_D6  1175
#define NOTE_DS6 1245
#define NOTE_E6  1319
#define NOTE_F6  1397
#define NOTE_FS6 1480
#define NOTE_G6  1568
#define NOTE_GS6 1661
#define NOTE_A6  1760
#define NOTE_AS6 1865
#define NOTE_B6  1976
#define NOTE_C7  2093
#define NOTE_CS7 2217
#define NOTE_D7  2349
#define NOTE_DS7 2489
#define NOTE_E7  2637
#define NOTE_F7  2794
#define NOTE_FS7 2960
#define NOTE_G7  3136
#define NOTE_GS7 3322
#define NOTE_A7  3520
#define NOTE_AS7 3729
#define NOTE_B7  3951
#define NOTE_C8  4186
#define NOTE_CS8 4435
#define NOTE_D8  4699
#define NOTE_DS8 4978
#define REST 0

const int potentiometerPin = A0;  // potentiometer is connected to analog pin A0
const int ledPin = 3;             // LED is connected to digital pin 3
const int buzzerPin = 11;         // Buzzer is connected to digital pin 11
const int otherLedPin = 10;       // Other LED is connected to digital pin 10

int tempo = 114; 

int melody[] = {

  
  NOTE_E4,4,  NOTE_E4,4,  NOTE_F4,4,  NOTE_G4,4,//1
  NOTE_G4,4,  NOTE_F4,4,  NOTE_E4,4,  NOTE_D4,4,
  NOTE_C4,4,  NOTE_C4,4,  NOTE_D4,4,  NOTE_E4,4,
  NOTE_E4,-4, NOTE_D4,8,  NOTE_D4,2,

  NOTE_E4,4,  NOTE_E4,4,  NOTE_F4,4,  NOTE_G4,4,//4
  NOTE_G4,4,  NOTE_F4,4,  NOTE_E4,4,  NOTE_D4,4,
  NOTE_C4,4,  NOTE_C4,4,  NOTE_D4,4,  NOTE_E4,4,
  NOTE_D4,-4,  NOTE_C4,8,  NOTE_C4,2,

  NOTE_D4,4,  NOTE_D4,4,  NOTE_E4,4,  NOTE_C4,4,//8
  NOTE_D4,4,  NOTE_E4,8,  NOTE_F4,8,  NOTE_E4,4, NOTE_C4,4,
  NOTE_D4,4,  NOTE_E4,8,  NOTE_F4,8,  NOTE_E4,4, NOTE_D4,4,
  NOTE_C4,4,  NOTE_D4,4,  NOTE_G3,2,

  NOTE_E4,4,  NOTE_E4,4,  NOTE_F4,4,  NOTE_G4,4,//12
  NOTE_G4,4,  NOTE_F4,4,  NOTE_E4,4,  NOTE_D4,4,
  NOTE_C4,4,  NOTE_C4,4,  NOTE_D4,4,  NOTE_E4,4,
  NOTE_D4,-4,  NOTE_C4,8,  NOTE_C4,2
  
};

int notes = sizeof(melody) / sizeof(melody[0]) / 2; 
int wholenote = (60000 * 4) / tempo;
int divider = 0, noteDuration = 0;

void setup() {
  pinMode(ledPin, OUTPUT);           // set the LED pin as an output
  pinMode(buzzerPin, OUTPUT);        // set the buzzer pin as an output
  pinMode(potentiometerPin, INPUT); // set the potentiometer pin as an input
  pinMode(otherLedPin, OUTPUT);      // set the other LED pin as an output
}

void loop() {
  // Lógica para ler o valor do potenciômetro e ajustar o LED e o buzzer
  int potentiometerValue = analogRead(potentiometerPin);
  int ledBrightness = map(potentiometerValue, 0, 1023, 0, 255);

  if (potentiometerValue > 800) { 
    tone(buzzerPin, 1000);
    digitalWrite(ledPin, HIGH);
  } else {
    noTone(buzzerPin);
    digitalWrite(ledPin, LOW);
  }

  delay(10);

  // Lógica para manter o LED no pino 10 ligado enquanto o LED no pino 3 estiver desligado
  if (digitalRead(ledPin) == LOW) {
    digitalWrite(otherLedPin, HIGH); // liga o outro LED
  } else {
    digitalWrite(otherLedPin, LOW);  // mantém o outro LED desligado
  }

  // Lógica para tocar a música
  if (digitalRead(ledPin) == HIGH) {
    for (int thisNote = 0; thisNote < notes * 2; thisNote = thisNote + 2) {
      divider = melody[thisNote + 1];
      if (divider > 0) {
        noteDuration = (wholenote) / divider;
      } else if (divider < 0) {
        noteDuration = (wholenote) / abs(divider);
        noteDuration *= 1.5;
      }
      tone(buzzerPin, melody[thisNote], noteDuration * 0.9);
      delay(noteDuration);
      noTone(buzzerPin);
    }
  }
}


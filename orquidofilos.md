// defindindo sensores como constantes inteiras
const int sensor_temperatura = A2;
const int sensor_umidade = A1;
const int sensor_luminosidade = A3;

// Define os LEDs como constantes inteiras
const int led_vermelho = 5;
const int led_amarelo = 6;
const int led_azul = 7;

void setup() {
  //solicitar comunicação serial
  Serial.begin(9600);
  Serial.println("Sistema Ligado");
  
  // Definindo sensores como entrada
  pinMode(sensor_temperatura, INPUT);
  pinMode(sensor_umidade, INPUT);
  pinMode(sensor_luminosidade, INPUT);

  // Definindo os LEDs RGB como saída
  pinMode(led_vermelho, OUTPUT);
  pinMode(led_amarelo, OUTPUT);
  pinMode(led_azul, OUTPUT);
}

void loop() {
  // definindo valores analogRead
  int valor_temperatura = analogRead(sensor_temperatura);
  int valor_LDR = analogRead(sensor_luminosidade);
  int valor_umidade = analogRead(sensor_umidade);
  
  
  // Condição temperatura
  if (valor_temperatura <= 15 && valor_temperatura >= 25) {
    digitalWrite(led_vermelho, HIGH);// acenda o led azul, para dizer que esta tudo ok
    Serial.println("LED Azul: A planta esta otima!Ela esta entra 15 e 25 graus");
    Serial.println(valor_temperatura);
    delay(1000);
  } 
  else {
    digitalWrite(led_vermelho, LOW);
    Serial.println("LED vermelho: A temperatura esta otima");
    Serial.println(valor_temperatura);
  }
  
  // Condição do LDR sensor de luminosidade 
  if(valor_LDR < 600 && valor_LDR > 1023){
    digitalWrite(led_amarelo, HIGH);
    Serial.println( "LED Amarelo: Esta faltando luz na sua planta, coloque ela em um ambiente mais claro");
    Serial.println(valor_LDR);
    delay(1000);
    
  }
  else{
    digitalWrite(led_amarelo, LOW);
    Serial.println("LED amarelo: Sua planta esta com boa luminosidade");
    Serial.println(valor_LDR);
  }

    // Condição sensor de umidade
  if ( valor_umidade > 700 && valor_umidade < 1023) {
    Serial.println("LED AZUL: solo seco, regue sua planta");   
    Serial.println(valor_umidade);
    digitalWrite(led_azul, HIGH);
    delay(1000);
  }
  else{
    digitalWrite(led_azul, LOW);
    Serial.println("LED azul apagado: Solo umido");
    Serial.println(valor_umidade);

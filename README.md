const int carroVerde=8, carroAmarelo=9, carroVermelho=10, pedVermelho=12, pedVerde=11, botao=7;

typedef enum{Janeiro = 1, Fevereiro, Marco, Abril, Maio, Junho, Julho, Agosto, Setembro, Outubro, Novembro, Dezembro}meses;

int LedDelay=1000, cont=0, vetor[2]={0}, a=0,d=0;

typedef struct {
    char rua[30];
    int contagemMes;
}nome;

void dia(int cont){
    vetor[0]= cont/2;
    vetor[1]= vetor[0]/5;
    nome p[2]={{"Rua Condor", 0},{"Rua Uirapuru", 0}};
    p[0].contagemMes=vetor[1];
    p[1].contagemMes=vetor[1];
    mostrarmes(p[0].contagemMes);
    Serial.println(vetor[0]);
}

void mostrarmes(int mes){
  //Testando se o valor está na faixa válida usando os valores da enum
  if((mes >= Janeiro) && (mes <= Dezembro)){
    //switch que determina qual mes será impresso na tela
    switch(mes){
    case Janeiro:
        Serial.println("Janeiro");
    break;
    case Fevereiro:
        Serial.println("Fevereiro");
    break;
    case Marco:
        Serial.println("Marco");
    break;
    case Abril:
        Serial.println("Abril");
    break;
    case Maio:
        Serial.println("Maio");
    break;
    case Junho:
        Serial.println("Junho");
    break;
    case Julho:
        Serial.println("Julho");
    break;
    case Agosto:
        Serial.println("Agosto");
    break;
    case Setembro:
        Serial.println("Setembro");
    break;
    case Outubro:
        Serial.println("Outubro");
    break;
    case Novembro:
        Serial.println("Novembro");
    break;
    case Dezembro:
        Serial.println("Dezembro");
    break;
    }
 }
 else{
    Serial.println("Mais de um ano.");
 }
}

void setup()
{
  Serial.begin(9600);
  
  pinMode(carroVerde, OUTPUT);
  pinMode(carroAmarelo, OUTPUT);
  pinMode(carroVermelho, OUTPUT);
  pinMode(pedVerde, OUTPUT);
  pinMode(pedVermelho, OUTPUT);

  pinMode(botao, INPUT_PULLUP);
}

void loop()
{
while(a<=20){
  digitalWrite(carroVerde, HIGH); // Acende o verde dos carros e o vermelho dos pedestres
  digitalWrite(pedVermelho, HIGH);
  delay(5000); // Aguarda 5 segundos
  digitalWrite(carroVerde, LOW);
  digitalWrite(carroAmarelo, HIGH); // apaga o verde dos carros e acende o amarelo
  delay(3000); // aguarda mais 3 segundos
  digitalWrite(carroAmarelo, LOW); // apaga o amarelo dos carros e acende o vermelho
  digitalWrite(carroVermelho, HIGH);
  digitalWrite(pedVermelho, LOW); // apaga o vermelho dos pedestres e acende o verde
  digitalWrite(pedVerde, HIGH);
  delay(5000);  // aguarda mais 5 segundos
  digitalWrite(pedVerde, LOW);
  for(int x = 0; x<5; x++) // Pisca o vermelho dos pedestres
  {
    digitalWrite(pedVermelho, HIGH);
    delay(250);
    digitalWrite(pedVermelho, LOW);
    delay(250);
  }
  digitalWrite(carroVermelho, LOW);
  cont ++;
  a++;
}
  while(d!=1){
    dia(cont);
    d=1;
  }
}

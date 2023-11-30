# gs1_edge

-Uma breve descrição do problema de saúde abordado.
  O porblema aborado foi a agilidade e priorização do atendimento aos pacientes mais graves que chegam nos hospitais.
  
  Nem sempre o primeiro paciente a chegar é o mais urgente para ser atendido, uma pessoa com uma simples dor de cabeça 
  poderia esperar um pouco mais enquanto pacientes mais graves como um corte aberto ou ate uma parada cardiaca.

  
-Uma visão geral da solução proposta.
  Criei essa solução em  conjunto com a diciplina de Computational Thinking with Python, minha proposta foi desenvolver um sistema
  que pudesse definir o tempo maximo que um paciente poderia esperar de acordo com a gravidade de sua enfermidade.
  
  Na diciplina de python desenvolvi um sistema para definir qual o grau de urgencia no atendimento do paciente de acordo com sua quixa.

  Ja aqui desenvolvi um circuito que pudesse mostrar qual o proximo paciente a ser atendido, um simples botao que mostra em um visor lcd 
  qual o proximo paciente, quando ligado junto ao banco de dados da diciplina de Python pode aumentar a eficiencia de de um ambulatorio lotado,
  o medico saberia exatamente qual o paciente que é deveria ser chamado no momento.


-Instruções claras sobre como configurar e executar a aplicação.
  Quando iniciado o circuito verificar se o potenciometro esta no maximo, depois sera necessario apenas precionar o botão que ja sera mostrado ao
  usuario qual sera o proximo paciente.

  deixei um Serial.print() no codigo para você poder verificar que a lista original é modificada retirando o paciente que acabou de ser chamado,
  fiz dessa forma pois o primeiro paciente pode ser alterado caso surja um paciente mais urgente, logo assim o sistema sempre chama o primeiro paciente
  e nao so percorre uma lista.
  
  Utilizei uma lista de exemplo para fornecer os dados ao circuito, porem quando integrado com o database que seria fornecida pela outra diciplina
  tera uma maior eficiencia 



https://www.tinkercad.com/things/jX74z56ifeT-circuito-gs1?sharecode=Lw7duEscChiq9jaopVpCoEAZS0-TRN-F08D_GBhm2PI

# Codigo fonte:

#include <LiquidCrystal.h>

const int botao = 8;
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

int array[] = {15, 22, 54, 32, 9, 40};
int arrayLength = sizeof(array) / sizeof(array[0]);

void setup()
{
  Serial.begin(9600);
  lcd.begin(16, 2);
  lcd.setCursor(2, 0);
  
  pinMode(botao, INPUT);
}


void loop()
{
  if (digitalRead(botao) == HIGH) {
    proximoPaciente();
    removerPaciente();
    
    delay(1000);
  }
}


void proximoPaciente(){
  	lcd.clear();
  	lcd.print(array[0]);  
}


void removerPaciente() {
  int newArray[arrayLength - 1];

  for (int i = 0; i < arrayLength - 1; ++i) {
    newArray[i] = array[i + 1]; 
  }

  for (int i = 0; i < arrayLength - 1; ++i) {
    array[i] = newArray[i]; 
  }

  for (int i = 0; i < arrayLength; ++i) {
    Serial.print("Numero ");
    Serial.print(i + 1);
    Serial.print(": ");
    Serial.println(array[i]);
  }

  --arrayLength;
}

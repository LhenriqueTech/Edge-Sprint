# Challenge Edge

## Descrição do Projeto:
O projeto tem como objetivo implementar um sistema utilizando arduino e um display LCD 16x2 para gerar códigos aleatórios. Estes códigos são gerados para serem resgatados em nosso site, onde os usuários podem acumular pontos ou benefícios ao inseri-los corretamente.

## Integrantes do grupo
- Pedro Guidotte Rm: 556630
- Cauã Rodrigues Rm: 555373
- Luiz Henrique Rm: 555235 
- Gabriel Ferreira Rm: 556476
- Felipe Xavier Rm: 556931

## Componentes Utilizados:
- 1 Arduino Uno R3
- 1 Placa de Ensaio
- 1 Resistores 220 Ω
- 1 LCD 16x2

## Link do Video
https://youtu.be/H9LZ4ATrQlA

## Link da simulação no Tinkercad
https://www.tinkercad.com/things/a7AgOXCeWFH-daring-robo/editel?sharecode=7dytNADaNq-KCQghysvwfQoB_7QcMLeXm1yZdnp6WZ8

## Código do Projeto:

#include <LiquidCrystal.h>

const int rs = 13, en = 12, d4 = 11, d5 = 10, d6 = 9, d7 = 8;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int Contrast = 0;

String generateRandomCode(int length) {
    const char chars[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    String randomCode = "";
    for (int i = 0; i < length; ++i) {
        randomCode += chars[random(0, sizeof(chars) - 1)];
    }
    return randomCode;
}

void setup() {
    Serial.begin(9600);
    analogWrite(6, Contrast);
    lcd.begin(16, 2);
    randomSeed(analogRead(0)); 
}

void loop() {
    int count;
    lcd.setCursor(0, 0);
    lcd.print("Resgate o codigo");
    lcd.setCursor(0, 1);
    lcd.print("e ganhe pontos: ");

    for (count = 5; count > 0; count--) {
        lcd.setCursor(15, 1); 
        lcd.print(" "); 
        lcd.setCursor(15, 1);
        lcd.print(count);
        delay(1000);
    }

    lcd.clear();

    String randomCode = generateRandomCode(8);
    lcd.setCursor(0, 0);
    lcd.print("Codigo:");
    lcd.setCursor(0, 1);
    lcd.print(randomCode);
    delay(10000); 

    lcd.clear();

    lcd.setCursor(0, 0);
    lcd.print("Obrigado!");
    delay(5000);
    lcd.clear();
}


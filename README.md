# -Menu-Interativo-
## Primeira atividade sobre menus interativos, realizada dia 11/05/2026. 


    import javax.swing.*;
    void main() {
    int opcaoPrincipal = -1;
    String entrada;
    while (opcaoPrincipal != 0) {
        String menu = "        MENU PRINCIPAL\n"
                + " 1) Conversor de Temperatura\n"
                + " 2) Cálculo de Fatorial\n"
                + " 3) Média de Notas\n"
                + " 4) Horário Internacional\n"
                + " 0) Encerrar Programa\n\n"
                + "Escolha uma opção:";
        entrada = JOptionPane.showInputDialog(null, menu, "Menu", JOptionPane.QUESTION_MESSAGE);
        if (entrada == null) break;
        opcaoPrincipal = Integer.parseInt(entrada);
        switch (opcaoPrincipal) {
            case 1:
                int de = Integer.parseInt(JOptionPane.showInputDialog("Escala de Origem:\n1-Celsius | 2-Fahrenheit | 3-Kelvin "));
                int para = Integer.parseInt(JOptionPane.showInputDialog("Escala de Destino:\n1-Celsius | 2-Fahrenheit | 3-Kelvin "));
                double temp = Double.parseDouble(JOptionPane.showInputDialog("Digite o valor da temperatura:"));
                double result = 0;
                if (de == 1 && para == 2) result = (temp * 9 / 5) + 32;
                else if (de == 2 && para == 1) result = (temp - 32) * 5 / 9;
                else if (de == 1 && para == 3) result = temp + 273.15;
                else if (de == 3 && para == 1) result = temp - 273.15;
                else if (de == 2 && para == 3) result = (temp - 32) * 5 / 9 + 273.15;
                else if (de == 3 && para == 2) result = (temp - 273.15) * 9 / 5 + 32;
                else if (de == para) result = temp;
                else {
                    JOptionPane.showMessageDialog(null, "Escalas inválidas.", "Erro", JOptionPane.ERROR_MESSAGE);
                    break;
                }
                JOptionPane.showMessageDialog(null, String.format("Resultado: %.2f", result));
                break;
            case 2:
                int numFact = Integer.parseInt(JOptionPane.showInputDialog("Digite um número inteiro positivo:"));
                if (numFact < 0) {
                    JOptionPane.showMessageDialog(null, "Erro: O número deve ser positivo.");
                } else {
                    long fat = 1;
                    int i = numFact;
                    while (i > 1) fat *= i--;
                    JOptionPane.showMessageDialog(null, numFact + "! = " + fat);
                }
                break;
            case 3:
                int qtd = Integer.parseInt(JOptionPane.showInputDialog("Quantas notas deseja informar?"));
                double soma = 0;
                int cont = 1;
                while (cont <= qtd) {
                    soma += Double.parseDouble(JOptionPane.showInputDialog("Digite a nota " + cont + ":"));
                    cont++;
                }
                JOptionPane.showMessageDialog(null, String.format("Média Final: %.2f", (soma / qtd)));
                break;
            case 4:
                double horarioInformado = Double.parseDouble(JOptionPane.showInputDialog("Hora do Brasil (Ex: 14.30 para 14h30 ou 23.59):"));
                int horaBR = (int) horarioInformado;
                double minutos = horarioInformado - horaBR;
                if (horaBR < 0 || horaBR >= 24 || minutos >= 0.60) {
                    JOptionPane.showMessageDialog(null, "Hora ou minutos inválidos. Use o formato HH.MM (minutos até 59).");
                } else {
                    int horaEUA = horaBR - 1;
                    if (horaEUA < 0) horaEUA += 24;
                    int horaEuropa = horaBR + 4;
                    if (horaEuropa >= 24) horaEuropa -= 24;
                    int horaJapao = horaBR + 12;
                    String sufixoJapao = "";
                    if (horaJapao >= 24) {
                        horaJapao -= 24;
                        sufixoJapao = " (dia seguinte)";
                    }
                    String out = "Horários Convertidos:\n"
                            + String.format("- Brasil: %.2fh\n", horaBR + minutos)
                            + String.format("- EUA (NY): %.2fh\n", horaEUA + minutos)
                            + String.format("- França/Alemanha/Itália: %.2fh\n", horaEuropa + minutos)
                            + String.format("- Japão: %.2fh%s", horaJapao + minutos, sufixoJapao);
                    JOptionPane.showMessageDialog(null, out, "Fusos Horários", JOptionPane.INFORMATION_MESSAGE);
                }
                break;
            case 0:
                JOptionPane.showMessageDialog(null, "O sistema foi encerrado. Até logo!");
                break;
            default:
                JOptionPane.showMessageDialog(null, "Opção inválida! Retornando...", "Erro",
                        JOptionPane.WARNING_MESSAGE);
                break;
        }
    }
}

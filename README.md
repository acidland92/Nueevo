/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pishing;

import java.io.*;
import java.util.*;

/**
 *
 * @author Usuario
 */
public class Pishing {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        Map<String, Integer> texto = inicializarTexto();
        String filePath = "C:/Users/Usuario/Documents/NetBeansProjects/Pishing/src/pishing/pishing.txt";
        int totalPuntos = 0;

        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;

            while ((line = reader.readLine()) != null) {
                totalPuntos += proceso(line, texto);
            }

            TotalPuntos(totalPuntos);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static Map<String, Integer> inicializarTexto() {
        Map<String, Integer> texto = new HashMap<>();
        texto.put("Enhora buena", 1);
        texto.put("Cuidado", 1);
        texto.put("usted a sido seleccionado", 3);
        texto.put("Gane dinero facil", 2);
        texto.put("por este mes", 1);
        texto.put("¡Importante! Su contraseña está a punto de expirar", 3);
        texto.put("Acción requerida", 2);
        texto.put("Se ha identificado una vulnerabilidad", 3);
        texto.put("Se requiere un cambio de contraseña inmediatamente", 3);
        texto.put("Verificación de cuenta", 2);
        texto.put("Contraseña expirada", 3);
        texto.put("Actividad sospechosa", 2);
        texto.put("Urgente: accione de inmediato", 3);
        texto.put("Actualice sus datos", 3);
        texto.put("phishing", 3);
        texto.put("contraseña", 2);
        texto.put("urgente", 2);
        texto.put("Google", 3);
        texto.put("Whatsapp", 3);
        texto.put("Netflix", 3);
        texto.put("Facebook", 3);
        texto.put("Gmail", 3);
        texto.put("Instagram", 3);
        texto.put("¡Necesito ayuda urgente!", 3);
        texto.put("Actividad sospechosa de Outlook", 1);
        texto.put("Inicie sesión para evitar el bloqueo", 3);
        texto.put("Su cuenta ha sido comprometida", 3);
        texto.put("Gane dinero rápido", 2);
        texto.put("Oferta exclusiva", 3);

        return texto;
    }
    private static int proceso(String line, Map<String, Integer> keywords) {
        int total = 0;

        for (Map.Entry<String, Integer> entry : keywords.entrySet()) {
            String keyword = entry.getKey();
            int puntos = entry.getValue();
            int ocurrencias = Ocurrencias(line, keyword);

            if (ocurrencias > 0) {
                total += ocurrencias * puntos;
                palabrasInfo(keyword, ocurrencias, ocurrencias * puntos);
            }
        }

        return total;
    }
    private static int Ocurrencias(String line, String texto) {
        int ocurrencias = 0;
        int index = line.indexOf(texto);

        while (index != -1) {
            ocurrencias++;
            index = line.indexOf(texto, index + 1);
        }

        return ocurrencias;
    }
    private static void palabrasInfo(String texto, int ocurrencias, int puntos){
        System.out.println("Palabra o frase: " + texto + ", Ocurrencias: " + ocurrencias + ", Puntos: " + puntos);
    }
    private static void TotalPuntos(int totalPuntos){
        System.out.println("---------------------------------------");
        System.out.println("Total de Puntos: " + totalPuntos);
    }
}

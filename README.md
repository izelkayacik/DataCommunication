# data-communication

Client Kodları:

package socketapp;
 
import java.io.*;
import java.net.*;
 
public class client {
 
     public static void main(String[] args) throws IOException {
          islem();
     }
 
     public static void islem() throws UnknownHostException, IOException {
          Socket socket = null;
          PrintWriter out = null;
          BufferedReader in = null;
          String deger;
          try {           
               socket = new Socket("37.155.9.77");
          } catch (Exception e) {
               System.out.println("Port Hatası!");
          }
          out = new PrintWriter(socket.getOutputStream(), true);
          in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
 
          System.out.println("Server'a gönderilecek sayısı giriniz:");

          BufferedReader data = new BufferedReader(new InputStreamReader(System.in));
 
          while((deger = data.readLine()) != null) {
               out.println(deger);
               System.out.println("Server'dan gelen sonuç = " + in.readLine());
               System.out.println("Server'a gönderilecek saysı giriniz");
          }
          out.close();
          in.close();
          data.close();
          socket.close();
     }
}

Server Kodları:
package socketapp;
 
import java.io.*;
import java.net.*;
 
public class server {
 
     public static void main(String[] args) throws IOException {
          String clientGelen;
          ServerSocket serverSocket = null;
          Socket clientSocket = null;
 
          int sayi;
 
          try {
               serverSocket = new ServerSocket(3389);
          } catch (Exception e) {
               System.out.println("Port Hatası!");
          }
          System.out.println("SERVER BAŞLANTI İÇİN HAZIR...");
          
          clientSocket = serverSocket.accept();
          
          PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);
 

          BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
 
          while((clientGelen = in.readLine()) != null) {
               System.out.println("Client'dan gelen veri = " + clientGelen);
               sayi = Integer.valueOf(clientGelen);
               out.println(sayi*sayi);
          }
          out.close();
          in.close();
          clientSocket.close();
          serverSocket.close();
     }
}

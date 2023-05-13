import java.util.Scanner;
import java.io.IOException;

class Console {

    public static void clear(String... arg) throws IOException, InterruptedException {
        new ProcessBuilder("cmd", "/c", "cls").inheritIO().start().waitFor();
    }
}

class ContaBancaria {
   
  static double saldo;  

  public static void topo()throws IOException, InterruptedException {
	Scanner teclado = new Scanner(System.in);       
    Console console = new Console();  
	console.clear();
	
	System.out.print("\n_____________________________________________________________\n\n");
    System.out.print("__________________________$-BANCO NEXT-$_____________________\n\n");
    System.out.print("_____________________________________________________________\n\n");
  }
  public static void pressioneParaMenu()throws IOException, InterruptedException { 
	System.out.print("-Pressione enter para voltar ao menu principal-");
	System.in.read();
  }
  public static boolean validarSangria(double valor){    
    
    if(valor > saldo){
      return false;
    }
    
    return true;
  }
  
  public static void reforcoSaldo(double valor){
    saldo = saldo + valor;
  }
  public static void sangriaSaldo(double valor){
    saldo = saldo - valor;
  }
    
  public static void depositar()throws IOException, InterruptedException{
      Scanner teclado = new Scanner(System.in);
	  	  
      
      double valor;
      
	  topo();
	  System.out.print("_______________________\n\n");
	  System.out.print("| Saldo atual: \n");
	  System.out.print("| R$ " + saldo + "\n");
	  System.out.print("_______________________\n\n");
	  
      System.out.print(" Qual a quantia que voce eseja depositar? \n\n");
	  System.out.print("\n R$ ");
      
      valor = teclado.nextDouble();
      
      reforcoSaldo(valor);
	  
	  topo();
	  System.out.print("_______________________\n\n");
	  System.out.print("| Saldo atual: \n");
	  System.out.print("| R$ " + saldo + "\n");
	  System.out.print("_______________________\n\n");
	  
	  System.out.print(" Deposito feito com sucesso! \n\n");
	  
	  pressioneParaMenu();
	  
  }
  
  public static double sacar()throws IOException, InterruptedException{
      Scanner teclado = new Scanner(System.in);
	  	  
      
      double valor;
	  
	  topo();
	  System.out.print("_______________________\n\n");
	  System.out.print("| Saldo atual: \n");
	  System.out.print("| R$ " + saldo + "\n");
	  System.out.print("_______________________\n\n");
	  
      System.out.print(" Qual a quantia necessaria que deseja sacar? \n\n");
	  System.out.print("\n R$ ");
      
      valor = teclado.nextDouble();
	  
	  sangriaSaldo(valor);
	  
	   topo();
	  System.out.print("_______________________\n\n");
	  System.out.print("| Saldo atual: \n");
	  System.out.print("| R$ " + saldo + "\n");
	  System.out.print("_______________________\n\n");
	  
	  System.out.print(" Saque feito com sucesso! \n\n");
	  
	  pressioneParaMenu();
	  
	  
      if(validarSangria(valor) == false){
        System.out.print(" Saldo insuficiente! \n\n");
        menu();
      }
	  
      return saldo;
  } 
  
  public static double exibirSaldo()throws IOException, InterruptedException{
	  
	topo();
      System.out.print("_______________________\n\n");
	  System.out.print("| Saldo atual: \n");
	  System.out.print("| R$ " + saldo + "\n");
	  System.out.print("_______________________\n\n");
	
    pressioneParaMenu();
	
    return saldo;
  }
  
  public static void menu()throws IOException, InterruptedException{
    Scanner teclado = new Scanner(System.in);   

    int opcao;
	
	topo();
    System.out.print("\n Porfavor seleciona o que deseja: \n\n");
    System.out.print("_____________________________________________________________\n\n");
    System.out.print(" [1] - Depositar na conta \n\n");
    System.out.print(" [2] - Sacar da conta \n\n");
    System.out.print(" [3] - Exibir saldo da conta \n\n");
    System.out.print(" [4] - Sair do sistema bancario \n");
	System.out.print("_____________________________________________________________\n\n");
	
    opcao = teclado.nextInt();
	Console console = new Console();  
	console.clear();
	    
    switch (opcao) {
      case 1:
      depositar();
	  menu();
      break;

      case 2:
      sacar();
      menu();
      break;

      case 3:
      exibirSaldo();
      menu();
      break;

      case 4:
      encerrarSistema();
      break;

    default:
      System.out.printf("Porfavor inserir uma opcao valida!");
    }
    
  }
  public static void encerrarSistema() throws IOException, InterruptedException{
	  
	topo();
	System.out.print("____________________________________________________________\n");
	System.out.print("Obrigada pela preferencia, te vejo em sua proxima visita! \n\n");
	System.out.print("____________________________________________________________\n");
	System.out.print("Estaremos encerrando automaticamente em 5 segundos!...... \n\n");
	System.out.print("____________________________________________________________\n");
	Thread.currentThread().sleep(5000);   
	Console console = new Console();  
	console.clear();
    System.exit(0);
	
  }

	public static void main(String args[]) throws IOException, InterruptedException {  

    saldo = 0;

    menu();    
       
    System.exit(0);
		
	}

}

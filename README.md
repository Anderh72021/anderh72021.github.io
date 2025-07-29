import java.util.*;

public class SistemaVentas {
    private Comprador compradorActual;
    private List<Localidad> localidades;
    private Random random;
    
    public SistemaVentas() {
        this.localidades = new ArrayList<>();
        localidades.add(new Localidad(1, 100, 20));
        localidades.add(new Localidad(5, 500, 20));
        localidades.add(new Localidad(10, 1000, 20));
        this.random = new Random();
    }
    
    public static void main(String[] args) {
        SistemaVentas sistema = new SistemaVentas();
        sistema.mostrarMenu();
    }
    
    public void mostrarMenu() {
        Scanner scanner = new Scanner(System.in);
        int opcion;
        
        do {
            System.out.println("\n--- MENÚ THE ERAS TOUR ---");
            System.out.println("1. Nuevo comprador");
            System.out.println("2. Nueva solicitud de boletos");
            System.out.println("3. Consultar disponibilidad total");
            System.out.println("4. Consultar disponibilidad individual");
            System.out.println("5. Reporte de caja");
            System.out.println("6. Salir");
            System.out.print("Seleccione una opción: ");
            
            opcion = scanner.nextInt();
            procesarOpcion(opcion);
        } while (opcion != 6);
    }
    
    private void procesarOpcion(int opcion) {
        switch (opcion) {
            case 1:
                nuevoComprador();
                break;
            case 2:
                nuevaSolicitudBoletos();
                break;
            case 3:
                consultarDisponibilidadTotal();
                break;
            case 4:
                consultarDisponibilidadIndividual();
                break;
            case 5:
                generarReporteCaja();
                break;
            case 6:
                System.out.println("Saliendo del sistema...");
                break;
            default:
                System.out.println("Opción no válida");
        }
    }
    
    private void nuevoComprador() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Ingrese nombre: ");
        String nombre = scanner.nextLine();
        System.out.print("Ingrese email: ");
        String email = scanner.nextLine();
        System.out.print("Ingrese cantidad de boletos: ");
        int cantidad = scanner.nextInt();
        System.out.print("Ingrese presupuesto máximo: ");
        double presupuesto = scanner.nextDouble();
        
        this.compradorActual = new Comprador(nombre, email, cantidad, presupuesto);
        System.out.println("Comprador registrado exitosamente!");
    }
    
    // Implementar los demás métodos según las especificaciones
}

class Comprador {
    private String nombre;
    private String email;
    private int cantidadBoletos;
    private double presupuesto;
    private int numeroTicket;
    
    public Comprador(String nombre, String email, int cantidadBoletos, double presupuesto) {
        this.nombre = nombre;
        this.email = email;
        this.cantidadBoletos = cantidadBoletos;
        this.presupuesto = presupuesto;
    }
    
    public void solicitarCompra() {
        Random random = new Random();
        this.numeroTicket = random.nextInt(15000) + 1;
    }
    
    public boolean esTicketApto() {
        Random random = new Random();
        int a = random.nextInt(15000) + 1;
        int b = random.nextInt(15000) + 1;
        
        int min = Math.min(a, b);
        int max = Math.max(a, b);
        
        return this.numeroTicket >= min && this.numeroTicket <= max;
    }
    
    // Getters
    public String getNombre() { return nombre; }
    public String getEmail() { return email; }
    public int getCantidadBoletos() { return cantidadBoletos; }
    public double getPresupuesto() { return presupuesto; }
    public int getNumeroTicket() { return numeroTicket; }
}

class Localidad {
    private int numero;
    private double precio;
    private int capacidad;
    private int boletosVendidos;
    
    public Localidad(int numero, double precio, int capacidad) {
        this.numero = numero;
        this.precio = precio;
        this.capacidad = capacidad;
        this.boletosVendidos = 0;
    }
    
    public boolean venderBoletos(int cantidad, double presupuesto) {
        if (presupuesto < precio * cantidad) return false;
        if (boletosVendidos + cantidad > capacidad) return false;
        
        boletosVendidos += cantidad;
        return true;
    }
    
    public int getDisponibilidad() {
        return capacidad - boletosVendidos;
    }
    
    public int getTotalVendido() {
        return boletosVendidos;
    }
    
    public double getPrecio() {
        return precio;
    }
    
    public int getNumero() {
        return numero;
    }
}

 import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// ======================================================
// CLASSE PARTICIPANTE
// ======================================================
class Participante {
    private int id;
    private String nome;
    private String cpf;

    public Participante(int id, String nome, String cpf) {
        this.id = id;
        this.nome = nome;
        this.cpf = cpf;
    }

    public int getId() { return id; }
    public String getNome() { return nome; }
    public String getCpf() { return cpf; }

    @Override
    public String toString() {
        return "ID: " + id + " | Nome: " + nome + " | CPF: " + cpf;
    }
}

// ======================================================
// CLASSE EVENTO (SUPERCLASSE)
// ======================================================
class Evento {
    protected int id;
    protected String titulo;
    protected String dataInicio;
    protected String dataFim;
    protected String horarioInicio;
    protected String horarioFim;
    protected List<Participante> participantes = new ArrayList<>();

    public Evento(int id, String titulo, String dataInicio, String dataFim,
                  String horarioInicio, String horarioFim) {
        this.id = id;
        this.titulo = titulo;
        this.dataInicio = dataInicio;
        this.dataFim = dataFim;
        this.horarioInicio = horarioInicio;
        this.horarioFim = horarioFim;
    }

    public int getId() { return id; }

    public void adicionarParticipante(Participante p) {
        participantes.add(p);
    }

    public void listarParticipantes() {
        if (participantes.isEmpty()) {
            System.out.println("Nenhum participante cadastrado.");
        } else {
            for (Participante p : participantes) {
                System.out.println(p);
            }
        }
    }

    @Override
    public String toString() {
        return "EVENTO: " + titulo + " | ID: " + id +
               "\nData: " + dataInicio + " a " + dataFim +
               "\nHorário: " + horarioInicio + " às " + horarioFim;
    }
}

// ======================================================
// CLASSE EVENTO PRESENCIAL (SUBCLASSE)
// ======================================================
class EventoPresencial extends Evento {
    private String local;
    private int capacidade;

    public EventoPresencial(int id, String titulo, String dataInicio, String dataFim,
                            String horarioInicio, String horarioFim,
                            String local, int capacidade) {

        super(id, titulo, dataInicio, dataFim, horarioInicio, horarioFim);
        this.local = local;
        this.capacidade = capacidade;
    }

    @Override
    public String toString() {
        return super.toString() +
               "\nLocal: " + local +
               "\nCapacidade: " + capacidade;
    }
}

// ======================================================
// CLASSE EVENTO ONLINE (SUBCLASSE)
// ======================================================
class EventoOnline extends Evento {
    private String link;
    private String plataforma;

    public EventoOnline(int id, String titulo, String dataInicio, String dataFim,
                        String horarioInicio, String horarioFim,
                        String link, String plataforma) {

        super(id, titulo, dataInicio, dataFim, horarioInicio, horarioFim);
        this.link = link;
        this.plataforma = plataforma;
    }

    @Override
    public String toString() {
        return super.toString() +
               "\nLink: " + link +
               "\nPlataforma: " + plataforma;
    }
}

// ======================================================
// PROGRAMA PRINCIPAL
// ======================================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        Evento evento = null;  
        
        while (true) {
            System.out.println("\n====== MENU ======");
            System.out.println("1 - Criar evento presencial");
            System.out.println("2 - Criar evento online");
            System.out.println("3 - Cadastrar participante");
            System.out.println("4 - Listar participantes");
            System.out.println("5 - Exibir evento");
            System.out.println("0 - Sair");
            System.out.print("Escolha: ");

            int op = sc.nextInt();
            sc.nextLine();

            if (op == 1) {

                System.out.print("ID: ");
                int id = sc.nextInt(); sc.nextLine();
                System.out.print("Título: ");
                String titulo = sc.nextLine();
                System.out.print("Data início: ");
                String di = sc.nextLine();
                System.out.print("Data fim: ");
                String df = sc.nextLine();
                System.out.print("Horário início: ");
                String hi = sc.nextLine();
                System.out.print("Horário fim: ");
                String hf = sc.nextLine();
                System.out.print("Local: ");
                String local = sc.nextLine();
                System.out.print("Capacidade: ");
                int cap = sc.nextInt(); sc.nextLine();

                evento = new EventoPresencial(id, titulo, di, df, hi, hf, local, cap);
                System.out.println("Evento presencial criado!");

            } else if (op == 2) {

                System.out.print("ID: ");
                int id = sc.nextInt(); sc.nextLine();
                System.out.print("Título: ");
                String titulo = sc.nextLine();
                System.out.print("Data início: ");
                String di = sc.nextLine();
                System.out.print("Data fim: ");
                String df = sc.nextLine();
                System.out.print("Horário início: ");
                String hi = sc.nextLine();
                System.out.print("Horário fim: ");
                String hf = sc.nextLine();
                System.out.print("Link: ");
                String link = sc.nextLine();
                System.out.print("Plataforma: ");
                String plat = sc.nextLine();

                evento = new EventoOnline(id, titulo, di, df, hi, hf, link, plat);
                System.out.println("Evento online criado!");

            } else if (op == 3) {
                if (evento == null) {
                    System.out.println("Crie um evento antes!");
                } else {
                    System.out.print("ID participante: ");
                    int id = sc.nextInt(); sc.nextLine();
                    System.out.print("Nome: ");
                    String nome = sc.nextLine();
                    System.out.print("CPF: ");
                    String cpf = sc.nextLine();

                    Participante p = new Participante(id, nome, cpf);
                    evento.adicionarParticipante(p);
                    System.out.println("Participante cadastrado!");
                }

            } else if (op == 4) {
                if (evento != null) evento.listarParticipantes();
                else System.out.println("Nenhum evento criado!");

            } else if (op == 5) {
                if (evento != null) System.out.println("\n" + evento);
                else System.out.println("Nenhum evento criado!");

            } else if (op == 0) {
                break;
            }
        }
        sc.close();
    }
}.util.List;
import java.util.Scanner;

// ====================== CLASSE BASE (SUPERCLASSE) =========================
// 👉 Troque o nome "Animal" por outro conforme o tema da prova (ex: Veiculo, Paciente, Aluno)
class Animal {
    private int numeroRegistro;
    private String nome;
    private int idade;
    private double peso;

    public Animal(int numeroRegistro, String nome, int idade, double peso) {
        this.numeroRegistro = numeroRegistro;
        this.nome = nome;
        this.idade = idade;
        this.peso = peso;
    }

    public int getNumeroRegistro() { return numeroRegistro; }
    public String getNome() { return nome; }
    public int getIdade() { return idade; }
    public double getPeso() { return peso; }

    public void setNome(String nome) { this.nome = nome; }
    public void setIdade(int idade) { this.idade = idade; }
    public void setPeso(double peso) { this.peso = peso; }

    // 👉 Exemplo de método comum para exibir dados
    public void exibirInfo() {
        System.out.println("Registro: " + numeroRegistro);
        System.out.println("Nome: " + nome);
        System.out.println("Idade: " + idade);
        System.out.println("Peso: " + peso);
    }

    // 👉 Exemplo de cálculo (pode ser seguro, valor, pontuação etc.)
    public double calcularSeguro() {
        return (idade * peso * 1000) / 2;
    }
}

// ====================== CLASSE DERIVADA (HERANÇA) =========================
// 👉 Exemplo: Tigre, AlunoEspecial, Carro, etc.
class Tigre extends Animal {
    private String origem;

    public Tigre(int numeroRegistro, String nome, int idade, double peso, String origem) {
        super(numeroRegistro, nome, idade, peso);
        this.origem = origem;
    }

    @Override
    public void exibirInfo() {
        super.exibirInfo();
        System.out.println("Origem: " + origem);
    }
}

// ====================== CLASSE DE AGRUPAMENTO (COMPOSIÇÃO) =========================
// 👉 Exemplo: Jaula, Turma, Frota, Departamento, etc.
class Jaula {
    private int id;
    private String tamanho;
    private List<Animal> animais = new ArrayList<>();

    public Jaula(int id, String tamanho) {
        this.id = id;
        this.tamanho = tamanho;
    }

    public int getId() { return id; }
    public String getTamanho() { return tamanho; }

    // 👉 Adiciona um animal
    public void adicionarAnimal(Animal a) {
        animais.add(a);
        System.out.println("Animal adicionado com sucesso!");
    }

    // 👉 Lista todos os animais
    public void listarAnimais() {
        if (animais.isEmpty()) {
            System.out.println("Nenhum animal na jaula.");
        } else {
            for (Animal a : animais) {
                a.exibirInfo();
                System.out.println("-------------------------");
            }
        }
    }

    // 👉 Busca animal por número de registro
    public Animal buscarAnimal(int numeroRegistro) {
        for (Animal a : animais) {
            if (a.getNumeroRegistro() == numeroRegistro) {
                return a;
            }
        }
        return null;
    }

    // 👉 Remove animal por número de registro
    public void removerAnimal(int numeroRegistro) {
        Animal encontrado = buscarAnimal(numeroRegistro);
        if (encontrado != null) {
            animais.remove(encontrado);
            System.out.println("Animal removido com sucesso!");
        } else {
            System.out.println("Animal não encontrado.");
        }
    }
}

// ====================== CLASSE PRINCIPAL (COM SCANNER) =========================
public class SistemaZoologico {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 👉 Cria uma jaula
        System.out.print("Digite o ID da jaula: ");
        int id = sc.nextInt();
        sc.nextLine();
        System.out.print("Digite o tamanho da jaula: ");
        String tamanho = sc.nextLine();

        Jaula jaula = new Jaula(id, tamanho);

        int opcao;
        do {
            System.out.println("\n========= MENU =========");
            System.out.println("1 - Adicionar Tigre");
            System.out.println("2 - Listar Animais");
            System.out.println("3 - Buscar Animal por Registro");
            System.out.println("4 - Remover Animal");
            System.out.println("5 - Calcular Seguro de um Animal");
            System.out.println("0 - Sair");
            System.out.print("Escolha: ");
            opcao = sc.nextInt();

            switch (opcao) {
                case 1:
                    System.out.print("Número de registro: ");
                    int num = sc.nextInt();
                    sc.nextLine();
                    System.out.print("Nome: ");
                    String nome = sc.nextLine();
                    System.out.print("Idade: ");
                    int idade = sc.nextInt();
                    System.out.print("Peso: ");
                    double peso = sc.nextDouble();
                    sc.nextLine();
                    System.out.print("Origem: ");
                    String origem = sc.nextLine();

                    Tigre t = new Tigre(num, nome, idade, peso, origem);
                    jaula.adicionarAnimal(t);
                    break;

                case 2:
                    jaula.listarAnimais();
                    break;

                case 3:
                    System.out.print("Digite o número de registro: ");
                    int busca = sc.nextInt();
                    Animal encontrado = jaula.buscarAnimal(busca);
                    if (encontrado != null) {
                        encontrado.exibirInfo();
                    } else {
                        System.out.println("Animal não encontrado.");
                    }
                    break;

                case 4:
                    System.out.print("Número de registro do animal a remover: ");
                    int rem = sc.nextInt();
                    jaula.removerAnimal(rem);
                    break;

                case 5:
                    System.out.print("Número de registro para cálculo de seguro: ");
                    int reg = sc.nextInt();
                    Animal a = jaula.buscarAnimal(reg);
                    if (a != null) {
                        System.out.println("Valor do seguro: R$ " + a.calcularSeguro());
                    } else {
                        System.out.println("Animal não encontrado.");
                    }
                    break;

                case 0:
                    System.out.println("Encerrando o sistema...");
                    break;

                default:
                    System.out.println("Opção inválida!");
            }
        } while (opcao != 0);

        sc.close();
    }
}



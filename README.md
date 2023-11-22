# RubricaWpf
```
public MainWindow()
        {
            InitializeComponent();
            Contatto[] Contatti = new Contatto[100];
            try  
            {
                for (int i = 0; i < Contatti.Length; i++)
                {
                    Contatti[i] = new Contatto();
                }
                StreamReader fin = new StreamReader("Dati.csv");
                int idx = 0;
                while (!fin.EndOfStream)
                {
                    string? riga = fin.ReadLine();
                    Contatti[idx] = new Contatto(riga);
                    idx++;
                }
                dgDati.ItemsSource = Contatti;
            }
            catch (Exception ex)
            {
                MessageBox.Show("Errore: " + ex.Message);
            }
        }

        private void dgDati_LoadingRow(object sender, DataGridRowEventArgs e)
        {
            Contatto c = e.Row.Item as Contatto;
            if (c != null)
            {
                if (c.Pk == 0)
                {
                    e.Row.Background = Brushes.Red;
                    e.Row.Foreground = Brushes.White;
                }
            }

```

Nel codice di MainWindow.cs, nel metodo InitializeComponent(), stiamo preparando la finestra dell'applicazione. Creiamo un vettore di 100 contatti e gestiamo eventuali problemi che possono verificarsi durante questo processo. Utilizziamo un ciclo "for" per riempire questo vettore con oggetti Contatto. Successivamente, apriamo un file chiamato "Dati.csv" per leggerne il contenuto e iniziamo un contatore chiamato "idx" a zero per tener traccia degli indici nel vettore.

All'interno di un ciclo "while", leggiamo ogni riga del file e la memorizziamo nel nostro vettore. Nel caso si verifichino problemi durante questo processo, catturiamo l'errore e mostriamo un messaggio a schermo per informare l'utente.

In un altro pezzo di codice, stiamo gestendo l'aspetto visivo di ogni riga nel DataGrid. Otteniamo l'oggetto Contatto associato alla riga corrente e verifichiamo se la chiave primaria (Pk) è uguale a zero. Se è così, cambiamo lo sfondo e il testo della riga per evidenziarla.

```
class Contatto
    {
        private int pk;
        private string nome;
        private string cognome;
        private string numero;
        private string indirizzo;
        private string mail;

        public int Pk { get => pk; set => pk = value; }
        public string Nome { get => nome; set => nome = value; }
        public string Cognome { get => cognome; set => cognome = value; }
        public string Numero { get => numero; set => numero = value; }
        
        public string Mail { get => mail; set => mail = value; }
        public string Indirizzo { get => indirizzo; set => indirizzo = value; }
        

        public Contatto(string riga)
        {

            string[] campi = riga.Split(';');
            
            if (int.TryParse(campi[0], out int res) && campi.Length==5) {
                this.pk = res;
                this.Nome = campi[1];
                this.Cognome = campi[2];
                this.numero = campi[3];
                this.mail = campi[4];
            }
            else
                this.pk = 0;



        }

        public Contatto()
        {
        }
    }
```

All'interno della classe Contatto, stiamo definendo diverse informazioni che vogliamo memorizzare per ogni contatto. Queste informazioni includono una chiave primaria (pk), il nome, il cognome, il numero di telefono, l'indirizzo e l'email.

Per rendere accessibili queste informazioni, stiamo creando delle "caselle" private per ciascuna di esse. Ad esempio, abbiamo una casella privata per la chiave primaria (pk), una per il nome (nome), una per il cognome (cognome), e così via.

Successivamente, stiamo creando delle "finestre" pubbliche attraverso le quali è possibile vedere e modificare queste informazioni. Queste finestre sono chiamate "proprietà" e sono create attraverso i metodi get e set. Ad esempio, con public int Pk { get => pk; set => pk = value; }, stiamo creando una finestra attraverso la quale possiamo vedere e modificare il valore della chiave primaria (pk) del contatto.

Abbiamo anche due modi di "costruire" un oggetto Contatto:

Il primo modo è fornendo una stringa che rappresenta tutti i dati di un contatto. Questo è fatto attraverso il costruttore public Contatto(string riga). Questo metodo prende la stringa, la divide in diverse parti usando il punto e virgola come separatore e utilizza queste parti per inizializzare i campi del nostro contatto, come chiave primaria, nome, cognome, numero di telefono e email.

Il secondo modo è utilizzando un costruttore predefinito public Contatto(), che non richiede alcun dato iniziale. Questo costruttore è utile quando vogliamo creare un nuovo contatto senza specificare immediatamente i dettagli. In questo caso, possiamo assegnare i valori dei campi successivamente, se necessario.


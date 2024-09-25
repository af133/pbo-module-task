using System;
using System.Collections.Generic;
using System.Runtime.InteropServices.Marshalling;
using System.Security.Cryptography.X509Certificates;

class Program
{
    static void Main(string[] args)
    {
        Singa singa = new Singa("Simba", 5, 4);//buat objek baru Singa
        Gajah gajah = new Gajah("Dumbo", 8, 4);//buat objek baru Gajah
        Ular ular = new Ular("Python", 3, 6.5);//buat objek baru Ular
        Buaya buaya = new Buaya("Croc", 12, 5.0);//buat objek baru Buaya
        KebunBinatang kebunBinatang = new KebunBinatang();//buat objek baru kebunBinatang
        singa.Suara();//menghasilkan ini singa
        ular.Suara();//menghasilkan ini ular
        singa.Mengaum();//menghasilkan kharrr...
        ular.Merayap();//menghasilkan Merayap:Ssss...
        kebunBinatang.TambahHewan(singa);//menambahkan objek singa di dalam objek KebunBinatang
        kebunBinatang.TambahHewan(gajah);//menambahkan objek gajah di dalam objek KebunBinatang
        kebunBinatang.TambahHewan(ular);//menambahkan objek ulaar di dalam objek KebunBinatang
        kebunBinatang.TambahHewan(buaya);//menambahkan objek buaya di dalam objek KebunBinatang

        kebunBinatang.TampilkanKoleksi();
    }

    //---------- Hewan ----------
    class Hewan
    {
        public string nama;//membuat varibael nama menjadi string
        public int umur;//membuat varibael umur menjadi umur

        public Hewan(string nama, int umur)//bertujuan untuk memudahkan menginputkan di objek yang akan dibuat sehingga tidak perlu 
            //dilakukan satu persatu dengan menuliskan nama=hewan, umur 3. Akan tetatpi, bisa langsung di dalam argumennya
        {
            this.nama = nama;//memastikan bahwa ini miliknya dengan inisial this.
            this.umur = umur;
        }

        public virtual string Suara()//membuat method non void sehingga harus dipanggil dengan Console.Writeline or Console.Write
        {
            return "Ini hewan";
        }
        public virtual void InfoHewan()// membuat method yang akan mengeluarkan nilainya langsung 
        {
            Console.WriteLine($"Nama: {nama}\nUmur: {umur} tahun");
        }
    }

    class Mamalia : Hewan//melakukan inheritance dengan ciri-ciri "... : ...."
    {
        public int jumlahKaki;//membuat variabel menjadi int dan dapat diakses di mana pun

        public Mamalia(string nama, int umur, int jumlahKaki) : base(nama, umur)//
        {
            this.jumlahKaki = jumlahKaki;
        }
        
        public override string Suara()
        {
            return "Ini mamalia";
        }

        public override void InfoHewan()
        {
            Console.WriteLine(Suara());
            base.InfoHewan();
            Console.WriteLine($"Jumlah kaki: {jumlahKaki}");
        }
    }

    class Singa : Mamalia
    {
        public Singa(string nama, int umur, int jumlahKaki) : base(nama, umur, jumlahKaki)
        {
        }

        public void Mengaum()
        {
            Console.WriteLine("Kharrrrr...");
        }

        public override string Suara()
        {
            return "Ini singa";
        }

        public override void InfoHewan()
        {
            Console.WriteLine(Suara());
            Mengaum();
            base.InfoHewan();
        }
    }

    class Gajah : Mamalia
    {
        public Gajah(string nama, int umur, int jumlahKaki) : base(nama, umur, jumlahKaki)
        {
        }

        public override string Suara()
        {
            return "Ini gajah";
        }

        public override void InfoHewan()
        {
            Console.WriteLine(Suara());
            base.InfoHewan();
        }
    }

    class Reptil : Hewan
    {
        protected double panjangTubuh;

        public Reptil(string nama, int umur, double panjangTubuh) : base(nama, umur)
        {
            this.panjangTubuh = panjangTubuh;
        }

        public override string Suara()
        {
            return "Ini reptil";
        }

        public override void InfoHewan()
        {
            Console.WriteLine(Suara());
            base.InfoHewan();
            Console.WriteLine($"Panjang tubuh: {panjangTubuh} meter");
        }
    }

    class Ular : Reptil
    {
        public Ular(string nama, int umur, double panjangTubuh) : base(nama, umur, panjangTubuh)
        {
        }

        public void Merayap()
        {
            Console.WriteLine("Merayap: Sssss....");
        }
        public override string Suara()
        {
            return "Ini ular";
        }
        public override void InfoHewan()
        {
            Merayap();
            Console.WriteLine(Suara());
            base.InfoHewan();
        }
    }

    class Buaya : Reptil
    {
        public Buaya(string nama, int umur, double panjangTubuh) : base(nama, umur, panjangTubuh)
        {
        }

        public override string Suara()
        {
            return "Ini buaya";
        }

        public override void InfoHewan()
        {
            Console.WriteLine(Suara());
            base.InfoHewan();
        }
    }

    //---------- KebunBinatang ----------
    class KebunBinatang
    {
        public List<Hewan> KoleksiHewan = new List<Hewan>();

        public void TambahHewan(Hewan hewan)
        {
            KoleksiHewan.Add(hewan);
        }

        public void TampilkanKoleksi()
        {
            Console.WriteLine("==== Koleksi hewan di kebun binatang ======");
            foreach (var hewan in KoleksiHewan)
            {
                hewan.InfoHewan();
                Console.WriteLine();
            }
        }
    }
}


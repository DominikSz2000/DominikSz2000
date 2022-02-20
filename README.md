using System;
namespace ConsoleApp1
{
    namespace Dominik Szewczyk_18129

class Program
    {
        static void Main()
        {
            Random random = new Random(); // generator losowych liczb 

            Sword miecz = new Sword(); // stworzenie obieku miecz
            Sword miecz2 = new Sword(); // stworzenie obieku miecz2
            Player player1 = new Player(); // stworzenie obieku player1
            Player player2 = new Player(); // stworzenie obieku player2

            // nadanie im wartości atrybutów
            miecz.SetName("Poskramiacz");
            miecz.SetValue(15);
            miecz.SetDamage(random.Next(1, 5)); // losowe nadanie wartości od 1 do 5

            // nadanie im wartości atrybutów
            miecz2.SetName("Poskramiacz II");
            miecz2.SetValue(25);
            miecz2.SetDamage(random.Next(1, 5)); // losowe nadanie wartości od 1 do 5

            // nadanie im wartości atrybutów
            player1.SetName("Argog");
            player1.SetHp(random.Next(15, 20)); // losowe nadanie wartości od 15 do 20
            player1.SetStr(random.Next(3, 6)); // losowe nadanie wartości od 3 do 6
            player1.SetHand(miecz);

            // nadanie im wartości atrybutów
            player2.SetName("Margog");
            player2.SetHp(random.Next(15, 20)); // losowe nadanie wartości od 15 do 20
            player2.SetStr(random.Next(3, 6)); // losowe nadanie wartości od 3 do 6
            player2.SetHand(miecz2);

            // wyświetlenie 5 gwiazdek
            for (int i = 0; i < 5; i++)
            {
                Console.Write("*");
            }
            // wyświetlenie 5 gwiazdek oraz napisu arena
            Console.Write(" Arena ");
            for (int i = 0; i < 5; i++)
            {
                Console.Write("*");
            }
            Console.WriteLine("");
            Console.WriteLine(player1.name + " vs " + player2.name);
            Console.WriteLine("");
            player1.show_stats(); // wywołanie metody która pokaże statystyki obiektu player1
            Console.WriteLine("");
            player2.show_stats(); // wywołanie metody która pokaże statystyki obiektu player2
            Console.WriteLine("");

            // pętla odpowiedzialna za walkę dwóch obiektów
            while (player1.hp > 0 && player2.hp > 0)
            {
                player1.attack(player2); // player1 atakuje player2
                player2.attack(player1); // player2 atakuje player1
            }
            // jeśli player1 ma hp na poziomie mniejszym od 0 tzn, że przegrał i player2 wygrał
            if (player1.hp < 0)
            {
                Console.WriteLine(player2.name + " wygrywa!");
            }
            // w innym przypadku wygrał player1
            else
            {
                Console.WriteLine(player1.name + " wygrywa!");
            }

            Console.WriteLine("");
            Console.WriteLine("Program wykonał Dominik Szewczyk.");
        }
    }

    // stworzenie klasy item
    class Item
    {
        public string name; // nazwa itemu
        public int value; // wartosc itemu

        // metody które służą do nadania wartości atrybutom 
        public void SetName(string nm)
        {
            name = nm;
        }

        public void SetValue(int vl)
        {
            value = vl;
        }

        // metody służące do wyświetlenia atrybutów
        public void show_name()
        {
            Console.WriteLine("Nazwa: " + name);
        }

        public void show_value()
        {
            Console.WriteLine("Wartość: " + value);
        }
    }

    // klasa Sword dziedziczy z klasy Item
    class Sword : Item
    {
        public int damage; // obrażenia miecza

        // nadanie wartości obrażeń
        public void SetDamage(int dm)
        {
            damage = dm;
        }

        // pokazanie obrażeń
        public void show_damage()
        {
            Console.WriteLine("Obrażenia: " + damage);
        }
    }

    // określenie gatunku, będzie służyć do zastosowania polimorfizmu
    public class creature
    {
        public virtual void show_type()
        {
            Console.WriteLine("Gatunek istoty: nieznany");
        }
    }

    // klasa Player
    class Player : creature
    {
        public string name; // nazwa
        public int hp; // zdrowie
        public int str; // siła
        public int dmg = 0; // obrażenia zadawane przez miecz
        public string hand = ""; // nazwa miecza trzymanego w dłoni

        // nadpisujemy metodę z klasy creature
        public override void show_type()
        {
            Console.WriteLine("Gatunek istoty: człowiek");
        }

        // metody do ustawiania wartości atrybutów
        public void SetName(string nm)
        {
            name = nm;
        }

        public void SetHp(int hp_vl)
        {
            hp = hp_vl;
        }

        public void SetStr(int strong)
        {
            str = strong;
        }

        // nadanie wartości atrybutom dmg i hand wartościami odpowiadającymi wartością obiektu sword
        public void SetHand(Sword sword)
        {
            hand = sword.name;
            dmg = sword.damage;
        }

        // pokazanie statystyk gracza
        public void show_stats()
        {
            Console.WriteLine("Statystyki: " + name);
            Console.WriteLine("HP: " + hp);
            Console.WriteLine("Siła: " + str);
            Console.WriteLine("Trzyma w ręce broń: " + hand + " zadający " + dmg + " obrażeń.");
        }

        // metoda odpowiadająca za atakowanie gracza
        public void attack(Player attack_player)
        { // attack_player jest to osoba atakowana
            attack_player.hp = attack_player.hp - str - dmg; // od zdrowia osoby atakowanej odejmowane jest siła i obrażenia osoby atakującej
            Console.WriteLine(name + " atakuje " + attack_player.name + " zadając " + (str + dmg) + " obrażeń");
            if (attack_player.hp < 0)
            { // jeśli osoba atakowana ma mniej niż 0 zdrowia to otrzymuje śmiertelne obrażenia
                Console.WriteLine("");
                Console.WriteLine(attack_player.name + " otrzymuje śmiertelne obrażenia!");
            }
        }
    }
    }
}

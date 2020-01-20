# hash-table-class-Vini-WCGS
hash-table-class-Vini-WCGS created by GitHub Classroom
Vini's Hash Table Class

            HashTable Hashtable1 = new HashTable();  //creates a new instance of the HashTable Class an calls it 'Hashtable1'
            int [] table = new int [11] {-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,};

            int option = 0;
            while (option != 6)
               
            {
                Console.ForegroundColor = ConsoleColor.Blue;
                Console.WriteLine("Please choose an option: \n 1) Add to hash table\n 2) Search hash table\n 3) Delete hash entry\n " +
                    "4) Return all values in the hash table\n 5) Output load factor\n 6) Quit" );
                Console.ForegroundColor = ConsoleColor.Cyan; 
                option = Convert.ToInt32(Console.ReadLine());
                Console.ForegroundColor = ConsoleColor.Magenta;
                if (option == 1) //add
                {
                    Hashtable1.AddValue(ref table);         //calls method in the HashTable Class to add a value
                }
                if (option == 2)
                {
                    Hashtable1.SearchTable(ref table);     //calls method in the HashTable Class to search for a value
                }
                if (option == 3)
                {
                    Hashtable1.DeleteEntry(ref table);     //calls method in the HashTable Class to delete a value
                }
                if (option == 4)
                {
                    Console.WriteLine();
                    int k = 0;
                    foreach (var item in table)
                    {
                        Console.WriteLine("[" + k + "]" + "\t" + item.ToString());
                        k = k + 1;
                    }
                }
                if (option == 5)
                {
                    Hashtable1.LoadFactor(ref table);        //calls method in the HashTable Class to find the load factor
                }
                if (option == 6)
                {
                    Console.WriteLine("Goodbye.");
                }
                Console.WriteLine();
            }
        }
    }

    public class HashTable
    {
        

       public void AddValue(ref int[] table)
       {
            Console.WriteLine("Please enter the value you would like to add:");
            int value = Convert.ToInt32(Console.ReadLine());
            int place = value % 11;
            for (int i = 0; i < 12; i++)
            {
                if (table[place] != -1 && table[place] != -2)
                {
                    place = (place + 1) % 11;
                    i = i + 1;
                    if (i == 11)
                    {
                        Console.WriteLine("Sorry, can't add this value because the hash table is full");
                    }
                }

                if (table[place] == -1 || table[place] == -2)
                {
                    table[place] = value;
                    i = 11;
                }

            }
       }
        public void SearchTable(ref int[] table)
        {
            Console.WriteLine("Please enter the value you would like to search for:");
            int value = Convert.ToInt32(Console.ReadLine());
            int place = value % 11;
            for (int i = 0; i < 12; i++)
            {
                if (table[place] != value)
                {
                    place = place + 1;
                    i = i + 1;
                    if (i == 11 || table[place] == -1)
                    {
                        i = 11;
                        Console.WriteLine("Sorry, this value is not stored in the table");
                    }
                }
            }
            if (table[place] == value)
            {
                Console.WriteLine("{0} is in location {1}", value, place);
            }
        }
        public void DeleteEntry (ref int[] table)
        {
            Console.WriteLine("Please enter the value you would like to delete:");
            int value = Convert.ToInt32(Console.ReadLine());
            int place = value % 11;
            for (int i = 0; i < 12; i++)
            {
                if (table[place] != value)
                {
                    place = place + 1;
                    i = i + 1;
                    if (i == 11 || table[place] == -1)
                    {
                        i = 11;
                        Console.WriteLine("Sorry, this value is not stored in the table");
                    }
                }
            }
            if (table[place] == value)
            {
                table[place] = -2;      // "-2" stands for deleted
            }
        }
        public void LoadFactor(ref int[] table)
        {
            int key = 0;
            foreach (var item in table)
            {
                if (item != -1 && item != -2)
                {
                    key = key + 1;
                }
            }
            decimal loadFactor = key / 11M;
            Console.WriteLine("The load factor is: {0}", Math.Round(loadFactor, 2));
        }   
    }

# Tugas-Akhir-Algortma
#include &lt;iostream> #include &lt;iomanip> #include &lt;limits>  using namespace std;   class Parkir {     //wadah atau prosedur (objek)   private:  //fungsi internal     struct Node {           int plat;         Node* next;     };       Node* head;     Node* tail;       static int size;     static int pendapatan;       int getSize() const;     int getPendapatan() const;     bool isTrue(int) const;   public: //fungsi yang dapat di akses umum       Parkir();     bool isEmpty() const;     void menu();     void addPlat(int);     void deletePlat(int);     void displayPendapatan();     void display(); }; // pendapatan = 0 //   int Parkir::pendapatan = 0;   // size = 0 //   int Parkir::size = 0;   // head and tail = null //   Parkir::Parkir() {       head = NULL;     tail = NULL; }   bool Parkir::isEmpty() const { //mengecek antrian apakah kadaan kosong       return head == NULL; }   int Parkir::getSize() const { //banyak data yang sudah masuk       return this->size; }   int Parkir::getPendapatan() const { //menampilkan pendapatan       return this->pendapatan; }   void Parkir::menu() {       cout &lt;&lt; "\n-------------------------------------------------" &lt;&lt; endl;     cout &lt;&lt; "|NO|.\t PARKIRAN UNIVERSITAS PAKUAN" &lt;&lt; endl;     cout &lt;&lt; "|--|---------------------------------------------\n" &lt;&lt; endl;       cout &lt;&lt; "|1.|\tAntrian Motor" &lt;&lt;endl;     cout &lt;&lt; "|2.|\tKeluarkan Motor" &lt;&lt; endl;     cout &lt;&lt; "|3.|\tTampilkan Antrian Motor" &lt;&lt; endl;     cout &lt;&lt; "|4.|\tMenghitung Total Pendapatan" &lt;&lt; endl;     cout &lt;&lt; "|0.|\tExit\n" &lt;&lt; endl;       cout &lt;&lt; "-------------------------------------------------\n" &lt;&lt; endl; }   //menambahkan plat yang masuk//   void Parkir::addPlat(int n) {        this->size++;       Node* temp = new Node;       temp->plat = n;     temp->next = NULL;       if(isEmpty()) {           head = temp;         tail = temp;       } else {           tail->next = temp;         tail = tail->next;     }       cout &lt;&lt; "\n" &lt;&lt; n &lt;&lt; " berhasil ditambahkan" &lt;&lt; endl; }   // is true, cek plat yang dicari ada / tidak //   bool Parkir::isTrue(int n) const {      bool result = false;      Node* temp = head;      while (temp != NULL) {          if(temp->plat == n) {               result = true;         }         temp = temp->next;     }     return result; }   // delete plat //   void Parkir::deletePlat(int n) {       if(isTrue(n)) {           Node* current = head;         Node* prev = NULL;           if(current->next == NULL) {               cout &lt;&lt; "\n" &lt;&lt; current->plat &lt;&lt; " sudah dikeluarkan!" &lt;&lt; endl;               delete current;             head = NULL;               this->size--;               this->pendapatan += 1000;           } else {               if(current->plat == n) {                   cout &lt;&lt; "\n" &lt;&lt; current->plat &lt;&lt; " sudah dikeluarkan!" &lt;&lt; endl;                   head = head->next;                 delete current;                   this->size--;                   this->pendapatan += 1000;               } else {                   int pos = 0;                   current = head;                   while (current != NULL) {                       if(current->plat == n) {                           pos++;                         break;                     }                       pos++;                       current = current->next;                 }                   current = head;                   for(int i = 0; i &lt; pos; i++) {                       cout &lt;&lt; "\n" &lt;&lt; current->plat &lt;&lt; " sudah dikeluarkan!";                       prev = current;                     delete current;                       current = current->next;                       this->size--;                       this->pendapatan += 1000;                 }                   head = prev->next;                   cout &lt;&lt; endl;             }         }       } else {           cout &lt;&lt; "\nPlat nomor yang diinputkan tidak ada!" &lt;&lt; endl;     } }   // display pendapatan //   void Parkir::displayPendapatan() {       cout &lt;&lt; "\nPendapatan : " &lt;&lt; getPendapatan() &lt;&lt; endl; }   // display //   void Parkir::display() {       if(isEmpty()) {           cout &lt;&lt; "\nParkiran Kosong!" &lt;&lt; endl;       } else {           cout &lt;&lt; "\nDaftar Plat Kendaraan : \n" &lt;&lt; endl;           int nomor = 1;           Node* temp = head;           while (temp != NULL) {               cout &lt;&lt; (nomor++) &lt;&lt; ". " &lt;&lt; temp->plat &lt;&lt; endl;               temp = temp->next;         }           cout &lt;&lt; "\nTotal Kendaraan : " &lt;&lt; getSize() &lt;&lt; endl;     } } // program parkir dengan implementasi queue //   int main() {       int pilihan, plat;     char answer;     bool isTrue = false;       Parkir* parkir = new Parkir();       do {           parkir->menu();           cout &lt;&lt; "Masukkan Pilihan : ";         cin >> pilihan;           switch (pilihan) {               case 0:                   exit(1);               case 1:                   cout &lt;&lt; "\nMasukkan Plat Nomor : ";                 cin >> plat;                   while (!cin) {                       cout &lt;&lt; "\nInput hanya angka!" &lt;&lt; endl;                       cin.clear();                     cin.ignore(numeric_limits&lt;streamsize>::max(), '\n');                       cout &lt;&lt; "\nMasukkan Plat Nomor : ";                     cin >> plat;                 }                   parkir->addPlat(plat);                   BACK1:                 cout &lt;&lt; "\nKembali ke menu? (y/N) : ";                 cin >> answer;                   if(answer == 'y' || answer == 'Y') {                       isTrue = true;                   } else if(answer == 'n' || answer == 'N') {                       isTrue = false;                   } else {                       cout &lt;&lt; "\nKode Salah!" &lt;&lt; endl;                       goto BACK1;                 }                   break;               case 2:                   if(parkir->isEmpty()) {                       parkir->display();                       BACK2:                     cout &lt;&lt; "\nKembali ke menu? (y/N) : ";                     cin >> answer;                       if(answer == 'y' || answer == 'Y') {                           isTrue = true;                       } else if(answer == 'n' || answer == 'N') {                           isTrue = false;                       } else {                           cout &lt;&lt; "\nKode Salah!" &lt;&lt; endl;                           goto BACK2;                     }                   } else {                       parkir->display();                       cout &lt;&lt; "\nPlat yang dihapus : ";                     cin >> plat;                       while (!cin) {                           cout &lt;&lt; "\nInput hanya angka!" &lt;&lt; endl;                           cin.clear();                         cin.ignore(numeric_limits&lt;streamsize>::max(), '\n');                           cout &lt;&lt; "\nMasukkan Plat Nomor : ";                         cin >> plat;                     }                       parkir->deletePlat(plat);                       BACK3:                     cout &lt;&lt; "\nKembali ke menu? (y/N) : ";                     cin >> answer;                       if(answer == 'y' || answer == 'Y') {                           isTrue = true;                       } else if(answer == 'n' || answer == 'N') {                           isTrue = false;                       } else {                           cout &lt;&lt; "\nKode Salah!" &lt;&lt; endl;                           goto BACK3;                     }                 }                   break;               case 3:                   parkir->display();                   BACK4:                 cout &lt;&lt; "\nKembali ke menu? (y/N) : ";                 cin >> answer;                   if(answer == 'y' || answer == 'Y') {                       isTrue = true;                   } else if(answer == 'n' || answer == 'N') {                       isTrue = false;                   } else {                       cout &lt;&lt; "\nKode Salah!" &lt;&lt; endl;                       goto BACK4;                 }                   break;               case 4:                   parkir->displayPendapatan();                   BACK5:                 cout &lt;&lt; "\nKembali ke menu? (y/N) : ";                 cin >> answer;                   if(answer == 'y' || answer == 'Y') {                       isTrue = true;                   } else if(answer == 'n' || answer == 'N') {                     isTrue = false;                   } else {                     cout &lt;&lt; "\nKode Salah!" &lt;&lt; endl;                   goto BACK5;                 }                 break;             default:                   cout &lt;&lt; "\nKode Salah!" &lt;&lt; endl;                   BACK6:                  cout &lt;&lt; "\nKembali ke menu? (y/N) : ";                 cin >> answer;                  if(answer == 'y' || answer == 'Y') {                     isTrue = true;                  } else if(answer == 'n' || answer == 'N') {                     isTrue = false;                  } else {                      cout &lt;&lt; "\nKode Salah!" &lt;&lt; endl;                      goto BACK6;                 }                 break;         }     } while (isTrue);     delete parkir;       return 0; }

# Fork: Parent - Child Process

##  1. Konsep fork()

fork() adalah system call di UNIX/Linux untuk membuat proses baru dengan menyalin proses pemanggil (parent). Proses baru disebut child dan berjalan paralel.

Return Value:
- 0 → Child process
- PID child → Parent process
- -1 → Gagal

### Fork01.cpp

```cpp
using namespace std;

#include <iostream>
#include <sys/types.h>
#include <unistd.h>

/* getpid() adalah system call yg dideklarasikan pada unistd.h.
Menghasilkan suatu nilai dengan type pid_t.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/
int main(void) {
        pid_t mypid;
        uid_t myuid;
        for (int i = 0; i < 3; i++) {
                mypid = getpid();
                cout << "I am process " << mypid << endl;
                cout << "My parent process ID is " << getppid() << endl;
                cout << "The owner of this process has uid " << getuid()
        << endl;
/* sleep adalah system call atau fungsi library
yang menghentikan proses ini dalam detik
*/
        sleep(3);
        }
return 0;
```

Program ini hanya menggunakan 1 proses (tidak ada child process).

**Fungsi Utama:**
- getpid() → ID proses saat ini
- getppid() → ID parent process
- getuid() → ID user
- sleep(3) → Jeda eksekusi 3 detik

Program melakukan loop 3x, mencetak info proses tiap iterasi.

### Fork02.cpp

```cpp
#include <iostream>
#include <sys/types.h>
#include <unistd.h>
using namespace std;

/* getpid() dan fork() adalah system call yg dideklarasikan
pada unistd.h.
Menghasilkan suatu nilai dengan type pid_t.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/
int main(void) {
        pid_t childpid;
        int x = 5;
        childpid = fork();

        while (1) {
                cout << "This is process ID" << getpid() << endl;
                cout << "In this process the value of x becomes " << x << endl;
                sleep(2);
                x++;
        }
        return 0;
}
```

**Fork() dan Proses Duplikasi**
- fork() membuat duplikat proses (parent & child)
- Keduanya menjalankan kode yang sama mulai dari baris setelah fork()
- Variabel x terpisah (tidak shared)

**Loop Infinite:**
- Parent & child masuk while(1), cetak:
  - PID proses
  - Nilai x (bertambah +1 tiap 2 detik)
- Nilai x berbeda antara parent dan child

### Fork03.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>

/* getpid() dan fork() adalah system call yg dideklarasikan
pada unistd.h.
Menghasilkan suatu nilai dengan type pid_t.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/
int main(void) {
        pid_t childpid;
        childpid = fork();
        for (int i = 0; i < 5; i++) {
                cout << "This is process " << getpid() << endl;
                sleep(2);
        }
        return 0;
}
```

**Eksekusi fork() dan Loop**
- fork() membuat 1 child process
- Parent & child sama-sama menjalankan loop 5x
- Tiap iterasi mencetak:
  - PID proses (getpid())
  - sleep(2)

**Karakteristik:**
- Loop dijalankan paralel oleh parent & child
- PID berbeda menunjukkan proses terpisah

### Fork04.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>
/* pid_t fork() dideklarasikan pada unistd.h.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/

int main(void) {
        pid_t child_pid;
        int status;
        pid_t wait_result;
        child_pid = fork();
        if (child_pid == 0) {
                /* kode ini hanya dieksekusi proses child */
                cout << "I am a child and my pid = " << getpid() << endl;
                cout << "My parent is " << getppid() << endl;
                /* keluar if akan menghentikan hanya proses child */
        }
        else if (child_pid > 0) {
                /* kode ini hanya mengeksekusi proses parent */
                cout << "I am the parent and my pid = " << getpid() << endl;
                cout << "My child has pid = " << child_pid << endl;
        }
        else {
                cout << "The fork system call failed to create a new process" << endl;
                exit(1);
        }
                /* kode ini dieksekusi baik oleh proses parent dan child */
                cout << "I am a happy, healthy process and my pid = " << getpid() << endl;
                if (child_pid == 0) {
                /* kode ini hanya dieksekusi oleh proses child */
                cout << "I am a child and I am quitting work now!"<< endl;
        }
        else {
                /* kode ini hanya dieksekusi oleh proses parent */
                cout << "I am a parent and I am going to wait for my child" << endl;
        do {
                /* parent menunggu sinyal SIGCHLD mengirim tanda bahwa proses child diterminasi */
                wait_result = wait(&status);
        } while (wait_result != child_pid);
                cout << "I am a parent and I am quitting." << endl;
        }
        return 0;
}
```

**Alur Program dengan fork() dan wait()**

1. Child Process:
    - Cetak PID sendiri (getpid()) dan PID parent (getppid())
    - Tampilkan pesan "Child selesai"
    - Exit
2. Parent Process:
    - Cetak PID sendiri dan PID child
    - wait(&status) → pause sampai child selesai
    - Tampilkan pesan "Parent keluar"

**Pentingnya wait():**
- Mencegah zombie process
- Memastikan parent menunggu child selesai

### Fork05.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>
/* pid_t fork() dideklarasikan pada unistd.h.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/

int main(void) {
  pid_t child_pid;
  int status;
  pid_t wait_result;
  child_pid = fork();
  if (child_pid == 0) {
    /* kode ini hanya dieksekusi proses child */
    cout << "I am a child and my pid = " << getpid() << endl;
    execl("/bin/ls", "ls", "-l", "/home", NULL);
    /* jika execl berhasil kode ini tidak pernah digunakan */
    cout << "Could not execl file /bin/ls" << endl;
    exit(1);
    /* exit menghentikan hanya proses child */
   }
  else if (child_pid > 0) {
    /* kode ini hanya mengeksekusi proses parent */
   cout << "I am the parent and my pid = " << getpid() << endl;
   cout << "My child has pid = " << child_pid << endl;
  }
 else {
   cout << "The fork system call failed to create a new process" << endl;
   exit(1);
  }
  /* kode ini hanya dieksekusi oleh proses parent karena
  child mengeksekusi dari "/bin/ls" atau keluar */
   cout << "I am a happy, healthy process and my pid = " << getpid() << endl;
   if (child_pid == 0) {
  /* kode ini tidak pernah dieksekusi */
   printf("This code will never be executed!\n");
  }
  else {
   /* kode ini hanya dieksekusi oleh proses parent */
    cout << "I am a parent and I am going to wait for my child" << endl;
    do {
      /* parent menunggu sinyal SIGCHLD mengirim tanda bila proses child diterminasi */
      wait_result = wait(&status);
    } while (wait_result != child_pid);
    cout << "I am a parent and I am quitting." << endl;
  }
  return 0;
}
```

**Eksekusi fork() + execl()**
Parent Process:
  - Buat child (fork())
  - Cetak info proses
  - Tunggu child (wait())

Child Process:
  - Cetak info proses
  - Ganti program dengan execl("ls -l /home")
    - Jika sukses: kode setelahnya tidak dijalankan
    - Jika gagal: cetak error

**Fungsi Kunci:**
  - fork(): duplikasi proses
  - execl(): ganti program child
  - wait(): sinkronisasi parent-child

### Fork06.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>
/* pid_t fork() dideklarasikan pada unistd.h.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/

int main(void) {
        pid_t child_pid;
        int status;
        pid_t wait_result;
        child_pid = fork();
int main(void) {
        pid_t child_pid;
        int status;
        pid_t wait_result;
        child_pid = fork();


        if (child_pid == 0) {
                /* kode ini hanya dieksekusi proses child */
                cout << "I am a child and my pid = " << getpid() << endl;
                execl("fork03", "goose", NULL);
                /* jika execl berhasil kode ini tidak pernah digunakan */
                cout << "Could not execl file fork3" << endl;
                exit(1);
                /* exit menghentikan hanya proses child */
        }
        else if (child_pid > 0) {
                /* kode ini hanya mengeksekusi proses parent */
                cout << "I am the parent and my pid = " << getpid()<< endl;
                cout << "My child has pid = " << child_pid << endl;
        }
        else {
                cout << "The fork system call failed to create a new process" << endl;
                exit(1);
        }
        /* kode ini hanya dieksekusi oleh proses parent karena
        child mengeksekusi dari "fork3" atau keluar */
                cout << "I am a happy, healthy process and my pid = " << getpid() << endl;
                if (child_pid == 0) {
        /* kode ini tidak pernah dieksekusi */
                printf("This code will never be executed!\n");
        }
        else {
        /* kode ini hanya dieksekusi oleh proses parent */
                cout << "I am a parent and I am going to wait for my child" << endl;
                do {
                /* parent menunggu sinyal SIGCHLD mengirim tanda
                bila proses child diterminasi */
                        wait_result = wait(&status);
                } while (wait_result != child_pid);
                cout << "I am a parent and I am quitting." << endl;
        }
        return 0;
}
```

**Eksekusi Program dengan fork() dan execl()**

Parent Process:
- Buat child process menggunakan fork()
- Tampilkan PID parent dan child
- Tunggu child selesai dengan wait()

Child Process:
- Tampilkan PID child
- Jalankan program eksternal fork03 menggunakan execl()
- Jika berhasil: ganti proses dengan fork03
- Jika gagal: tampilkan error dan exit(1)

Catatan Penting:
- Program fork03 harus sudah tercompile sebagai executable
- Harus berada di direktori yang sama
- wait() mencegah zombie process
- exit(1) menghentikan child jika eksekusi gagal
exit(1) menghentikan child jika eksekusi gagal

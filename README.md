# Guess-the-number-Game
Alright, let’s break this **line by line** and explain in simple terms.

---

### 1️⃣ `#include <stdio.h>`

* **What it is:**

  * `stdio` stands for **Standard Input/Output**.
  * This library allows your program to **read input** and **print output**.

* **Functions it provides:**

  * `printf()` → print text to the screen
  * `scanf()` → read input from the user
  * `getchar()`, `putchar()` → read/write a single character
  * `fgets()`, `fputs()` → read/write strings

* **If you remove it:**

  * Any line using `printf`, `scanf`, or other I/O functions will **cause a compilation error**.

**Example:**

```c
printf("Hello world\n"); // needs stdio.h
```

---

### 2️⃣ `#include <time.h>`

* **What it is:**

  * This library is used for **time and date operations**.

* **Functions it provides:**

  * `time()` → get the current time
  * `clock()` → measure program execution time
  * `localtime()` → convert time to local date/time
  * `difftime()` → difference between two times

* **Example usage:**

```c
time_t t;
t = time(NULL);           // get current time in seconds since 1970
printf("%ld\n", t);
```

* **If you remove it:**

  * Any function that deals with **time or date** (like `time()`, `localtime()`, `sleep()` on some systems) will **not work**.

---

### 3️⃣ `#include <stdlib.h>`

* **What it is:**

  * Stands for **Standard Library**.
  * Provides general-purpose functions for **memory, process control, random numbers, and conversions**.

* **Functions it provides:**

  * `malloc()`, `free()` → dynamic memory allocation
  * `rand()`, `srand()` → random numbers
  * `exit()` → exit the program
  * `system()` → run a system command like `clear` or `dir`

* **Example usage:**

```c
int r = rand() % 100;  // random number 0–99
system("clear");       // clear screen on Linux/Unix
```

* **If you remove it:**

  * Functions like `malloc`, `rand`, `system`, and `exit` will **not compile**.

---

### ⚠️ Common mistakes

In your code you wrote:

```c
#include<stdlib>
```

* ❌ Wrong! It must be:

```c
#include <stdlib.h>
```

* All standard libraries in C **end with `.h`**

---

### ✅ TL;DR

| Library    | Purpose                         | What breaks if removed?         |
| ---------- | ------------------------------- | ------------------------------- |
| `stdio.h`  | Input/Output (printf, scanf)    | Any printing or input fails     |
| `time.h`   | Work with date/time             | Time-related functions fail     |
| `stdlib.h` | Memory, random, system commands | malloc, rand, system, exit fail |

---

If you want, I can make a **tiny example program** showing all **3 libraries in action** so you can see exactly why each one is needed.

Do you want me to do that?
    =  =  ==  =  =  =  =  =  =  =  =  =  ==  =  =  =  =  =  =  =  =  ==  =  =  ==  =  =  =  

    Sure! Let’s keep it **super simple**.

---

### 1️⃣ `rand()` syntax

```c
int rand(void);
```

* Returns a **pseudo-random integer** between **0 and RAND_MAX** (usually 32767).
* Example:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int r = rand();      // get a random number
    printf("%d\n", r);
    return 0;
}
```

* To get numbers in a range (e.g., 0–99):

```c
int r = rand() % 100;  // 0–99
```

---

### 2️⃣ `srand()` syntax

```c
void srand(unsigned int seed);
```

* Sets the **starting point (seed)** for `rand()`.
* Usually, we use **time as a seed** so numbers are different each run:

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    srand(time(0));       // seed with current time

    for(int i = 0; i < 5; i++) {
        printf("%d\n", rand() % 100); // random number 0–99
    }

    return 0;
}
```

* `time(0)` → returns **current seconds** since 1970.

---

### ✅ TL;DR

| Function | Syntax            | Purpose                                     |
| -------- | ----------------- | ------------------------------------------- |
| `rand`   | `int r = rand();` | Generates pseudo-random numbers             |
| `srand`  | `srand(seed);`    | Sets the starting point for rand() sequence |

---

  =  =    ==    ==  =  =  =  =  =  =  =  =  =  ==  =    ==  =
  No worries! Let’s **slow down completely** and explain `srand` and `rand` in the simplest possible way, step by step, with an **analogy**.

---

### 1️⃣ Think of `rand()` as a dice

* `rand()` is like a **dice machine** that gives you numbers.
* But here’s the catch: it **always starts from the same position**.

Example: if you roll it 5 times, it might **always give the same numbers**:

```
41, 67, 23, 89, 5
```

Even if you stop and run the program again, it **gives the same numbers**.

---

### 2️⃣ `srand()` = “shuffle the dice”

* `srand(seed)` tells the dice **where to start rolling from**.

* `seed` is a number that decides the starting point of the sequence.

* Commonly, we use **time** as the seed:

```c
srand(time(0));
```

* `time(0)` → gives **current seconds** (always different each moment)
* Now the dice starts in a **different position** every time you run the program → truly “random” numbers.

---

### 3️⃣ Example: With and without `srand`

**Without `srand`:**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    for(int i=0;i<5;i++)
        printf("%d\n", rand() % 100);
    return 0;
}
```

* Output **always the same**, like a broken dice:

```
41 67 23 89 5
```

**With `srand(time(0))`:**

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    srand(time(0));  // shuffle dice
    for(int i=0;i<5;i++)
        printf("%d\n", rand() % 100);
    return 0;
}
```

* Output **changes every time** you run the program:

```
12 87 3 56 41
```

Next run:

```
34 2 65 11 90
```

---

### 4️⃣ Simple TL;DR

* `rand()` → gives numbers (pseudo-random)
* `srand(seed)` → decides where the number sequence **starts**
* `srand(time(0))` → makes the sequence **different every time you run the program**

---

If you want, I can make a **tiny diagram with dice and arrows** showing **how `rand()` numbers change with and without `srand`**, so it will make it **super visual and easy to understand**.



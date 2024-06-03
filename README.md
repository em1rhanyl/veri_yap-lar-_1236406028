# veri_yap-lar-_1236406028

#include <stdio.h>

// Insertion Sort algoritması
void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        // Sıralanmış kısımdaki elemanlar arasında arama yapılır
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Diziyi ekrana yazdıran fonksiyon
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int X[500]; // 500 elemanlı dizi
    int min = 0; // Minimum değer
    int max = 1000; // Maksimum değer

    // Diziyi rasgele sayılarla doldur
    for (int i = 0; i < 500; i++) {
        X[i] = min + rand() % (max - min + 1);
    }

    int n = sizeof(X) / sizeof(X[0]);

    printf("Oluşturulan rasgele dizi:\n");
    printArray(X, n);

    // Insertion Sort'u uygula
    insertionSort(X, n);

    printf("Sıralanmış dizi:\n");
    printArray(X, n);

    return 0;
}
/*2.*/
#include <stdio.h>

// Selection Sort algoritması
void selectionSort(int arr[], int n) {
    int i, j, minIndex, temp;
    for (i = 0; i < n - 1; i++) {
        minIndex = i;
        for (j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex])
                minIndex = j;
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}

// Diziyi ekrana yazdıran fonksiyon
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int X[500]; // 500 elemanlı dizi
    int min = 0; // Minimum değer
    int max = 1000; // Maksimum değer

    // Diziyi rasgele sayılarla doldur
    for (int i = 0; i < 500; i++) {
        X[i] = min + rand() % (max - min + 1);
    }

    int n = sizeof(X) / sizeof(X[0]);

    printf("Oluşturulan rasgele dizi:\n");
    printArray(X, n);

    // Selection Sort'u uygula
    selectionSort(X, n);

    printf("Sıralanmış dizi:\n");
    printArray(X, n);

    return 0;
}

#include <stdio.h>

// Selection Sort algoritması
void selectionSort(int arr[], int n) {
    int i, j, maxIndex, temp;
    for (i = 0; i < n - 1; i++) {
        maxIndex = i;
        for (j = i + 1; j < n; j++) {
            if (arr[j] > arr[maxIndex])
                maxIndex = j;
        }
        temp = arr[i];
        arr[i] = arr[maxIndex];
        arr[maxIndex] = temp;
    }
}

// Diziyi ekrana yazdıran fonksiyon
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int X[6] = {60, 80, 3, 9, 57, 11}; // 6 elemanlı dizi

    printf("Oluşturulan dizi:\n");
    printArray(X, 6);

    // Selection Sort'u uygula
    selectionSort(X, 6);

    printf("Sıralanmış dizi:\n");
    printArray(X, 6);

    return 0;
}
Trie (Metin Ağacı), metinleri ve karakter dizilerini depolamak ve aramak için kullanılan bir veri yapısıdır. Aynı zamanda önek ağacı olarak da bilinir. Trie, her düğümün kendisinden sonra gelen harfi işaret ettiği bir ağaçtır. Bu nedenle metinlerin hızlı bir şekilde aranmasını sağlar.

Trie’nin çalışma şekli şu adımları içerir:

Kök Düğüm (Root Node): Trie’nin başlangıç noktasıdır ve her zaman boş bir metni ifade eder.
Düğümler (Nodes): Her düğüm bir harfi temsil eder. Bir düğümden bir harf taşıyan sadece bir kol çıkabilir.
Yollar (Paths): Düğümler arasındaki yollar, metinlerin kodlanmasını sağlar.
 Bir düğümün yolunu takip ederek metinler arasında gezinebiliriz.
Metin Kodlama: Metinler, Trie üzerinde tek bir yol izleyerek kodlanır.
 Bu, metni veren ağacın üzerindeki düğümlerin birleştirilmiş halidir.
Arama İşlemi: Verilen bir metni Trie’de aramak, metin boyutu kadar işlem gerektirir.
 Bu, ikili arama ağaçlarına göre büyük bir avantajdır. İkili arama ağaçlarında bu süre log n kadar varkit almaktadır.
 #include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Trie düğüm yapısı
struct TrieNode {
    struct TrieNode* children[26]; // 26 harf için alt düğümler
    int isEndOfWord; // Kelimenin sonu mu?
};

// Yeni bir Trie düğümü oluştur
struct TrieNode* createNode() {
    struct TrieNode* newNode = (struct TrieNode*)malloc(sizeof(struct TrieNode));
    newNode->isEndOfWord = 0;
    for (int i = 0; i < 26; i++) {
        newNode->children[i] = NULL;
    }
    return newNode;
}

// Trie'ye kelime ekle
void insert(struct TrieNode* root, const char* word) {
    struct TrieNode* current = root;
    for (int i = 0; i < strlen(word); i++) {
        int index = word[i] - 'a';
        if (!current->children[index]) {
            current->children[index] = createNode();
        }
        current = current->children[index];
    }
    current->isEndOfWord = 1;
}

// Trie'de kelime ara
int search(struct TrieNode* root, const char* word) {
    struct TrieNode* current = root;
    for (int i = 0; i < strlen(word); i++) {
        int index = word[i] - 'a';
        if (!current->children[index]) {
            return 0; // Kelime bulunamadı
        }
        current = current->children[index];
    }
    return current->isEndOfWord; // Kelime bulundu mu?
}

int main() {
    struct TrieNode* root = createNode();

    // Örnek kelimeleri Trie'ye ekle
    insert(root, "apple");
    insert(root, "app");
    insert(root, "banana");

    // Kelime arama örnekleri
    printf("Kelime 'apple' Trie'de %s.\n", search(root, "apple") ? "bulundu" : "bulunamadı");
    printf("Kelime 'app' Trie'de %s.\n", search(root, "app") ? "bulundu" : "bulunamadı");
    printf("Kelime 'orange' Trie'de %s.\n", search(root, "orange") ? "bulundu" : "bulunamadı");

    return 0;
}
s